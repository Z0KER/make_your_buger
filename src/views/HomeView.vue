<template>
    <main>
        <BannerComponent/>
        <section class="main-container">
            <h1>Monte o seu burger:</h1>
            <BurgerForm/>
        </section>
    </main>
    
</template>

<script>
    import BannerComponent from '../components/BannerComponent.vue'
    import BurgerForm from '../components/BurgerForm.vue'

    export default {
        name: 'HomeView',
        components: {
            BannerComponent,
            BurgerForm
        }
    }
</script>