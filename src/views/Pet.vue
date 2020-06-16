<template>
  <div class="data-container">
    <h2>{{ animal.name }} ({{ $route.params.species }})</h2>
    <div class="pet-details">
      <p class="p-data">Breed: <span class="values">{{ animal.breed }}</span></p>
      <p class="p-data">Gender: <span class="values">{{ animal.gender }}</span></p>
      <p class="p-data">Age: <span class="values">{{ animal.age }}</span> years old</p>
      <p class="p-data">Color: <span class="values">{{ animal.color }}</span></p>
      <p class="p-data">Weight: <span class="values">{{ animal.weight }}</span> LBS</p>
      <p class="p-data">Location: <span class="values">{{ animal.location }}</span></p>
      <p class="p-data">Notes: <span class="values">{{ animal.notes }}</span></p>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      animal: {}
    }
  },
  computed: {
    ...mapState([
      'cats',
      'dogs'
    ])
  },
  mounted () {
    const species = this.$route.params.species
    const id = this.$route.params.id
    this.animal = this[species][id]
  }
}
</script>

<style scoped>
  .data-container{
    background-color: rgb(255, 255, 227);
  }
  h2{
    background-color: lightgreen;
  }
  .pet-details{
    padding: 10px 15px;
  }
  .p-data{
    text-align: left;
  }
  .values{
    font-weight: bold;
  }
</style>
