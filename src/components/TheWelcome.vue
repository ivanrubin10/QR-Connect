<template>
  <div>
    <label for="ssid">SSID:</label>
    <input v-model="ssid" id="ssid" type="text" placeholder="Enter SSID" />

    <label for="securityType">Security Type:</label>
    <select v-model="securityType" id="securityType">
      <option value="WPA">WPA</option>
      <option value="WEP">WEP</option>
      <option value="nopass">Open (no password)</option>
    </select>

    <label for="password">Password:</label>
    <input v-model="password" id="password" type="password" placeholder="Enter Password" />

    <button @click="generateQRCode">Generate QR Code</button>

    <img v-if="qrCodeUrl" :src="qrCodeUrl" alt="QR Code" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Wi-Fi network information
const ssid = ref('YourSSID');
const securityType = ref('WPA');
const password = ref('YourPassword');

// QR code URL
const qrCodeUrl = ref('');

const generateQRCode = () => {
  const wifiPayload = `WIFI:S:${ssid.value};T:${securityType.value};P:${password.value};;`;
  const qrCodeData = encodeURIComponent(wifiPayload);

  // Set the size of the QR code in pixels (adjust as needed)
  const qrCodeSize = '200x200';

  // Construct the API URL
  qrCodeUrl.value = `https://api.qrserver.com/v1/create-qr-code/?data=${qrCodeData}&size=${qrCodeSize}`;
};
</script>

<style scoped>
/* Add your styles here if needed */
</style>
