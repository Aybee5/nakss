<template>
  <v-app>
    <NavBar/>
    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
import FormDetail from './components/FormDetail';
import NavBar from './components/NavBar'

export default {
  name: 'App',

  components: {
    FormDetail,
    NavBar
  },

  data: () => ({
    //
  }),
};
</script>
