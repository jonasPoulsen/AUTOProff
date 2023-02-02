<template>
    <div class="peoplelist">
        <!-- <div v-for="(item, index) in peopleData" :key="index">
            {{ index }} - {{ item.name }} - {{ item.possition }}
        </div> -->
        <PersonCard v-for="item in peopleData" :key="item.id" :personData="item"/>
    </div>
  </template>
  
  <script>
  import PersonCard from '@/components/PersonCard.vue'

  export default {
    name: 'PeopleList',
    components: {
        PersonCard,
    },
    props: {
        peopleData: Array
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
  .peoplelist {
    display:flex;
    flex-direction: column;
  }

  </style>
  