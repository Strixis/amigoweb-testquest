<template>
  <form class="registration-form">
    <h1 class="registration-form_heading">Регистрация</h1>
    <p class="registration-form_sub-heading">
      Уже есть аккаунт?<a href="#" class="link">Войти</a>
    </p>
    <label class="registration-form_label">
      <span class="registration-form_title">Имя</span>
      <input type="text" class="registration-form_input" placeholder="Введите Ваше имя">
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Еmail</span>
      <input type="text" class="registration-form_input" placeholder="Введите ваш email">
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Номер телефона</span>
      <input type="text" class="registration-form_input" placeholder="Введите номер телефона">
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Язык</span>
      <select class="registration-form_select">
        <option disabled>Язык</option>
        <option value="Russian">Русский</option>
        <option value="English">Английский</option>
        <option value="Chinese">Китайский</option>
        <option value="Spanish">Испанский</option>
      </select>
    </label>
    <label class="registration-form_label">
      <input type="checkbox" class="registration-form_checkbox">
      <span>Принимаю <a href="#" class="link">условия</a> использования</span>
    </label>
    <input type="submit" class="registration-form_submit-button" placeholder="Зарегистрироваться">
  </form>
</template>

<script>
export default {
  data() {
    return {
      isValid: true,
      testValue: 1,
    };
  },
  methods: {
    test(event) {
      this.isValid ? this.testValue = 0 : event.preventDefault();
      console.log(this.testValue);
    },
  },
}
</script>
