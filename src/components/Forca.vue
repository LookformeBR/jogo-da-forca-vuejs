<template>
  <div class="forca">
    <img
      :src="`https://raw.githubusercontent.com/william-costa/wdev-hangman-game-resources/master/images/hangman/${erros}.svg`"
    />
  </div>
</template>

<script>
export default {
  name: "Forca",
  props: {
    erros: Number,
  },
};
</script>

<style>
.forca img {
  height: 100px;
}
</style>