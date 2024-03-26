<template>
  <v-card v-if="user" class="mt-4">
     <v-row no-gutters>
       <v-col cols="4">
         <v-img :src="user.image" aspect-ratio="1" class="fill-height">
          <template v-slot:placeholder>
            <div class="d-flex align-center justify-center fill-height">
              <v-progress-circular
                color="grey"
                indeterminate
              ></v-progress-circular>
            </div>
          </template>
         </v-img>
       </v-col>
       <v-col cols="8">
         <v-card-text>
           <div>Имя: {{ user.firstname }} {{ user.lastname }}</div>
           <div>Email: {{ user.email }}</div>
           <div>Пол: {{ user.gender === 'female' ? 'Женский' : 'Мужской' }}</div>
           <div>Дата рождения: {{ new Date(user.birthday).toLocaleDateString() }}</div>
           <div>Телефон: {{ user.phone }}</div>
           <div>Веб-сайт: {{ user.website }}</div>
           <div>Адрес: {{ user.address.zipcode }}, {{ user.address.county_code }}, {{ user.address.country }}, {{ user.address.city }},<br>
              {{ user.address.street }}, {{ user.address.streetName }}, {{ user.address.buildingNumber }}, <br>
              Кординаты: {{ user.address.latitude }}, {{ user.address.longitude }}
            </div>
         </v-card-text>
       </v-col>
     </v-row>
  </v-card>
 </template>
 
 <script>
 export default {
  name: "UserInfo",
  props: {
     user: {
       type: Object,
       required: true,
     },
  },
 };
 </script>
 
 <style scoped>
 .fill-height {
  height: 100%;
 }
 </style>
 