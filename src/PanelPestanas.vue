<script setup>
import { shallowRef } from 'vue';
import TabTodos from './components/tabs/TabTodos.vue';
import TabElectronica from './components/tabs/TabElectronica.vue';
import TabPerifericos from './components/tabs/TabPerifericos.vue';

const tabActivo = shallowRef(TabTodos)


const cambiartab = (componente) => {
    tabActivo.value = componente
}
</script>

<template>
    <div class="panel-pestanas">
        <div class="controles">
            <button @click="cambiartab(TabTodos)">Ver Todos</button>
            <button @click="cambiartab(TabElectronica)">Electronica</button>
            <button @click="cambiartab(TabPerifericos)">Periféricos</button>
        </div>

        <div class="comparativa-contenedor">
            <div class="columna"></div>
            <!-- <p class="nota"> Cada cambio monta/desmonta el componente entero </p> -->
            <div class="caja-render">

                <component :is="tabActivo"></component>
            </div>
        </div>

        <div class="columna">
            <!-- <h3>Desde KeepAlive</h3> -->
            <!-- <p class="nota"> Mantiene el estado y congela/descongela el componente </p> -->
           <div class="caja-render">
                <keep-alive>
                    <component :is="tabActivo"></component>
                </keep-alive>
            </div>
        </div>
    </div>

</template>

<style scoped>
.panel-pestanas {
    padding: 20px;
}
.controles{
    display:flex;
    gap:10px;
    justify-content: center;
    margin-bottom: 20px;
}
.controles button{
    padding: 10px 20px;
    font-size: 1em;
    cursor:pointer;
    background-color: #007bff;
    color: white;
    border:none;
    border-radius:4px;
}
.controles button:hover {
    background-color: #0056b3;
}
.columna {
    flex:1;
    background-color: #f1f1f1;
    padding: 15px;
    border-radius: 8px;
}
.nota {
    font-size: 0.85em;
    color:#666;
}
.caja-render{
    background-color: white;
    padding: 10px;
    border-radius: 4px;
    margin-top: 10px;
}
</style>
