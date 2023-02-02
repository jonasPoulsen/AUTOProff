<template>
    <div class="createform">
        
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
            
            <button @click="storeNewUser">Gem</button>
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
        storeNewUser(e) {
            e.preventDefault();

            if (localStorage.getItem("people") === null) {
                localStorage.setItem("people", "[]");
            }

                
            const storedData = JSON.parse(localStorage.getItem("people"))
            //const bob = JSON.parse(storedData)
            //console.log(storedData)

            storedData.push(
                        {
                            "id": Date.now(),
                            "name": this.formName, 
                            "department": this.formDepartment, 
                            "possition": this.formPossition, 
                            "birthday": this.formBirthday,
                            "phone": this.formPhone
                        })

            localStorage.setItem("people", JSON.stringify(storedData));

            this.formName = ""
            this.formDepartment = ""
            this.formPossition = ""
            this.formBirthday = ""
            this.formPhone = ""

            this.$refs.formName.focus()
                

            //localStorage.setItem("people", JSON.stringify(this.jsonData));

            
        }
    },
    mounted() {
        this.$refs.formName.focus()
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  