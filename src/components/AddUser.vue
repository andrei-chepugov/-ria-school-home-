<template>
  <div>
    <Error v-bind:errors="errors"/>
    <form @submit.prevent="onSubmit">
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Name" v-model="name">
        </div>
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Email" v-model="email" @change="onEmailChange">
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
      age: '',
      showEmailInvalid: false
    }
  },
  methods: {
    onSubmit: function () {
      this.$emit('AddUser', {
        name: this.name,
        email: this.email,
        age: Number(this.age)
      })
      this.clean();
    },
    onEmailChange: function () {
      this.showEmailInvalid = this.isEmailInvalid && this.isEmailNonEmpty;
    },
    clean: function () {
      this.name = '';
      this.email = '';
      this.age = '';
    }
  },
  computed: {
    isNameInvalid: function () {
      return !this.name.length || this.name.length > 20;
    },
    isNameNonEmpty: function () {
      return Boolean(this.name.length);
    },
    isEmailInvalid: function () {
      return !this.email.length || !validEmail(this.email);
    },
    isEmailNonEmpty: function () {
      return Boolean(this.email.length);
    },
    isAgeInvalid: function () {
      return !this.age.trim().length || this.age.length > 3 || Number.isNaN(Number(this.age));
    },
    isAgeNonEmpty: function () {
      return Boolean(this.age.length);
    },
    errors: function () {
      return {
        name: this.isNameNonEmpty && this.isNameInvalid,
        email: this.showEmailInvalid,
        age: this.isAgeNonEmpty && this.isAgeInvalid
      }
    },
    invalid: function () {
      return this.isNameInvalid || this.isEmailInvalid || this.isAgeInvalid
    }
  },
  watch: {
    email: function () {
      this.showEmailInvalid = false;
    }
  }
}
</script>

<style scoped>

</style>