<template>
    <router-link
    :to="{ name: 'rediger-person', params: { id: personData.id }}"
      custom
      v-slot="{ navigate }"
    >
        <button class="personcard" @click="navigate" role="link">
            <p class="personcard-name">{{ personData.name }}</p>
            <p class="personcard-phone"><span>&#128222;</span> {{ personData.phone }}</p>
            <p class="personcard-info">{{ personData.department }} - {{ personData.possition }} - {{ personData.birthday }}</p>
        </button>
    </router-link>
  </template>
  
  <script>
  export default {
    name: 'PersonCard',
    props: {
        personData: Object
    }
  }
  </script>
  
  <style scoped>
  .personcard {
    background-color: white;
    margin-top: 10px;
    border: 1px solid gray;
    border-radius: 5px;
  }
  .personcard-name {
    font-size: 18px;
    font-weight: 700;
    
  }
  .personcard-phone {
    font-size: 15px;
    font-weight: 600;
  }
  .personcard-info {
    font-size: 16px;
  }
  p {
    text-transform: capitalize;
  }

  </style>
  