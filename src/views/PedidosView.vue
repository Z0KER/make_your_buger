<template>
    <main class="main-container">
        <section>
            <h1>Gerenciar pedidos:</h1>
        </section>
        <DashboardComponent/>
    </main>
</template>

<script>
import DashboardComponent from '../components/DashboardComponent.vue'

export default {
    name: 'PedidosView',
    components: {
        DashboardComponent
    }
}
</script>