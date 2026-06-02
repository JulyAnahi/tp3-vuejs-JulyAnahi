<script setup>
import {ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef, onUnmounted, onActivated, onDeactivated } from 'vue';
import {productos} from '../../data/productos';
import ListaProductos from '../ListaProductos.vue';
 
onMounted(()=>console.log('TabTodos - montado'))
onUnmounted(()=>console.log('TabTodos - desmontado'))
onActivated(()=> console.log('TabTodos - activado'))
onDeactivated(() =>console.log('TabTodos - desactivado'))

</script>

<template>
    <div class="">
        <h2>Todos los productos</h2>
        <ListaProductos :productos = "productos"></ListaProductos>
    </div>
</template>