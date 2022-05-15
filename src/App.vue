<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div id="app">
      <Header />
      <Home />
    </div>
</template>

<script>
import Vue from 'vue'
import './style/style.css'
import Header from './components/Header';
import Home from './components/Home';

export default {
  name: 'App',
  components: {
    Header,
    Home
  }
}
</script>
