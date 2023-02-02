<template>
    <div class="container">
        <div class="fixed">
            <h3>Søg efter personele her</h3>
            <input type="text" placeholder="Skriv navn" v-model="searchVal" ref="searchVal" />
            <div class="card-wrapper">
                <PersonCard v-for="(item, index) in searchPerson" :key="index" :personData="item" />
            </div>
        </div>
        <div class="flex-item">
             <PeopleList :peopleData="peopleData" /> 
        </div>
    </div>
  </template>
  
  <script>
  import PeopleList from '@/components/PeopleList.vue'
  import PersonCard from '@/components/PersonCard.vue'
  
  
  export default {
    name: 'PeopleView',
    components: {
        PeopleList,
        PersonCard,
    },
    data() {
        return {
            peopleData: [],
            searchVal: "",
            searchArray: []
        }
    },
    computed: {
        searchPerson() {
            if (this.searchVal.length > 2) {
                
                let tempPeople = this.peopleData;
                
                tempPeople = tempPeople.filter((item) => {
                    return (item.name.includes(this.searchVal))
                })
                
                return tempPeople;
            }else{
                return null
            }
            
        }
    },
    mounted() {
        const people = localStorage.getItem("people")
        this.peopleData = JSON.parse(people)

        this.$refs.searchVal.focus()
    }
  }
  </script>

<style scoped>
.container {
    display:flex;
}
.fixed {
    width: 400px;
}
.flex-item {
    flex-grow: 2;
    padding-left: 75px;
    
}
.card-wrapper {
    display:flex;
    flex-direction: column;
}
</style>
  