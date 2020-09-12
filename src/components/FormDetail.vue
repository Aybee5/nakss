<template>
  <v-container class="ml-4">
    <v-layout row>
      <v-flex xs12 sm6 offset-sm1>
        <h4>Student's ID Card detail</h4>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <form
          @submit.prevent="handleSubmit"
          name="student-detail"
          method="post"
          data-netlify="true"
          data-netlify-honeypot="bot-field"
        >
          <input type="hidden" name="form-name" value="student-detail" />
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" lg="12" sm="12">
                <v-text-field v-model="student.name" name="name" label="Full Name" required></v-text-field>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" lg="12" sm="12">
                <v-text-field
                  type="tel"
                  name="phone"
                  v-model="student.number"
                  label="Phone Number"
                  pattern="[0-9]{11}"
                  placeholder="08012345678"
                  required
                ></v-text-field>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" lg="12" sm="12">
                <v-text-field
                  v-model="student.regNum"
                  name="regNum"
                  label="Registration Number"
                  required
                  placeholder="CST/00/COM/12345"
                  pattern="[A-Za-z]{3}\/[0-9]{2}\/[A-Za-z]{3}\/[0-9]{5}"
                ></v-text-field>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" lg="12" sm="12">
                <v-text-field
                  v-model="student.faculty"
                  name="faculty"
                  label="Faculty Name"
                  required
                ></v-text-field>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" lg="12" sm="12">
                <v-text-field v-model="student.dept" name="dept" label="Department" required></v-text-field>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" sm="12" lg="6">
                <v-select
                  :items="['100','200','300', '400', '500']"
                  required
                  name="level"
                  label="Level"
                  class="ml-1 py-0"
                  v-model="student.level"
                ></v-select>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm1>
              <v-col cols="11" sm="12" lg="6">
                <v-file-input
                  v-model="student.img"
                  accept="image/*"
                  name="passport"
                  placeholder="Upload your ID size photo"
                  label="Passport"
                  prepend-icon="mdi-paperclip"
                >
                  <template v-slot:selection="{ text }">
                    <v-chip small label color="primary">{{ text }}</v-chip>
                  </template>
                </v-file-input>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 md6 offset-sm1>
              <v-col>
                <v-btn color="primary" @click="makePayment">Make Payment(N300)</v-btn>
              </v-col>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 md6 offset-sm1>
              <v-col>
                <v-btn color="success" type="submit">Submit</v-btn>
                <pre>
                  {{student}}
                </pre>
              </v-col>
            </v-flex>
          </v-layout>
        </form>
      </v-flex>
    </v-layout>
  </v-container>
</template>
          <script src="https://checkout.flutterwave.com/v3.js"></script>

<script>
export default {
  data() {
    return {
      student: {
        name: null,
        number: null,
        dept: null,
        faculty: null,
        regNum: null,
        level: null,
        img: [],
      },
    };
  },
  methods: {
    seeFile() {
      console.log(this.student.img);
    },
    makePayment() {
      FlutterwaveCheckout({
        public_key: "FLWPUBK_TEST-31d61a13026483fc38f15f0e90232374-X",
        tx_ref: "hooli-tx-1920bbtyt",
        amount: 54600,
        currency: "NGN",
        payment_options: "card,mobilemoney,ussd",
        customer: {
          email: "user@gmail.com",
          phonenumber: "08102909304",
          name: "yemi desola",
        },
        callback: function (data) {
          // specified callback function
          console.log(data);
        },
        customizations: {
          title: "My store",
          description: "Payment for items in cart",
          logo: "https://assets.piedpiper.com/logo.png",
        },
      })
    },
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit(e) {
      console.log(e);
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": "student-detail",
          ...this.student,
        }),
      })
        .then((a) => {
          // this.$router.push("thanks");
          console.log("success", a);
        })
        .catch((err) => {
          // this.$router.push("404");
          console.log("fail", err);
        });
    },
  },
};
</script>

<style>
</style>