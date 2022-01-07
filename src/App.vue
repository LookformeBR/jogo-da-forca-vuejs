<template>
  <div id="app">
    <h1>Jogo da Forca</h1>

    <section v-if="tela === 'inicio'" id="inicio">
      <Formulario
        v-if="etapa === 'palavra'"
        title="Defina a Palavra"
        button="Próximo"
        :action="setPalavra"
      />

      <Formulario
        v-if="etapa === 'dica'"
        title="Defina a Dica"
        button="Iniciar o Jogo"
        :action="setDica"
      />
    </section>

    <section v-if="tela === 'jogo'" id="jogo">
      <Jogo
        :erros="erros"
        :palavra="palavra"
        :dica="dica"
        :verificarLetra="verificarLetra"
        :etapa="etapa"
        :letras="letras"
        :jogar="jogar"
        :jogarNovamente="jogarNovamente"
      />
    </section>
  </div>
</template>

<script>
import "./css/global.css";

import Formulario from "./components/Formulario";
import Jogo from "./components/Jogo";

export default {
  name: "App",
  data() {
    return {
      tela: "inicio",
      etapa: "palavra",
      palavra: "palavra",
      dica: "dica",
      erros: 0,
      letras: [],
    };
  },
  components: { Formulario, Jogo },
  methods: {
    setPalavra: function (palavra) {
      this.palavra = palavra;
      this.etapa = "dica";
    },
    setDica: function (dica) {
      this.dica = dica;
      this.etapa = "jogo";
      this.tela = "jogo";
    },
    verificarLetra: function (letra) {
      return this.letras.find(
        (item) => item.toLowerCase() === letra.toLowerCase()
      );
    },
    jogar: function (letra) {
      this.letras.push(letra);

      //validar erro
      this.verificarError(letra);
    },

    verificarError: function (letra) {
      //acerto
      if (this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificarAcertos();
      }

      //Erros
      this.erros++;

      //ENforcado
      if (this.erros === 6) {
        this.etapa = "enforcado";
      }
    },
    verificarAcertos: function () {
      let letrasUnicas = [...new Set(this.palavra.split(""))];
      if (letrasUnicas.length === this.letras.length - this.erros) {
        this.etapa = "ganhador";
      }
    },
    jogarNovamente: function(){
      this.palavra = '';
      this.dica = '';
      this.erros = 0;
      this.letras = [];
      this.tela = 'inicio';
      this.etapa = 'palavra';
    }
  },
};
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
