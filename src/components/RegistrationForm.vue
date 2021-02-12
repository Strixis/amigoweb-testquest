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
        v-model.trim="formValues.name"
        @change="validate()"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.name,  }"
      >
        Введено не корректное значение
      </span>
    </label>
    <label class="registration-form_label">
      <span class="registration-form_title">Еmail</span>
      <input type="text"
        class="registration-form_input"
        :class="{'registration-form_input__filled': formValues.email !== ''}"
        placeholder="Введите ваш email"
        v-model="formValues.email"
        @change="validate()"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.email }"
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
        @change="validate()"
      >
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.phone }"
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
      <span class="registration-form_error"
        :class="{ '__visible': !isValid.formValues.choosenLanguage }"
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

      formValues: {
        name: '',
        email: '',
        phone: '',
        choosenLanguage: '',
        agreement: false,
      },
      isValid: {
        formValues: {
          name: true,
          email: true,
          phone: true,
          choosenLanguage: true,
          agreement: true,
        },
        total: false,
      }
    };
  },
  methods: {
    changeLanguage(language, event) {
      this.formValues.choosenLanguage = language;
      this.isOpen = !this.isOpen;
      this.validate('language');
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

      this.isValid.formValues.choosenLanguage = this.formValues.choosenLanguage !== "" ?
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
