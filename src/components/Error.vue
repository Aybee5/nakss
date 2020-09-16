<template>
  <v-container>
      <v-col>
        <h1 class="display-2 font-weight-bold mb-3" style="color:red;">Error</h1>

        <p class="subheading font-weight-regular">
          Something went wrong
        </p>
        <br>Send a message to 08139349336 with the following details refKey: <b>{{refKey}}</b>
        and transaction id: <b>{{transId}}</b>
      </v-col>

      <v-col cols="12">
        <h2 class="headline font-weight-bold mb-3">If you have any question, contact:</h2>
        <ul>
          <li>Nafi'u Zugachi (President): +2348012345678</li>
          <li>Ibrahim Abdullahi (DPS): +2348139349336</li>
          <li>Imran (PRO): +2348139349936</li>
        </ul>
      </v-col>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      transId: localStorage.getItem('transId'),
      refKey:localStorage.getItem('refKey')
    }
  }
}
</script>