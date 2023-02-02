<template>
    <div class="createform">
        
        <form class="d-flex flex-column">
            <div class="createform-input-holder">
                <p class="createform-label">Skriv navn</p>
                <p v-if="this.formName === ''" class="createform-required">*Ufyld dette felt</p>
                <input v-model="formName" placeholder="Navn" ref="formName" />
            </div>
            <div class="createform-input-holder">
                <p class="createform-label">Afdeling</p>
                <p v-if="this.formDepartment === ''" class="createform-required">*Ufyld dette felt</p>
                <select v-model="formDepartment" ref="formDepartment">
                    <option disabled value="">Vælg afdeling</option>
                    <option>Afd. Syd</option>
                    <option>Afd. Nord</option>
                    <option>Afd. Vest</option>
                </select>
            </div>
            <div class="createform-input-holder">
                <p class="createform-label">Stilling</p>
                <p v-if="this.formPossition === ''" class="createform-required">*Ufyld dette felt</p>
                <input v-model="formPossition" placeholder="Stilling" ref="formPossition" />
            </div>
            <div class="createform-input-holder">
                <p class="createform-label">Fødelsdag</p>
                <p v-if="this.formBirthday === ''" class="createform-required">*Ufyld dette felt</p>
                <input v-model="formBirthday" placeholder="DD-MM-ÅÅÅÅ" ref="formBirthday" />
            </div>
            <div class="createform-input-holder">
                <p class="createform-label">Telefon</p>
                <p v-if="this.formPhone === ''" class="createform-required">*Ufyld dette felt</p>
                <input v-model="formPhone" placeholder="Telefon" ref="formPhone" />
            </div>
            
            <button class="save-button" @click="storeNewUser">Gem</button>
        </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CreateForm',
    data() {
        return {
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
        storeNewUser(e) {
            e.preventDefault();

            if (localStorage.getItem("people") === null) {
                localStorage.setItem("people", "[]");
            }

            if (this.validateInput()) {
            
                const storedData = JSON.parse(localStorage.getItem("people"))

                storedData.push(
                            {
                                "id": Date.now(),
                                "name": this.formName.toLowerCase(),
                                "department": this.formDepartment.toLowerCase(),
                                "possition": this.formPossition.toLowerCase(),
                                "birthday": this.formBirthday.toLowerCase(),
                                "phone": this.formPhone.toLowerCase()
                            })

                localStorage.setItem("people", JSON.stringify(storedData));

                this.formName = ""
                this.formDepartment = ""
                this.formPossition = ""
                this.formBirthday = ""
                this.formPhone = ""

                this.$router.push({ name: 'people' })
            }
            
        }
    },
    mounted() {
        this.$refs.formName.focus()
    }
  }
  </script>
  
  <style scoped>
    .createform-required {
        font-size: 10px;
        color: red;
        margin-block-end: 0;
        margin-block-start: 0;
        
    }
    .createform-input-holder {
        margin-bottom: 25px;
    }
    .save-button {
        width: 120px;
        height: 35px;
        font-size: 18px;
        font-weight: 600;
        border-radius: 8px;
    }
    .createform-label {
        margin-block-end: 0;
    }
  </style>
  