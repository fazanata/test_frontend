<template>
  <v-app>
    <v-main>
      1. Отображение информации о пользователе
      <br />
      <!-- TODO сделать в отдельном блоке отображение информации о выбранном пользователе с использование v-card -->
      <UserInfo v-if="selectedUser" :user="selectedUser" />
      2. Выбор пользователя
      <br />
      <!-- TODO используйте v-autocomplete для выбора пользователя -->
      <v-autocomplete
          label="Выберите пользователя"
          :items="users"
          item-text="fio"
          item-value="id"
          return-object
          v-model="selectedUser"
          :custom-filter="customFilter"
          class="ml-10 mt-5"
      ></v-autocomplete>

      3. Редактирование пользователя
      <!-- TODO добавить возможность редактировать данные пользователя -->
      <UserEdit v-if="selectedUser" :userInfo="selectedUser" />
    </v-main>
  </v-app>
</template>

<script>
import UserInfo from "./components/UserInfo";
import UserEdit from "./components/UserEdit";

export default {
  name: "App",
  components: { UserInfo, UserEdit },
  data: () => ({
      users: [],
      selectedUser: null
  }),

  methods: {
    getUsers() {
      // TODO получить список пользователей отсюда
      // https://fakerapi.it/api/v1/persons?_locale=ru_RU
      fetch('https://fakerapi.it/api/v1/persons?_locale=ru_RU')
      .then(response => response.json())
      .then(data => {
        this.users = data.data.map(x=> {
          return {
            fio: x.firstname + ' ' + x.lastname,
            ...x
          }
        });
      })
      .catch(error => console.error('Error:', error));
    },
    customFilter(item, queryText, itemText) {
      const hasValue = val => val != null ? val : ''
      const text = hasValue(itemText)
      const query = hasValue(queryText)
      return text.toString()
        .toLowerCase()
        .indexOf(query.toString().toLowerCase()) > -1
    },
  },
  mounted(){
    this.getUsers();
  }
};
</script>
