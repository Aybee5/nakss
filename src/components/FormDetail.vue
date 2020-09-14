<template>
  <v-container class="ml-4">
    <v-layout row>
      <v-flex xs12 sm6 offset-sm1>
        <h4>Student's ID Card detail</h4>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <!-- <form
          @submit.prevent="handleSubmit"
          name="student-detail"
          method="post"
          enctype="multipart/form-data"
          data-netlify="true"
          data-netlify-honeypot="bot-field"
        > -->
        <!-- <form @submit.prevent="submitForm" enctype="multipart/form-data" action="https://api.staticforms.xyz/submit" method="post"> -->
          <!-- <input type="hidden" name="form-name" value="student-detail" /> -->
          <!-- <input type="hidden" name="accessKey" value="230f7536-36df-4a36-81ad-c30cefc0b7eb">
          <input type="hidden" name="subject" value="New Detail"> -->
        <!-- Replace with the url you want to redirect to -->
          <!-- <input type="hidden" name="redirectTo" value="/about"> -->
          <form @submit.prevent="submitThis" id="formDetail" enctype="multipart/form-data" method="post">
          <input type="hidden" name="ref" :value="this.$route.query.tx_ref">
          <input type="hidden" name="trans_id" :value="this.$route.query.transaction_id">
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
                  @change="seeFile"
                  placeholder="Upload your ID size photo"
                  label="Passport"
                  prepend-icon="mdi-camera"
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
                <v-btn color="success" type="submit" :disabled="checkPayment">Submit</v-btn>
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
    seeFile(file) {
      console.log(this.checkPayment);
      console.log(file);
    },
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    submitThis() {
      fetch('https://fast-temple-47704.herokuapp.com/submit',{
        body: new FormData(document.getElementById('formDetail')),
        method: "post"
      }).then(res=> {
        console.log(res)
      }).catch(err=>{
        console.log(err);
      })
    },
    handleSubmit(e) {
      console.log(e);
      fetch("/", {
        method: "POST",
        // headers: { "Content-Type": "application/x-www-form-urlencoded" },
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
  computed: {
    checkPayment() {
      return this.$route.query.status === 'completed' ? false : true
    }
  }
};
</script>

<style>
</style>