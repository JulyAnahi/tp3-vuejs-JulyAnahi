<script setup>
import PanelPestanas from './PanelPestanas.vue';

</script>

<template>
  <div id="app-global">
    <header class="app-header">
      <h1>Catalogo de productos</h1>

    </header>
    <main>
      <PanelPestanas></PanelPestanas>
    </main>
  </div>

</template>
<style scoped>
  body{
    margin:0;
    font-family: Arial, Helvetica, sans-serif;
    background-color: #e9ecef;
  }
  .app-header{
    background-color: #343a40;
    color: white;
    text-align: center;
    padding: 15px;
  }
  .app-header h1{
    
    color: white;
  
  }
</style>