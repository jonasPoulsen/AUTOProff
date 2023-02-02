<template>
    <router-link
    :to="{ name: 'rediger-person', params: { id: personData.id }}"
      custom
      v-slot="{ navigate }"
    >
        <button class="personcard" @click="navigate" role="link">
            {{ personData.name }} - {{ personData.possition }} - {{ personData.department }}
        </button>
    </router-link>
  </template>
  
  <script>
  export default {
    name: 'PersonCard',
    props: {
        personData: Object
    },
    methods: {
        goToEdit() {

        }
    },
    data() {
        return {
            //peopleData: Array
        }
    },
    mounted() {
        // const people = localStorage.getItem("people")
        // this.peopleData = JSON.parse(people)
        //console.log(people)
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  