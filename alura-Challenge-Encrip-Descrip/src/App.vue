<template>
  <div class="container">
    <div class="input-container">
      <input class="digite-seu-texto" type="text" v-model="inputText" placeholder="Digite seu texto" id="text">
      <div class="button-container">
        <button @click="encrypt">Encrypt</button>
        <button @click="decrypt">Decrypt</button>
      </div>
    </div>
    <div class="output-container">
      <textarea  v-model="outputText" readonly></textarea>
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
