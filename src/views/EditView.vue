<template>
    <div class="">
        the id is {{  personId }} - index {{ theIndex }}
        <form class="d-flex flex-column">
            <div>
                <label>Skriv navn</label><input v-model="formName" placeholder="Navn" ref="formName" />
            </div>
            <div>
                <label>Skriv navn</label><select v-model="formDepartment" ref="formDepartment">
                    <option disabled value="">Vælg afdeling</option>
                    <option>Afd. Syd</option>
                    <option>Afd. Nord</option>
                    <option>Afd. Vest</option>
                </select>
            </div>

            <div>
                <label>Stilling</label><input v-model="formPossition" placeholder="Stilling" ref="formPossition" />
            </div>
            <div>
                <label>Fødelsdag</label><input v-model="formBirthday" placeholder="Fødselsdag DD-MM-ÅÅÅÅ" ref="formBirthday" />
            </div>
            <div>
                <label>Fødelsdag</label><input v-model="formPhone" placeholder="Telefon" ref="formPhone" />
            </div>
            
            <button @click="editThisPerson">Gem ændringer</button>
        </form>
    </div>
  </template>
  
  <script>
  import { useRoute } from 'vue-router'
  
  export default {
    name: 'EditView',
    components: {
        
    },
    props: ['id'],
    data() {
        return {
            personId: String,
            allPersons: Object,
            theIndex: Number,
            formName: "",
            formDepartment: "",
            formPossition: "",
            formBirthday: "",
            formPhone: ""
        }
    },
    methods: {
        getThisPerson() {
            //let thisPerson = localStorage.getItem("people")

            let allPeops = JSON.parse(localStorage.getItem("people"))
            this.allPersons = allPeops
            let thisPerson = allPeops
            //thisPerson = JSON.parse(thisPerson);

            thisPerson.filter((item, index) => {
                if (item.id == this.personId) {
                    this.theIndex = index
                    //this.thisPerson = item 
                    this.formName = item.name
                    this.formDepartment = item.department
                    this.formPossition = item.possition
                    this.formBirthday = item.birthday
                    this.formPhone = item.phone
                }
                return true
            })
            // console.log(allPeops[this.theIndex])
        },
        editThisPerson(e) {
            e.preventDefault()
            //console.log(this.allPersons[this.theIndex])

            let newArray = this.allPersons
            newArray[this.theIndex].name = this.formName
            newArray[this.theIndex].department = this.formDepartment
            newArray[this.theIndex].possition = this.formPossition
            newArray[this.theIndex].birthday = this.formBirthday
            newArray[this.theIndex].phone = this.formPhone
            
            localStorage.removeItem("people");
            localStorage.setItem("people", JSON.stringify(newArray));
        },
        deleteThisPerson() {

        }
        
    },
    mounted() {
        this.personId = useRoute().params.id
        this.getThisPerson()
    }
  }
  </script>

<style scoped>

</style>
  