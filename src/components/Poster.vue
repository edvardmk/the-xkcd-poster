<template>
<v-card :height="height" tile>
  <v-container id="poster" fill-height>
    <v-img :src="this.imgPath" :height="imgHeight" contain></v-img>
    <v-container>
    <div id="name">
      <h2>{{ state.name }}</h2>
    </div>
    <div id="birthday">
      <h2>* {{ state.birthday }}</h2>
    </div>
    </v-container>
  </v-container>
</v-card>
</template>

<script>
export default {
  name: 'Poster',
  props: ['state'],
  data: () => ({
    height: 0,
  }),
  computed: {
    imgPath() {
      return '../characters/' + this.state.character.toLowerCase().split(' ').join('-') + '.png';
    },
    imgHeight() {
      return this.height * this.state.size / 70;
    }
  },
  methods: {
    calculateHeight() {
      this.height = this.$el.clientWidth / 5 * 7;
    },
  },
  mounted() {
    this.$nextTick(this.calculateHeight);
    window.addEventListener('resize', this.calculateHeight);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.calculateHeight)
  },
};
</script>

<style>
#poster {
  align-content: center;
}
#name, #birthday {
  flex-basis: 100%;
  text-align: center;
}
</style>
