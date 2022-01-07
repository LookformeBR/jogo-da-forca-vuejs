<template>
  <div class="teclado">
    <button
      class="teclado-botao"
      v-for="(letra, key) in 'abcdefghijklmnopqrstuvxyz'"
      :key="key"
      :disabled="verificarLetra(letra)"
      v-on:click="jogar(letra)"
    >
      {{ letra }}
    </button>
  </div>
</template>

<script>
export default {
  name: "Teclado",
  props: {
    Letras: Array,
    verificarLetra: Function,
    jogar: Function,
  },
};
</script>

<style>
.teclado {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 80%;
  margin-top: 20px;
}
.teclado-botao {
  margin: 5px;
  text-transform: uppercase;
}
</style>