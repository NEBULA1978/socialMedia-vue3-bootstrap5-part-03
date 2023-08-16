<template>
    <div class="container">
        <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
        <h3 class="precio">Precio: {{ productos[contador].precio }}€</h3>
        <div class="todosLosDias dias" v-if="productos[contador].finDeSemana === true">(Solo fines de semana)</div>
        <div class="dias soloFinesDeSemana" v-else>(De Lunes a Domingo)</div>
        <div v-if="productos[contador].precio < 100" class="oferta">
            <div>Ahorra un 10% dto: {{ nuevoPrecio }}€</div>
            <img src="/oferta.jpg" alt="rey godo en descuento" />
        </div>
        <img :src="imagen" alt="">
        <button @click="siguiente" class="boton">Siguiente ({{ contador + 1 }}/ {{ total }} )</button>
    </div>
</template>

<script setup>
import { ref, computed } from "vue"
import { productos } from "@/datos.js"



const contador = ref(0)
const total = productos.length;
// Define the URL for the images
const ruta = "https://www.html6.es/img/rey_"

const siguiente = () => {
    // Increment the value of contador
    contador.value++
    // Check if contador is greater than or equal to total
    if (contador.value >= total) {
        // If so, reset contador back to 0
        contador.value = 0;
    }
}
const rey = computed(() => {
    const elNombre = productos[contador.value].nombre.toLowerCase()

    return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1)
})

const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})

const nuevoPrecio = computed(() => {
    return Number(productos[contador.value].precio / 1.10).toFixed(2)
})
</script>

<style scoped>
.container {
    text-align: center;
}

.boton {
    margin-top: 20px;
    /* Espacio entre la imagen y el botón */
}

.todosLosDias {
    background-color: green;
}

.soloFinesDeSemana {
    background-color: red;
}

.dias {
    color: white;
    padding: 4px 17px;
    font-size: 0.9em;
    border-radius: 4px;
    margin: 5px 0 10px;
    display: inline-block;
}

.oferta img {
    width: 65px;
    margin: 12px 5px;
}
</style>
