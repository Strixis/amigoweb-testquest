<template>
  <form class="registration-form">
    <h1 class="registration-form_heading">Регистрация</h1>
    <p class="registration-form_sub-heading">
      Уже есть аккаунт? <a href="#" class="link">Войти</a>
    </p>
    <label v-for="(field, index) of fields"
      :key="index"
     class="registration-form_label">
      <span class="registration-form_title">{{field.text}}</span>
      <input type="text"
        class="registration-form_input"
        :class="{'registration-form_input__filled': formValues[field.name] !== ''}"
        :placeholder="field.placeholder"
        v-model.trim="formValues[field.name]"
        @change="validate()"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues[field.name] }"
      >
        {{ field.errorMessage }}
      </span>
    </label>
    <div class="registration-form_label">
      <span class="registration-form_title">Язык</span>
      <button @click.prevent="isOpen = !isOpen"
        class="pseudo-select"
        :class="{
          'pseudo-select__focus': isOpen,
          'pseudo-select__filled': formValues.language !== ''
        }"
      >
        {{ formValues.language === "" ? 'Язык' : choosenLanguage }}
      </button>
      <div v-show="isOpen" class="pseudo-select_list">
        <button class="pseudo-select_item"
          v-for="(language, index) of languages"
          :key="index"
          @click="changeLanguage(language, $event)"
        >
          {{ language.text }}
        </button>
      </div>
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.language }"
      >
        Введено не корректное значение
      </span>
    </div>
    <label class="registration-form_checkbox-label">
      <input
        type="checkbox"
        class="registration-form_checkbox"
        v-model="formValues.agreement"
        @change="validate()"
      >
      <div class="pseudo-checkbox"></div>
      <span>Принимаю <a href="#" class="link">условия</a> использования</span>
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.agreement }"
      >
        Введено не корректное значение
      </span>
    </label>
    <button type="submit"
      class="registration-form_submit-button"
      :class="{ 'registration-form_submit-button__disabled': !isValid.total }"
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
      isOpen: false,
      fields: [
        {
          name: 'name',
          text: 'Имя',
          placeholder: 'Введите Ваше имя',
          errorMessage: 'Введено не корректное значение',
        },
        {
          name: 'email',
          text: 'Email',
          placeholder: 'Введите ваш email',
          errorMessage: 'Введено не корректное значение',
        },
        {
          name: 'phone',
          text: 'Номер телефона',
          placeholder: 'Введите номер телефона',
          errorMessage: 'Введено не корректное значение',
        },
      ],
      languages: [
        {text: 'Русский', value: 'russian'},
        {text: 'Английский', value: 'english'},
        {text: 'Китайский', value: 'chinese'},
        {text: 'Испанский', value: 'spain'},
      ],
      choosenLanguage: '',

      formValues: {
        name: '',
        email: '',
        phone: '',
        language: '',
        agreement: false,
      },
      isValid: {
        formValues: {
          name: true,
          email: true,
          phone: true,
          language: true,
          agreement: true,
        },
        total: false,
      }
    };
  },
  methods: {
    changeLanguage(language, event) {
      this.formValues.language = language.value;
      this.choosenLanguage = language.text;
      this.isOpen = !this.isOpen;
      this.validate();
      event.preventDefault();
    },
    sendData(event) {
      if (this.isValid.total) {
        const sendValue = {...this.formValues};
        sendValue.phone = sendValue.phone.replace(/\D/g, "");
        alert(JSON.stringify(sendValue));
        event.preventDefault();
      } else {
        event.preventDefault();
      };
    },
    validate() {
      const nameRule = /^[\p{L} -]+$/igu;
      this.isValid.formValues.name = this.formValues.name.match(nameRule) ? true : false;

      const falseMailRule = /(^\.)|(\.\.)|(\.@)/;
      const trueMailRule = /^[\w-\.]+@[a-z]+\.[a-z]{2,}$/ig;
      const mail = this.formValues.email;
      this.isValid.formValues.email = (
        !mail.match(falseMailRule) && mail.match(trueMailRule) && mail.length < 78
      ) ? true : false;

      const phoneRule = /^[\d()+-]+$/g;
      const phone = this.formValues.phone;
      this.isValid.formValues.phone = (
        phone.match(phoneRule) && phone.replace(/\D/g, "").length === 11
      ) ? true : false;

      this.isValid.formValues.language = this.formValues.language !== "" ?
        true :
        false;
        
      this.isValid.formValues.agreement = this.formValues.agreement;

      this.isValid.total = Object.values(this.isValid.formValues).every(
        (element) => element === true
      ) ? true : false;
    },
  },
}
</script>
