<template>
  <div class="qr_generator">
    <img alt="Vue logo" src="./assets/logo.png">
    <label for="qr_input"><strong>Генерация QR кода по строке</strong></label>
    <input id="qr_input" v-model="app_qr_value">
    <QrComponent :qr_value="app_qr_value"/>    
  </div>
  <QrReader/>
</template>

<script>
import QrComponent from './components/QrComponent.vue'
import QrReader from './components/QrReader.vue'

export default {
  name: 'App',
  data(){
    return {
      app_qr_value: 'https://example.com'
    }
  },
  components: {
    QrComponent,
    QrReader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex; 
  flex-direction: row;
  justify-content: center;
}
.qr_generator {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
