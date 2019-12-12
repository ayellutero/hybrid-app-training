<template>
  <q-page class="flex flex-center bg-grey-9">
    <!-- <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
    <h3>{{ parseInt(num2) + parseInt(num1) }}</h3>
    <q-input standout="bg-teal text-white" type="number" v-model="num1" label="Custom standout" :dense="dense" />
    <q-input standout="bg-teal text-white" type="number" v-model="num2" label="Custom standout" :dense="dense" /> -->
    <div class="row text-white">
      <div class="col">
        <q-input v-model="movName" label="Movie Name"/>
        <q-input v-model="yr" label="Year" type="number"/>
        <q-btn color='green' class="bg-white text-black" @click="addMovie()">ADD</q-btn>
        <!-- <q-btn v-if="!isEdit" class="bg-white text-black" @click="addMovie">Add</q-btn>
        <q-btn v-if="isEdit" class="bg-white text-black" @click="updateMovie">Edit</q-btn> -->
      </div>
      <div class="col">
        <li v-for="(movie, index) in movieList" :key="index">
          {{ index + 1 }} : {{ movie.name }} ({{ movie.year }}) <q-btn icon="edit" flat color="green" @click="editMovie(movie, index)"></q-btn> <q-btn icon="delete" flat color="red" @click="deleteMovie(movie.id)"></q-btn>
        </li>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      movName: '',
      yr: '',
      movieId: '',
      movieList: [],
      isEdit: false
    }
  },
  created () {
    // get from firebase
    console.log(this.$db.collection('movies'));
    this.$bind('movieList', this.$db.collection('movies'));
  },
  methods: {
    addMovie () {
      console.log('add')
      // Add a new document in collection "cities"
      this.$db.collection('movies').add({
        name: this.movName,
        year: this.yr
      });
      this.movName = '';
      this.yr = '';
    },
    deleteMovie (id) {
      this.$db.collection('movies').doc(id).delete().then(function() {
          console.log("Document successfully deleted!");
      }).catch(function(error) {
          console.error("Error removing document: ", error);
      });
    },
    editMovie (data, i) {
      console.log('edit')
      this.$router.push('/newpage/' + data.id)
    }
  }
}
</script>
