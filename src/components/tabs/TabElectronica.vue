<script setup>
import {ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef,onUnmounted, onActivated,onDeactivated, computed} from 'vue'
import { productos } from '../../data/productos'
import ListaProductos from '../ListaProductos.vue';

onMounted(()=>console.log('TabElectronica - montado'))
onUnmounted(()=>console.log('TabElectronica - desmontado'))
onActivated(()=> console.log('TabElectronica - activado'))
onDeactivated(() =>console.log('TabElectronica - desactivado'))

//filtro productos de electronica

const productosFiltrados = computed(()=>{
    return productos.filter(p => p.categoria === 'Electrónica')
})

</script>
<template>
    <div class="">

        <h2>Categoria: Electrónica</h2>
        <ListaProductos :productos = "productosFiltrados"></ListaProductos>
    </div>

</template>