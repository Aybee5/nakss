<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col>
        <h1 class="display-2 font-weight-bold mb-3">
          NAKSS-BUK
        </h1>

        <p class="subheading font-weight-regular">
          As mandated by the ES Scholarship Board, that each student must posses a union ID Card before being screened for the scholarship.
          This is to ease the collection of retriving the record of student by National Association of Kano State Student Bayero University Kano (NAKSS-BUK)
          <br><b>Please Make sure you submit correct detail</b>
        </p>
      </v-col>

      <v-col
        class=""
        cols="12"
      >
        <v-btn color="success" to="/payment"> Fill Detail </v-btn>
      </v-col>

      <v-col
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Should you need any help, you can contact:
        </h2>
        <ul>
          <li>Nafi'u Zugachi (President): +2348012345678</li>
          <li>Ibrahim Abdullahi (DPS): +2348139349336</li>
          <li>Imran (PRO): +2348139349936</li>
        </ul>
      </v-col>
    </v-row>
  </v-container>
</template>
