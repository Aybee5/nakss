<template>
  <v-container class="ml-4">
    <v-layout row>
      <v-flex xs12 sm6 offset-sm1>
        <h3>Make sure you submit this form before closing your browser</h3>
        <p>
          If you have any issue regarding send a mail to
          <a
            href="mailto:ibrahiimaa05@gmail.com"
          >ibrahiimaa05@gmail.com</a>
          or call
          <a href="tel:+2348139349336">08139349336</a>with reference number:
          <b>{{this.$route.query.tx_ref}}</b> and a transaction_id:
          <b>{{this.$route.query.transaction_id}}</b>
        </p>
        <h4>Student's ID Card detail</h4>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <form
          @submit.prevent="submitThis"
          id="formDetail"
          enctype="multipart/form-data"
          method="post"
        >
          <input type="hidden" name="ref" :value="this.$route.query.tx_ref" />
          <input type="hidden" name="trans_id" :value="this.$route.query.transaction_id" />
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
    <v-overlay :value="loading">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
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
      loading: false,
    };
  },
  methods: {
    submitThis() {
      console.log("submitting");
      this.loading = true;
      if (!this.$route.query.tx_ref && !this.$route.query.transaction_id) {
        this.$router.replace("/payment");
      } else {
        // https://fast-temple-47704.herokuapp.com
        fetch("https://fast-temple-47704.herokuapp.com/submit", {
          body: new FormData(document.getElementById("formDetail")),
          method: "post",
        })
          .then((res) => {
            return res.json();
          })
          .then((data) => {
            if (data.msg) {
              console.log("submit success");
              this.$router.replace("/success");
            }
            else {
              console.log("else fired", data)
              // this.$router.replace("/error");
            }
          })
          .catch(err=>{
            console.log("cache fired", err)
            // this.$router.replace("/error");
          })
      }
    },
  },
  computed: {
    checkPayment() {
      return this.$route.query.status === "completed" ? false : true;
    },
  },
  mounted() {
    localStorage.setItem("refKey", this.$route.query.tx_ref);
    localStorage.setItem("transId", this.$route.query.transaction_id);
  },
};
</script>

<style>
</style>