<template>
    <header>
      <div class="content">
          <img alt="Empresta bem melhor" id="logo" src="https://empresta.com.br/wp-content/uploads/2022/01/logo-empresta.svg">
          <div class="vertical-line"></div>
          <h1>Simulador</h1>
      </div>
    </header>
</template>

<script>
//import { defineComponent } from '@vue/composition-api'

export default {
    name: 'Header'
}
</script>

<style scoped>
    header {
        background-color: #fff;
        box-shadow: 0 0 10px 0 rgb(54 68 75 / 30%);
        height: 100px;
        width: 100%;
        margin: 0 auto
    }

    .content {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .content h1 {
        color: var(--color-secondary);
        padding-top: 5px;
    }

    .vertical-line {
       
        border-left: 1px solid rgb(212, 212, 212);
        height: 80px;
        margin: 10px;
        
    }
</style>