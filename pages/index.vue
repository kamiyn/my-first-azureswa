<template>
  <div>
    <h1>Sample</h1>
    <v-btn @click="clickLogin">LOGIN</v-btn>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import * as msal from '@azure/msal-browser'

const msalConfig = {
  auth: {
    clientId: 'f8f8156f-eaca-4d76-8591-b7a99fefd769',
    authority:
      'https://kamiynb2cpoc.b2clogin.com/kamiynb2cpoc.onmicrosoft.com/B2C_1_Susi',
    knownAuthorities: ['kamiynb2cpoc.b2clogin.com'],
    redirectUri: location.origin
  }
}

const loginRequest = {
  scopes: ['openid', 'offline_access']
}

const msalInstance = new msal.PublicClientApplication(msalConfig)

async function loginAsync() {
  try {
    const loginResponse = await msalInstance.loginPopup(loginRequest)
    console.log(loginResponse)
  } catch (err) {
    console.error(err)
  }
}

export default Vue.extend({
  methods: {
    async clickLogin() {
      await loginAsync();
    }
  }
})
</script>
