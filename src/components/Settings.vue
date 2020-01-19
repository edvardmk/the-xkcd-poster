<template>
<v-container>
  <v-form>
    <v-select :items="characters" label="Character" v-model="state.character" outlined></v-select>
    <v-text-field label="Name" placeholder="" v-model="state.name" outlined></v-text-field>
      <v-menu
        v-model="datepickerMenu"
        :nudge-right="40"
        transition="scale-transition"
        offset-y
        min-width="290px"
      >
        <template v-slot:activator="{ on }">
          <v-text-field
            v-model="computedDateFormatted"
            label="Birthday"
            v-on="on"
          outlined></v-text-field>
        </template>
        <v-date-picker v-model="date" @input="datepickerMenu = false"></v-date-picker>
      </v-menu>
    <v-slider v-model="state.size" min="25" max ="50" label="Size" :thumb-size="24" thumb-label outlined></v-slider>
  </v-form>
</v-container>
</template>

<script>
export default {
  name: 'Settings',
  model: {
    prop: 'state',
    event: 'changedState'
  },
  props: ['state'],
  data: vm => ({
      date: new Date().toISOString().substr(0, 10),
      dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
      datepickerMenu: false,
    // name: '',
    // size: 35,
    characters: ['Beret Guy', 'Black Hat', 'Cueball', 'Hairy', 'Danish', 'Megan', 'Ponytail'],
    // character: this.data.characters[1],
  }),
    computed: {
      computedDateFormatted () {
        return this.formatDate(this.date)
      },
    },
  watch: {
      date () {
        this.dateFormatted = this.formatDate(this.date)
        this.state.birthday = this.formatDate(this.date)
      },
    },
  methods: {
      formatDate (date) {
        if (!date) return null

        const [year, month, day] = date.split('-')
        return `${day}.${month}.${year}`
      },
      parseDate (date) {
        if (!date) return null

        const [month, day, year] = date.split('.')
        return `${year}-${month.padStart(2, '0')}-${day.padStart(2, '0')}`
      },
  },
  mounted() {

        this.state.birthday = this.formatDate(this.date)
  }
};
</script>

<style>
.v-input__slider {
  margin: 0 12px;
}
</style>
