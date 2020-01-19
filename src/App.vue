<template>
  <v-app>
    <v-content>
    <v-row no-gutters justify="center">
      <v-col cols="12" sm="6" md="5" lg="4" id="left">
        <v-container>
          <h1>The XKCD Poster</h1>
          <br>
          <Settings v-model="state"/>
        </v-container>
      </v-col>
      <v-col cols="12" sm="6" md="5" lg="4"  id="right">
        <v-container>
          <Poster :state="state"/>
        </v-container>
      </v-col>
    </v-row>
    </v-content>
  </v-app>
</template>

<script>
import Settings from './components/Settings';
import Poster from './components/Poster';

export default {
  name: 'App',

  components: {
    Settings,
    Poster,
  },

  data: () => ({
    state: {
      character: 'Black Hat',
      name: 'James',
      size: 35,
      birthday: '01.01.2020',
    }
  }),
};
</script>

<style scoped>
</style>
