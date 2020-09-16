<template>
  <v-container>
      <v-col>
        <h1 class="display-2 font-weight-bold mb-3">Success</h1>

        <p class="subheading font-weight-regular">
          You've successfully submitted your details, do you want to submit another?
        </p>
      </v-col>

      <v-col class cols="12">
        <v-btn color="primary" to="/payment">Submit Another</v-btn>
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