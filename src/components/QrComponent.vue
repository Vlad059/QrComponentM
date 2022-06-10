<template>
  <qrcode-vue :value="qr_value" :size="size" level="H" />
</template>
<script>
  import QrcodeVue from 'qrcode.vue'

  export default {
    props: ['qr_value'],
    data() {
      return {
        size: 300
      }
    },
    components: {
      QrcodeVue,
    },
  }
</script>