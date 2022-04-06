<template>
    <section>
        <MessageComponent :msg="msg" v-show="msg"/>
        <table id="burger-table">
            <thead>
                <tr>
                    <th class="order-id">#:</th>
                    <th>Cliente:</th>
                    <th>Pão:</th>
                    <th>Carne:</th>
                    <th>Opcionais:</th>
                    <th>Ações:</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="burger in burgers" :key="burger.id">
                    <td class="order-number">{{ burger.id }}</td>
                    <td>{{ burger.nome }}</td>
                    <td>{{ burger.pao }}</td>
                    <td>{{ burger.carne }}</td>
                    <td>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index"> {{ opcional }}</li>
                        </ul>
                    </td>
                    <td>
                        <select name="satus" class="status" @change="updateBurger($event, burger.id)">
                            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">{{ s.tipo }}</option>
                        </select>
                        <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                    </td>
                </tr>
            </tbody>
        </table>

    </section>
</template>

<script>
import MessageComponent from './MessageComponent.vue'


export default {
    name: 'DashboardComponent',
    components: {
        MessageComponent
    },
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos() {
            const req = await fetch('http://localhost:3000/burgers')

            const data = await req.json()

            this.burgers = data

            this.getStatus()
        },
        async getStatus() {
            const req = await fetch('http://localhost:3000/status')

            const data = await req.json()

            this.status = data
        },
        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE'
            })
            
            const res = await req.json()

            this.msg = `Pedido removido com sucesso!`

            setTimeout(() => this.msg = '', 3000)

            this.getPedidos()
        },
        async updateBurger(event, id) {
            const option = event.target.value

            const dataJson = JSON.stringify({ status: option })

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: dataJson
            })

            const res = await req.json()

            this.msg = `Pedido Nº ${res.id} atualizado para ${res.status}!`

            setTimeout(() => this.msg = '', 3000)

        }
    },
    mounted() {
        this.getPedidos()
    }
}
</script>

<style scoped>
    #burger-table {
        width: 100%;
        margin: 0 auto;
        border-collapse: collapse;
    }

    thead tr {
        border-bottom: 3px solid #333;
    }

    th {
        padding: 12px;
        width: 19%;
        text-align: start;
    }

    tbody tr {
        border: 1px solid #CCC;
    }

    td {
        padding: 12px;
    }

    .order-id, .order-number {
        width: 5%;
    }

    select {
        padding: 10px 4px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 14px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>