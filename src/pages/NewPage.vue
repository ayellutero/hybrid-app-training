<template>
  <q-page padding>
    <!-- content -->
    <div class="row text-white">
      <div class="col">
        <q-input v-model="movieData.name" label="Movie Name"/>
        <q-input v-model="movieData.year" label="Year" type="number"/>
        <q-btn class="bg-white text-black" @click="updateMovie">Update</q-btn>
        <q-btn class="bg-white text-black" @click="cancel">CANCEL</q-btn>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  // name: 'PageName',
  data () {
    return {
      movieData: {},
      movName: '',
      yr: ''
    }
  },
  created () {
    this.$bind('movieData', this.$db.collection('movies').doc((this.$route.params.id)));
  },
  methods: {
    updateMovie () {
      console.log('update')
      this.$db.collection('movies').doc(this.movieData.id)
        .set({
          name: this.movieData.name,
          year: this.movieData.year
        })  
        .then(() => {
          console.log('Movie updated!')
          this.$router.push('/')
        })
    },
    cancel () {
      console.log('cancel')
      this.$router.push('/')
    }
  }
}
</script>
