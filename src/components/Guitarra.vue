<script setup>
    import {ref} from "vue"
    const props = defineProps ({guitarra: {type: Object, require: true}})
    const numero = ref(0)
</script>

<template>
     <div class="col-md-6 col-lg-4 my-4 row align-items-center">
        <div class="col-4">
            <img class="img-fluid" :src="'/img/'+ guitarra.imagen + '.jpg'" :alt="'imagen guitarra' + guitarra.nombre">
        </div>
        <p>{{ numero }}</p>>
        <div class="col-8">
            <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitarra.nombre }}</h3>
            <p>{{ guitarra.descripcion }}</p>
            <p class="fw-black text-primary fs-3">${{ guitarra.precio }}</p>
            <button 
                type="button"
                class="btn btn-dark w-100 "
                v-on:click="numero++"
            >Agregar al Carrito</button>
        </div>
    </div>
</template>



<style lang="scss" scoped>

</style>