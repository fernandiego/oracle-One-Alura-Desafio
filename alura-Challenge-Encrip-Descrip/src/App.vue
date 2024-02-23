<template>
  <div class="container">
    <div class="input-container">
      <input class="input-text" type="text" v-model="inputText" placeholder="Digite seu texto" id="text">
      <div class="texto-exclamcao">
        <img src="./assets/bi_exclamation-circle-fill.svg">
        Apenas letras minúsculas e sem acento.</div>
      <div class="button-container">
        <button class="button-cript" @click="encrypt">Encrypt</button>
        <button class="button-descript" @click="decrypt">Decrypt</button>
      </div>
    </div>
    <div class="output-container">
      <textarea v-model="outputText" v-if="outputText"></textarea>
      <img class="img" v-if="!outputText" src="./assets/High%20quality%20products%201%201.svg">
      <div class="texto-nenhuma-mensagem">
        Nenhuma mensagem encontrada
      </div>
      <div class="digite-um-texto">Digite um texto que você deseja criptografar ou descriptografar.</div>

    </div>
  </div>
</template>
<style src="./style.css"></style>
<script>
import CryptoJS from 'crypto-js'; // Import CryptoJS library
// import "./style.css"


export default {
  data() {
    return {
      inputText: "",
      outputText: ""
    };
  },
  methods: {
    encrypt() {
      this.outputText = CryptoJS.AES.encrypt(this.inputText, "secret_key").toString();
    },
    decrypt() {
      try {
        this.outputText = CryptoJS.AES.decrypt(this.inputText, "secret_key").toString(CryptoJS.enc.Utf8);
      } catch (error) {
        console.error("Decryption error:", error);
        this.outputText = "Error: Unable to decrypt. Make sure the input is a valid encrypted text.";
      }
    }
  }
};
</script>
