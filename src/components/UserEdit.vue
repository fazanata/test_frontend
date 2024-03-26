<template>
  <v-form v-if="userInfo" ref="form" v-model="valid" lazy-validation class="ml-10" style="width:600px;">
     <v-text-field
       v-model="user.firstname"
       :rules="[v => !!v || 'Имя обязательно']"
       label="Имя"
       required
     ></v-text-field>
 
     <v-text-field
       v-model="user.lastname"
       :rules="[v => !!v || 'Фамилия обязательна']"
       label="Фамилия"
       required
     ></v-text-field>
 
     <v-text-field
       v-model="user.email"
       :rules="[v => !!v || 'Email обязателен', v => /.+@.+\..+/.test(v) || 'Email должен быть валидным']"
       label="Email"
       required
     ></v-text-field>
 
     <v-select
       v-model="user.gender"
       :items="['male', 'female']"
       :rules="[v => !!v || 'Пол обязателен']"
       label="Пол"
       required
     ></v-select>
    <div>Дата рождения</div>
     <v-date-picker
       v-model="user.birthday"
       :rules="[v => !!v || 'Дата рождения обязательна']"
       label="Дата рождения"
       required
     ></v-date-picker>
 
     <v-text-field
       v-model="user.phone"
       :rules="[v => !!v || 'Телефон обязателен']"
       label="Телефон"
       required
     ></v-text-field>
 
     <v-text-field
       v-model="user.website"
       :rules="[v => !!v || 'Веб-сайт обязателен']"
       label="Веб-сайт"
       required
     ></v-text-field>
 
     <v-text-field
       v-if="user.address"
       v-model="user.address.street"
       :rules="[v => !!v || 'Улица обязательна']"
       label="Улица"
       required
     ></v-text-field>

    <v-row>
      <v-col cols="9">
        <v-text-field
          v-if="user.address"
          v-model="user.address.streetName"
          :rules="[v => !!v || 'Улица обязательна']"
          label="Улица"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="3">
        <v-text-field
          v-if="user.address"
          v-model="user.address.buildingNumber"
          :rules="[v => !!v || 'Номер здания обязателен']"
          label="Номер здания"
          required
        ></v-text-field>
      </v-col>
    </v-row>
 
    <v-text-field
       v-if="user.address"
       v-model="user.address.city"
       :rules="[v => !!v || 'Город обязателен']"
       label="Город"
       required
    ></v-text-field>

    <v-row>
      <v-col cols="3">
        <v-text-field
          v-if="user.address"
          v-model="user.address.county_code"
          :rules="[v => !!v || 'Код страны обязателен']"
          label="Код страны"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="9">
        <v-text-field
          v-if="user.address"
          v-model="user.address.country"
          :rules="[v => !!v || 'Страна обязательна']"
          label="Страна"
          required
        ></v-text-field>
      </v-col>
    </v-row>
 
    <v-text-field
        v-if="user.address"
       v-model="user.address.zipcode"
       :rules="[v => !!v || 'Индекс обязателен']"
       label="Индекс"
       required
    ></v-text-field>

    <v-row>
      <v-col cols="6">
        <v-text-field
          v-if="user.address"
          v-model="user.address.latitude"
          :rules="[v => !!v || 'Широта обязательна']"
          label="Широта"
          required
        ></v-text-field>
      </v-col>
      <v-col cols="6">
        <v-text-field
          v-if="user.address"
          v-model="user.address.longitude"
          :rules="[v => !!v || 'Долгота обязателен']"
          label="Долгота"
          required
        ></v-text-field>
      </v-col>
    </v-row>

    <v-img :src="imageUrl" aspect-ratio="1" class="fill-height">
          <template v-slot:placeholder>
            <div class="d-flex align-center justify-center fill-height">
              <v-progress-circular
                color="grey"
                indeterminate
              ></v-progress-circular>
            </div>
          </template>
    </v-img>
    <v-file-input
          label="Загрузите изображение"
          v-model="imageFile"
          @change="onFileChange"
    ></v-file-input>

    <v-btn :disabled="!valid" @click="submit" class="mt-4">Сохранить</v-btn>
  </v-form>
 </template>
 
<script>
export default {
 props: {
    userInfo: {
      type: Object,
      required: true,
    },
 },
 data: () => ({
    valid: true,
    user: {},
    imageFile: [],
    imageUrl: null,
 }),
 watch:{
  userInfo:{
    deep: true,
    immediate: true,
    handler(val){
      this.user = val;
      this.imageUrl = val.image;
      this.imageFile = val.image;
    }
  }
 },
 methods: {
    submit() {
      if (this.$refs.form.validate()) {
        // Здесь обработать отправку данных, отправить их на сервер
      }
    },
    onFileChange(file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        this.imageUrl = e.target.result;
      };
      reader.readAsDataURL(file);
    },
 }
};
</script>