<script setup>
import {ref} from 'vue'

  const expandida = ref(false)

  const toggleExpandir = () =>{
    expandida.value = !expandida.value
  }

</script>

<template>
  <div class="tarjeta-producto">
    <header class="tarjeta-header">
        <slot name="header"></slot>
    </header>
    <main class="tarjeta-body">
        <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir"></slot>
    </main>
    <footer class="tarjeta-footer">
        <slot name="footer">
            <span class="fallback-text">Nada que mostrar</span>
        </slot>
    </footer>
  </div>
</template>
<style scoped>
    .tarjeta-producto {
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 15px;
        margin-bottom: 15px;
        background-color:#fff;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .tarjeta-header{
        border-bottom: 1px solid #eee;
        padding-bottom: 8px;
        margin-bottom: 10px;
    }
    .tarjeta-body{
        margin-bottom: 10px;
    }

    .tarjeta-footer{
        border-top: 1px solid #eee;
        padding-top: 8px;
        margin-top: 10px;
    }
    .fallback-text{
        color: #888;
        font-style: italic;
    }

</style>