<template>
    <div class="">
        <form class="d-flex flex-column">
            <div class="editform-input-holder">
                <h4>{{ formDepartment }}</h4>
            </div>
            <div class="editform-input-holder">
                <p class="editform-label">Skriv navn</p>
                <p v-if="this.formName === ''" class="editform-required">*Ufyld dette felt</p>
                <input v-model="formName" placeholder="Navn" ref="formName" />
            </div>

            <div class="editform-input-holder">
                <p class="editform-label">Stilling</p>
                <p v-if="this.formPossition === ''" class="editform-required">*Ufyld dette felt</p>
                <input v-model="formPossition" placeholder="Stilling" ref="formPossition" />
            </div>
            <div class="editform-input-holder">
                <p class="editform-label">Fødelsdag</p>
                <p v-if="this.formBirthday === ''" class="editform-required">*Ufyld dette felt</p>
                <input v-model="formBirthday" placeholder="Fødselsdag DD-MM-ÅÅÅÅ" ref="formBirthday" />
            </div>
            <div class="editform-input-holder">
                <p class="editform-label">Telefon</p>
                <p v-if="this.formPhone === ''" class="editform-required">*Ufyld dette felt</p>
                <input v-model="formPhone" placeholder="Telefon" ref="formPhone" />
            </div>
            <div>
                <button class="save-button" @click="editThisPerson">Gem</button>
                <button class="delete-button" @click="deleteThisPerson">Slet person</button>
            </div>
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
        validateInput() {
            if (this.formName === "" || this.formDepartment === "" || this.formPossition === "" || this.formBirthday === "" || this.formPhone === ""){
                return false;
            }
            return true;
        },
        getThisPerson() {

            let allPeops = JSON.parse(localStorage.getItem("people"))
            this.allPersons = allPeops
            let thisPerson = allPeops

            thisPerson.filter((item, index) => {
                if (item.id == this.personId) {
                    this.theIndex = index
                    this.formName = item.name
                    this.formDepartment = item.department
                    this.formPossition = item.possition
                    this.formBirthday = item.birthday
                    this.formPhone = item.phone
                }
                return true
            })
        },
        editThisPerson(e) {
            e.preventDefault()

            if (this.validateInput()) {
                
                let newArray = this.allPersons
                newArray[this.theIndex].name = this.formName.toLowerCase()
                newArray[this.theIndex].department = this.formDepartment.toLowerCase()
                newArray[this.theIndex].possition = this.formPossition.toLowerCase()
                newArray[this.theIndex].birthday = this.formBirthday.toLowerCase()
                newArray[this.theIndex].phone = this.formPhone.toLowerCase()
                
                localStorage.setItem("people", JSON.stringify(newArray));
                this.$router.push({ name: 'people' })
            }
        },
        deleteThisPerson(e) {
            e.preventDefault()

            if (confirm("Du sletter en bruger permanent - Denne handling kan ikke fortrydes bag efter!")) {
                let newArray = this.allPersons
                newArray.splice(this.theIndex, 1)
                localStorage.setItem("people", JSON.stringify(newArray));

                this.$router.push({ name: 'people' })

            }

            

        }
        
    },
    mounted() {
        this.personId = useRoute().params.id
        this.getThisPerson()
        this.$refs.formName.focus()
    }
  }
  </script>

<style scoped>
.editform-required {
    font-size: 10px;
    color: red;
    margin-block-end: 0;
    margin-block-start: 0;
    
}
.editform-input-holder {
    margin-bottom: 25px;
}
.editform-label {
    margin-block-end: 0;
}
.save-button {
    width: 120px;
    height: 35px;
    font-size: 18px;
    font-weight: 600;
    border-radius: 8px;
}
.delete-button {
    width: 120px;
    height: 35px;
    font-size: 18px;
    font-weight: 600;
    border-radius: 8px;
    background-color: red;
    color: white;
    border-color: red;
}
</style>
  