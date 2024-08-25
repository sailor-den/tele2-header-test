<template>
  <Header />
</template>

<script setup>
  import Header from './components/Header.vue';
</script>

<style>
  @font-face {
    font-family: 'Tele2TextSansWebSHORT';
    src: url('../src/assets/fonts/tele2textsanswebshort-regular.eot'); 
    src: url('../src/assets/fonts/tele2textsanswebshort-regular.eot?#iefix') format('embedded-opentype'), 
      url('../src/assets/fonts/tele2textsanswebshort-regular.woff2') format('woff2'), 
      url('../src/assets/fonts/tele2textsanswebshort-regular.woff') format('woff'), 
      url('../src/assets/fonts/tele2textsanswebshort-regular.ttf') format('truetype'), 
      url('../src/assets/fonts/tele2textsanswebshort-regular.svg#tele2textsanswebshort-regular') format('svg'); 
      font-weight: normal;
      font-style: normal;
  }

  @font-face {
    font-family: 'Tele2TextSansWebSHORT';
    src: url('../src/assets/fonts/tele2textsanswebshort-bold.eot'); 
    src: url('../src/assets/fonts/tele2textsanswebshort-bold.eot?#iefix') format('embedded-opentype'), 
      url('../src/assets/fonts/tele2textsanswebshort-bold.woff2') format('woff2'), 
      url('../src/assets/fonts/tele2textsanswebshort-bold.woff') format('woff'), 
      url('../src/assets/fonts/tele2textsanswebshort-bold.ttf') format('truetype'), 
      url('../src/assets/fonts/tele2textsanswebshort-bold.svg#tele2textsanswebshort-bold') format('svg'); 
      font-weight: bold;
      font-style: normal;
  }

  body {
    margin: 0;
    font-family: 'Tele2TextSansWebSHORT';
  }
</style>
