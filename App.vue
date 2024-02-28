<template>
  <div class="container">
    <div class="logo-alura">
      <img src="assets/Frame%206.svg">
    </div>
    <div class="input-container">
      <input class="input-text" type="text" v-model="inputText" placeholder="Digite seu texto" id="text">
      <div class="texto-exclamcao">
        <img src="assets/bi_exclamation-circle-fill.svg">
        Apenas letras minúsculas e sem acento.
      </div>
      <div class="button-container">
        <button class="button-cript" @click="encrypt">Criptografar</button>
        <button class="button-descript" @click="decrypt">Descriptografar</button>
      </div>
    </div>
    <div class="output-container">
      <textarea v-model="outputText" v-if="started"></textarea>
      <img class="img" v-if="!started" src="assets/High%20quality%20products%201%201.svg">
      <div class="texto-nenhuma-mensagem" v-if="!started">
        Nenhuma mensagem encontrada
      </div>
      <div class="digite-um-texto" v-if="!started">
        Digite um texto que você deseja criptografar ou descriptografar.
      </div>
      <div class="button-copy-container" v-if="started">
        <button class="button-copy" @click="copyOutputText">Copiar</button>
      </div>

    </div>
  </div>
</template>
<style src="style.css"></style>
<script>
import CryptoJS from 'crypto-js'; // Import CryptoJS library
// import "./style.css"


export default {
  data() {
    return {
      inputText: "",
      outputText: "",
      started: false
    };
  },
  methods: {
    encrypt() {
      this.outputText = CryptoJS.AES.encrypt(this.inputText, "secret_key").toString();
      this.started = true
    },
    decrypt() {
      try {
        this.outputText = CryptoJS.AES.decrypt(this.inputText, "secret_key").toString(CryptoJS.enc.Utf8);
      } catch (error) {
        console.error("Decryption error:", error);
        this.outputText = "Error: Unable to decrypt. Make sure the input is a valid encrypted text.";
        this.started = true
      }
    },
    copyOutputText() {
      const textarea = document.createElement('textarea');
      textarea.value = this.outputText;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
    }
  }
};
</script>
