<template>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Age</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(user, i) in users">
      <th scope="row">{{ i + 1 }}</th>
      <td>{{ capitalize(user.name) }}</td>
      <td>{{ user.email }}</td>
      <td>{{ user.age }}</td>
    </tr>
    </tbody>
  </table>
</template>

<script>
const capitalizeFirstLetter = (string) => string.charAt(0).toUpperCase() + string.slice(1);

export default {
  name: "UserList",
  props: ['users'],
  methods: {
    capitalize: capitalizeFirstLetter
  }
}
</script>

<style scoped>

</style>