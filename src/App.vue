<script setup>
    import {ref, onMounted, watch} from "vue"
    import {db} from "./data/db.js"
    import Header from "./components/Header.vue";
    import Guitarra from "./components/Guitarra.vue";
    import Footer from "./components/Footer.vue";
    import Swal from "sweetalert2";

    const guitarras = ref([])
    const carrito = ref([])

    onMounted(() => {
        guitarras.value = db
        const carritoStorage = localStorage.getItem('carrito')
        if(carritoStorage){
            carrito.value = JSON.parse(carritoStorage)
        }
    })

    watch(carrito, () => {
            guardarCarritoLocalStorage()
        }, {
            deep: true
        }
    )

    const guardarCarritoLocalStorage = () => {
        localStorage.setItem('carrito', JSON.stringify(carrito.value))
    }

    const AgregarCarrito = (guitarra) => {
        if(carrito.value.includes(guitarra)){
            guitarra.cantidad++
        }else{
            guitarra.cantidad = 1
            carrito.value.push(guitarra)
        }  
        Swal.fire({
            title: 'Exito',
            text: 'La guitarra ha sido agregada con exito',
            icon: 'success',
            confirmButtonText: 'Ok'
        })
    }

    const IncrementarGuitarra = (guitarra) => {
        guitarra.cantidad++
    }

    const DescrementarGuitarra = (guitarra) =>{
        if(guitarra.cantidad <= 1) return
        guitarra.cantidad--
    }

    const eliminarGuitarra = (guitarra) => {
        carrito.value = carrito.value.filter(item => item.id != guitarra.id)
    }

    const vaciarCarrito = () => {
        carrito.value = []
    }
    

</script>

<template>
    <body>
        <Header
            :carrito="carrito"
            @incrementar-guitarra="IncrementarGuitarra"
            @descrementar-guitarra="DescrementarGuitarra"
            @eliminar-guitarra="eliminarGuitarra"
            @vaciar-carrito="vaciarCarrito"
        />
        <main class="container-xl mt-5">
            <h2 class="text-center">Nuestra Colección</h2>
            <div class="row mt-5">
            <Guitarra v-for="guitarra in guitarras"
                :guitarra="guitarra"
                @agregar-carrito="AgregarCarrito"
            />
            </div>
        </main>
        <Footer/>
    </body>
</template>
