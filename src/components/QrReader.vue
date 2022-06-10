<template>
    <div class="qr_reader">
        <label><strong>Декодированная строка с QR кода:</strong></label>
        <p>{{ decoded_string }}</p>
        <label><strong>Состояние камеры:</strong></label>
        <p>{{ error }}</p>       
        <label><strong>Камера:</strong></label>
        <div class="div_qr"><qrcode-stream @init="onInit_camera" @decode="onDecode"></qrcode-stream></div>
        <label><strong>Зона для перетаскивания QR кода:</strong></label>
        <div class="div_qr div_qr_drop"><qrcode-drop-zone @decode="onDecode">Можно перетащить QR код сюда</qrcode-drop-zone></div>
    </div>
</template>

<script>
import { QrcodeStream, QrcodeDropZone} from 'vue3-qrcode-reader'

export default {
    data (){
        return {
            error: '',
            cap: null,
            decoded_string: ''
        }
    },
    methods: {
        async onInit_camera (promise){
            // show loading indicator
            try {
                const { capabilities } = await promise;
                this.cap = capabilities;
                this.error = 'Find device';
            } catch (error) {
                if (error.name === 'NotAllowedError') {
                    this.error = 'user denied camera access permisson';
                } else if (error.name === 'NotFoundError') {
                    this.error = 'no suitable camera device installed';
                } else if (error.name === 'NotSupportedError') {
                    this.error = 'page is not served over HTTPS (or localhost)';
                } else if (error.name === 'NotReadableError') {
                    this.error = 'maybe camera is already in use';
                } else if (error.name === 'OverconstrainedError') {
                    this.error = 'did you requested the front camera although there is none?';
                } else if (error.name === 'StreamApiNotSupportedError') {
                    this.error = 'browser seems to be lacking features';
                }
            } finally {
                // hide loading indicator
            }
        },
        onDecode(decoded_string){
            this.decoded_string = decoded_string;
        }
    },
    components: {
        QrcodeStream,
        QrcodeDropZone
    }
}
</script>

<style>
.qr_reader{
    flex-direction: column;
}
.div_qr{
    margin: 1%;   
}
.div_qr_drop {
    height: 30px;
    border: 1px solid black;
}
</style>
