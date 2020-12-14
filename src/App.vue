<template>
  <v-app>
    <v-content>
      <v-main>
        <Header />
        <router-view/>
      </v-main>
    </v-content>
  </v-app>
</template>


<script>
import Header from './components/layault/Header';

export default {
  name: 'App',

  components: {
    Header,
  },

  data: () => ({
    //
  }),
};
</script>