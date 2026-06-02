<script setup>

import {ref, onMounted, onUpdated, onUnmounted, onBeforeUnmount, useTemplateRef ,onActivated, onDeactivated, computed} from 'vue'
import { productos } from '../../data/productos'
import ListaProductos from '../ListaProductos.vue';

onMounted(()=>console.log('TabElectronica - montado'))
onUnmounted(()=>console.log('TabElectronica - desmontado'))
onActivated(()=> console.log('TabElectronica - activado'))
onDeactivated(() =>console.log('TabElectronica - desactivado'))

// filtro productos categ. perifericos

const productosfiltrados = computed(() =>{
    return productos.filter(p => p.categoria === 'Periféricos')
})

</script>

<template>
   <div class="">
    <h2>Categoria: Periféricos</h2>
    <ListaProductos :productos = "productosfiltrados"></ListaProductos>
   </div> 
</template>