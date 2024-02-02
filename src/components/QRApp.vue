<template>
  <div class="qr-app-container">
    <div class="form-container">
      <div class="form-ssid">
        <label for="ssid">SSID:</label>
        <input v-model="ssid" id="ssid" type="text" placeholder="Enter SSID" />
      </div>
      <div class="form-security">
        <label for="securityType">Security Type:</label>
        <select v-model="securityType" id="securityType">.
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
const ssid = ref("");
const securityType = ref("");
const password = ref("");

// QR code URL
const qrCodeUrl = ref("");

const generateQRCode = () => {
  if(!ssid.value || !securityType.value || !password.value){
    alert('Please fill out all fields');
    return;
  }
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
  top: 5em;
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

button {
  background-image: linear-gradient(to right, #302b63, #24243e);
  border-radius: 10px;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}

select {
  border: 1px solid black;
  border-radius: 0.25em;
  padding: 0.25em 0.5em;
  font-size: 1.25rem;
  cursor: pointer;
  line-height: 1.1;
  background-color: #fff;
  background-image: linear-gradient(to top, #f9f9f9, #fff 33%);
}

input {
  border: 1px solid black;
  border-radius: 0.25em;
  padding: 0.25em 0.5em;
  font-size: 1.25rem;
  cursor: pointer;
  line-height: 1.1;
  background-color: #fff;
  background-image: linear-gradient(to top, #f9f9f9, #fff 33%);
}
 
/* For Mobile Portrait View */
@media screen and (max-device-width: 500px) 
    and (orientation: portrait) {
    .qr-app-container {
        width: auto;
        border: none;
        border-radius: 0px;
        background-color: transparent;
    }
}

</style>
