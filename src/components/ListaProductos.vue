<script setup>
import {ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef } from 'vue'
import TarjetaProducto from './TarjetaProducto.vue';

const props = defineProps({
    productos: {
        type:Array,
        required:true
    }
})

const cargando = ref(true)

let timer = null

const box = useTemplateRef('box')

function esperar(ms){
    return new Promise(resolve=> setTimeout(resolve, ms))
}

async function cargarProductos(){
    cargando.value = true
    await esperar(800)
    cargando.value = false
}
//HOOK1 cuando monta el componente
onMounted(()=>{
    cargarProductos()
    timer = setInterval(()=>{

        console.log('ListaProductos - Actualizando productos por Polling...')
        cargarProductos()
    }, 30000)
})

//HOOK2 Al actualizarse el HTML del componente
onUpdated(()=>{
    if (box.value) {
        box.value.scrollTop = box.value.scrollHeight
    }
})
 
//HOOK3 antes de destruir el componente

onBeforeUnmount(()=>{
    clearInterval(timer)
    console.log('ListaProductos desmontado - polling detenido')
})

const alertaCompra = (producto) => {
    alert(`Agregando ${producto.nombre} al carrito`)
}
</script>
<template>
<div class="">
    <div v-if="cargando" class="cargando">
        <p>Cargando productos...</p>
    </div>

    <div v-else ref="box" class="lista-contenedor">
        <TarjetaProducto v-for="prod in props.productos" :key="prod.id">
            <template #header>
                <h3>{{ prod.nombre }}</h3>
                <span class="categoria">{{ prod.categoria }}</span>
            </template>
            
            <template #body="{ expandida, toggleExpandir}">
                <p>Precio: <strong>${{ prod.precio }}</strong></p>
            <button @click="toggleExpandir">
                {{ expandida ? 'Ocultar detalles': 'Ver mas detalles'}}
            </button>
            
            <div v-if="expandida" class="detalle-extra">
                <p>Stock disponible: {{ prod.stock }} unidades</p>
            </div>
        </template>
        <template #footer v-if="prod.id <= 5">
            <button class="btn-comprar" @click="alertaCompra(prod)">Comprar</button>
            
            
        </template>
    </TarjetaProducto>
</div>
</div>
</template>

<style scoped>
.lista-contenedor{
    max-height: 400px;
    overflow-y:auto;
    border:2px dashed #aaa;
    padding: 10px;
    background-color: #fafafa;
}
.cargando {
    text-align: center;
    font-weight: bold;
    padding:20px;
}
.categoria{
   background-color: #e0e0e0;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 0.8em;
}
.detalle-extra {
  margin-top: 10px;
  padding: 5px;
  background-color: #fff9c4;
 
}
.btn-comprar {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}
</style>