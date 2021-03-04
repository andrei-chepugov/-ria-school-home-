<template>
  <div>
    <div class="alert alert-danger" role="alert" v-if="errors.name">
      Name: Довжина поля не повинна перевищувати 20 символів.
    </div>
    <div class="alert alert-danger" role="alert" v-if="errors.email">
      Email: Введіть валідне значення.
    </div>
    <div class="alert alert-danger" role="alert" v-if="errors.age">
      Age: Поле приймае тільки цифри. Довжина поля до 3 цифр.
    </div>
  </div>
</template>

<script>
export default {
  name: "Error",
  props: ['errors']
}
</script>

<style scoped>

</style>