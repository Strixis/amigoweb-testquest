<template>
  <form class="registration-form">
    <h1 class="registration-form_heading">Регистрация</h1>
    <p class="registration-form_sub-heading">
      Уже есть аккаунт? <a href="#" class="link">Войти</a>
    </p>
    <label class="registration-form_label">
      <span class="registration-form_title">Имя</span>
      <input type="text"
        class="registration-form_input"
        :class="{'registration-form_input__filled': formValues.name !== ''}"
        placeholder="Введите Ваше имя"
        v-model="formValues.name"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid,  }"
      >
        Введено не корректное значение
      </span>
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Еmail</span>
      <input type="text"
        class="registration-form_input"
        :class="{'registration-form_input_filled': formValues.email !== ''}"
        placeholder="Введите ваш email"
        v-model="formValues.email"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid }"
      >
        Введено не корректное значение
      </span>
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Номер телефона</span>
      <input type="text"
        class="registration-form_input"
        :class="{'registration-form_input__filled': formValues.phone !== ''}"
        placeholder="Введите номер телефона"
        v-model="formValues.phone"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid }"
      >
        Введено не корректное значение
      </span>
    </label>
    <div class="registration-form_label">
      <span class="registration-form_title">Язык</span>
      <button @click.prevent="isOpen = !isOpen"
        class="pseudo-select"
        :class="{
          'pseudo-select__focus': isOpen,
          'pseudo-select__filled': formValues.choosenLanguage !== ''
        }"
      >
        {{ formValues.choosenLanguage === "" ? 'Язык' : formValues.choosenLanguage }}
      </button>
      <div v-show="isOpen" class="pseudo-select_list">
        <button class="pseudo-select_item"
          @click="changeLanguage('Русский', $event)"
        >
          Русский
        </button>
        <button class="pseudo-select_item"
          @click="changeLanguage('Английский', $event)"
        >
          Английский
        </button>
        <button class="pseudo-select_item"
          @click="changeLanguage('Китайский', $event)"
        >
          Китайский
        </button>
        <button class="pseudo-select_item"
          @click="changeLanguage('Испанский', $event)"
        >
          Испанский
        </button>
      </div>
    </div>
    <label class="registration-form_checkbox-label">
      <input type="checkbox" class="registration-form_checkbox" v-model="formValues.agreement">
      <div class="pseudo-checkbox"></div>
      <span>Принимаю <a href="#" class="link">условия</a> использования</span>
    </label>
    <button type="submit"
      class="registration-form_submit-button"
      :class="{ 'registration-form_submit-button__disabled': !isValid }"
      @click="sendData($event)"
    >
      Зарегистрироваться
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      isValid: true,
      testValue: 1,
      isOpen: false,

      formValues: {
        name: '',
        email: '',
        phone: '',
        choosenLanguage: '',
        agreement: false,
      },
    };
  },
  methods: {
    changeLanguage(language, event) {
      this.formValues.choosenLanguage = language;
      this.isOpen = !this.isOpen;
      event.preventDefault();
    },
    sendData(event) {
      if (this.isValid) {
        console.log({...this.formValues});
        event.preventDefault();
      } else {
        event.preventDefault()
      };
    },
  },
}
</script>
