<script setup>
    import {ref, reactive} from "vue"
    import {db} from "./data/db.js"
    import Header from "./components/Header.vue";
    import Guitarra from "./components/Guitarra.vue";
    const state = reactive({
        guitarras: db
    })

    console.log(state.guitarras)
</script>

<template>
  <body>
    <Header/>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
           <Guitarra v-for="guitarra in state.guitarras"
            :guitarra="guitarra"
           />
        </div>
    </main>


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>
</body>
</template>

<style scoped>

</style>
