<template>
  <div>
    <Error v-bind:errors="errors"/>
    <form @submit.prevent="onSubmit">
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Name" v-model="name">
        </div>
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Email" v-model="email">
        </div>
        <div class="col-sm">
          <input type="text" class="form-control" placeholder="Your Age" v-model="age">
        </div>
      </div>
      <br>
      <div class="col">
        <button type="submit" class="btn btn-primary" v-bind:class="{'disabled': invalid}">Add
          User
        </button>
      </div>

    </form>
  </div>

</template>

<script>
import Error from "@/components/Error";

const emailPattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
const validEmail = (email) => emailPattern.test(email);

export default {
  name: "AddUser",
  components: {Error},
  data() {
    return {
      name: '',
      email: '',
      age: ''
    }
  },
  methods: {
    onSubmit: function (event) {
      this.$emit('AddUser', {
        name: this.name,
        email: this.email,
        age: Number(this.age)
      })
      this.clean();
    },
    clean: function () {
      this.name = '';
      this.email = '';
      this.age = '';
    }
  },
  computed: {
    errorName: function () {
      return this.name.length > 20;
    },
    errorEmail: function () {
      return !validEmail(this.email);
    },
    isEmailNonEmpty: function () {
      return this.email.length;
    },
    errorAge: function () {
      return this.age.length > 3 || Number.isNaN(Number(this.age));
    },
    errors: function () {
      return {
        name: this.errorName,
        email: this.isEmailNonEmpty && this.errorEmail,
        age: this.errorAge
      }
    },
    invalid: function () {
      return this.errorName || this.errorEmail || this.errorAge
    }
  },
}
</script>

<style scoped>

</style>