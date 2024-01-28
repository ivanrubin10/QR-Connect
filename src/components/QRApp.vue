<template>
  <div class="qr-app-container">
    <div class="form-container">
      <div class="form-ssid">
        <label for="ssid">SSID:</label>
        <input v-model="ssid" id="ssid" type="text" placeholder="Enter SSID" />
      </div>
      <div class="form-security">
        <label for="securityType">Security Type:</label>
        <select v-model="securityType" id="securityType">
          <option value="WPA">WPA</option>
          <option value="WEP">WEP</option>
          <option value="nopass">Open (no password)</option>
        </select>
      </div>
      <div class="form-pass">
        <label for="password">Password:</label>
        <input v-model="password" id="password" type="password" placeholder="Enter Password" />
      </div>

      <button @click="generateQRCode">Generate QR Code</button>
    </div>
    <div class="qr-result">
      <img v-if="qrCodeUrl" :src="qrCodeUrl" alt="QR Code" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
// Wi-Fi network information
const ssid = ref("YourSSID");
const securityType = ref("WPA");
const password = ref("YourPassword");

// QR code URL
const qrCodeUrl = ref("");

const generateQRCode = () => {
  const wifiPayload = `WIFI:S:${ssid.value};T:${securityType.value};P:${password.value};;`;
  const qrCodeData = encodeURIComponent(wifiPayload);

  // Set the size of the QR code in pixels (adjust as needed)
  const qrCodeSize = "200x200";

  // Construct the API URL
  qrCodeUrl.value = `https://api.qrserver.com/v1/create-qr-code/?data=${qrCodeData}&size=${qrCodeSize}`;
};
</script>

<style scoped>
.qr-app-container {
  margin: auto;
  width: 500px;
  height: auto;
  top: 10em;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid white;
  border-radius: 30px;
  background-color: #121212;
}

.qr-result {
  margin: 20px;
}

.form-container {
  display: flex;
  flex-direction: column;
  color: white;
}

.form-container div {
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  justify-content: start;
}

.form-container button {
  margin-top: 50px;
}
</style>
