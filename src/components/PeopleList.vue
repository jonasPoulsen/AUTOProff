<template>
    <div class="peoplelist">
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
    }
  }
  </script>
  
  <style scoped>
  .peoplelist {
    display:flex;
    flex-direction: column;
  }

  </style>
  