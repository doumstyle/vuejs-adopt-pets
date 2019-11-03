<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    <span>{{ getAllCats.length }} cats</span> |
    <span>{{ getAllDogs.length }} dogs</span> |
    <span>{{ animalsCount }} pets total</span><br>
    <button @click="togglePetForm" class="btn btn-primary mt-3 mb-3">Add New Pet</button>

    <b-form @submit.prevent="onSubmit" @reset="onReset" v-if="showPetForm">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['Select species', 'cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.age"
          required
          placeholder="Enter age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" class="btn btn-success mr-3">Submit</b-button>
      <b-button type="reset" class="btn btn-danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
    name: 'home',
    data() {
      return {
        showPetForm: false,
        formData: {
          name: '',
          age: 0,
          species: null
        }
      }
    },
    computed: {
      ...mapGetters([
        'animalsCount',
        'getAllCats',
        'getAllDogs'
      ])
    },
    methods: {
      ...mapActions([
        'addPet'
      ]),
      togglePetForm() {
        this.showPetForm = !this.showPetForm
      },
      onSubmit() {
        const { species, age, name } = this.formData
        const payload = {
          species,
          pet: {
            name,
            age
          }
        }
        this.addPet(payload)
        this.onReset()
      }, 
      onReset() {
        this.formData = {
          name: '',
          age: 0,
          species: null
        }
      }
    }
}
</script>

