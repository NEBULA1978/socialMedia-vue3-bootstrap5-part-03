<template>
    <div class="container">
        <!-- Muestra el número de la cena y el rey godo correspondiente -->
        <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
        <!-- Muestra el precio del producto actual -->
        <h3 class="precio">Precio: {{ productos[contador].precio }}€</h3>
        <!-- Muestra si el producto es solo para fines de semana o todos los días -->
        <div class="todosLosDias dias" v-if="productos[contador].finDeSemana === true">(Solo fines de semana)</div>
        <div class="dias soloFinesDeSemana" v-else>(De Lunes a Domingo)</div>
        <!-- Muestra una oferta si el precio es menor a 100 -->
        <div v-if="productos[contador].precio < 100" class="oferta">
            <div>Ahorra un 10% dto: {{ nuevoPrecio }}€</div>
            <img src="/oferta.jpg" alt="rey godo en descuento" />
        </div>
        <!-- Muestra la imagen correspondiente al producto actual -->
        <img :src="imagen" alt="">
        <!-- Botón para cambiar al siguiente producto -->
        <button @click="siguiente" class="boton">Siguiente ({{ contador + 1 }}/ {{ total }} )</button>
    </div>
</template>

<script setup>
import { ref, computed } from "vue"
import { productos } from "@/datos.js"

// Define el contador y el total de productos
const contador = ref(0)
const total = productos.length;

// Función para cambiar al siguiente producto
const siguiente = () => {
    contador.value++
    if (contador.value >= total) {
        contador.value = 0;
    }
}

// Calcula el nombre del rey godo con formato
const rey = computed(() => {
    const elNombre = productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1)
})

// Calcula la URL de la imagen del producto
const ruta = "https://www.html6.es/img/rey_"
const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})

// Calcula el nuevo precio con descuento del producto
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
