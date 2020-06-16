<template>
  <div class="home-container">
    <h2>Adopt a pet</h2>

    <span class="total-animals mr-3">{{ animalsCount }} (animals) {{ getAllCats.length }} (cats)</span>
    <button @click="toggelePetForm" class="btn btn-primary">Add New Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm" class="my-4">

      <b-form-group id="pet-name-group" label="Pet's Name:" label-for="pet-name">
        <b-form-input type="text" id="pet-name" v-model="formData.name" required placeholder="Enter name"></b-form-input>
      </b-form-group>

      <b-form-group id="pet-breed-group" label="Pet's breed:" label-for="pet-breed">
        <b-form-input type="text" id="pet-breed" v-model="formData.breed" placeholder="Enter breed"></b-form-input>
      </b-form-group>

      <b-form-group id="pet-species-group" label="Species:" label-for="pet-species">
        <b-form-select typt="text" id="pet-species" v-model="formData.species" :options="['cats', 'dogs']" required></b-form-select>
      </b-form-group>

      <b-form-group id="pet-age-group" label="Pet's Age:" label-for="pet-age">
        <b-form-input type="number" id="pet-age" v-model="formData.age" required placeholder="Enter age"></b-form-input>
      </b-form-group>

      <b-form-group id="pet-gender-group" label="Gender:" label-for="pet-gender">
        <b-form-select typt="text" id="pet-gender" v-model="formData.gender" :options="['male', 'female']" ></b-form-select>
      </b-form-group>

      <b-form-group id="pet-weight-group" label="Pet's weight:" label-for="pet-weight">
        <b-form-input type="number" id="pet-weight" v-model="formData.weight" placeholder="Enter weigh"></b-form-input>
      </b-form-group>

      <b-form-group id="pet-color-group" label="Pet's color:" label-for="pet-color">
        <b-form-input type="text" id="pet-color" v-model="formData.color" placeholder="Enter color"></b-form-input>
      </b-form-group>

       <b-form-group id="pet-location-group" label="Pet's location:" label-for="pet-location">
        <b-form-input type="text" id="pet-location" v-model="formData.location" placeholder="Enter location"></b-form-input>
      </b-form-group>

       <b-form-group id="pet-note-group" label="Pet's note:" label-for="pet-note">
        <b-form-input type="text" id="pet-note" v-model="formData.notes" placeholder="Enter note"></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger" class="ml-2">Reset</b-button>
    </b-form>

  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null,
        breed: '',
        gender: null,
        color: '',
        weight: 0,
        location: '',
        notes: ''
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    toggelePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name, breed, gender, color, weight, location, notes } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age,
          breed,
          gender,
          color,
          weight,
          location,
          notes
        }
      }
      this.addPet(payload)
      // reset form because is not submited to server, just local memory
      this.formData = {
        name: '',
        age: 0,
        species: null,
        breed: '',
        gender: null,
        color: '',
        weight: 0,
        location: '',
        notes: ''
      }
      this.showPetForm = !this.showPetForm
    }
  }
}
</script>

<style >
  .total-animals{
    font-size: 23pt;
    font-weight: bold;
  }
</style>
