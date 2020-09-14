<template>
  <v-container>
      <v-col>
        <h1 class="display-2 font-weight-bold mb-3">Payment</h1>

        <p class="subheading font-weight-regular">
          Before you can submit the detail, you'll have to make payment of 300 for the ID Card
          <br />
          <b>Click on the blue button to make payment</b>
        </p>
      </v-col>

      <v-col class cols="12">
        <v-btn color="primary" @click="makePayment">Make Payment</v-btn>
      </v-col>

      <v-col cols="12">
        <h2 class="headline font-weight-bold mb-3">If you have any question, contact:</h2>
        <ul>
          <li>Nafi'u Zugachi (President): +2348012345678</li>
          <li>Ibrahim Abdullahi (DPS): +2348139349336</li>
          <li>Imran (PRO): +2348139349936</li>
        </ul>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  methods: {
    makePayment() {
      FlutterwaveCheckout({
        public_key: "FLWPUBK_TEST-31d61a13026483fc38f15f0e90232374-X",
        tx_ref: `KN ${Date.now().toString(36)}`,
        amount: 300,
        currency: "NGN",
        payment_options: "card, account, ussd, banktransfer",
        redirect_url: "http://localhost:8080/form",
        customer: {
          email: "user@gmail.com",
          phonenumber: "08102909304",
          name: "yemi desola",
        },
        customizations: {
          title: "NAKSS-BUK",
          description: "Payment for ID Card",
          logo: "https://assets.piedpiper.com/logo.png",
        },
      });
    },
  },
};
</script>