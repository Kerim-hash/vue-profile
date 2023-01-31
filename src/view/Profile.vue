<template>
  <div class="profile">
    <div class="container">
      <h2 class="title">Мой профиль</h2>
      <UploadFile v-model="imageFile" />

      <div class="profile-items">
        <Form
          class="profile-form"
          @submit="onSubmit"
          :validation-schema="schema"
        >
          <h2 class="title">Личные данные</h2>
          <label>Имя фамилия</label>
          <Field
            id="name"
            name="name"
            type="string"
            placeholder="Имя фамилия"
          />
          <ErrorMessage class="error" name="name" />
          <label>Дата рождения</label>
          <Field id="birthDate" name="birthDate" type="date" />
          <ErrorMessage class="error" name="birthDate" />
          <label>E-mail</label>
          <Field id="email" name="email" type="email" placeholder="E-mail" />
          <ErrorMessage class="error" name="email" />
          <label>Город</label>
          <Field id="city" name="city" type="string" placeholder="Город" />
          <ErrorMessage class="error" name="city" />
          <label>email</label>
          <GroupSelectInput name="PhoneNumber" />
          <ErrorMessage class="error" name="PhoneNumber" />
          <label>Владение языками</label>
          <SelectLanguage name="Language" />
          <ErrorMessage class="error" name="Language" />
          <button class="profile-form__button">Сохранить</button>
        </Form>

        <Form
          class="profile-form"
          @submit="onSubmit"
          :validation-schema="schemaPassword"
        >
          <h2 class="title">Безопасность</h2>
          <label>Старый пароль</label>
          <Field
            name="oldPassword"
            type="password"
            placeholder="Старый пароль"
          />
          <ErrorMessage class="error" name="oldPassword" />
          <label>Новый пароль</label>
          <Field name="password" type="password" placeholder="Новый пароль" />
          <ErrorMessage class="error" name="password" />
          <label>Повторите новый пароль</label>
          <Field
            name="confirmPassword"
            type="password"
            placeholder="Повторите новый пароль"
          />
          <ErrorMessage class="error" name="confirmPassword" />
          <button class="profile-form__button">Сохранить</button>
        </Form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { Form, Field, ErrorMessage } from "vee-validate";
import * as Yup from "yup";
import UploadFile from "../components/uploadAvatar.vue";
import GroupSelectInput from "../components/groupSelectInput.vue";
import SelectLanguage from "../components/SelectLanguage.vue";

// validate
const schema = Yup.object().shape({
  email: Yup.string().email().required().label("Email Address"),
  name: Yup.string().required(),
  birthDate: Yup.string().required(),
  city: Yup.string().required(),
  Language: Yup.string().required(),
  PhoneNumber: Yup.string().required(),
});
// schema for pasword
const schemaPassword = Yup.object().shape({
  oldPassword: Yup.string().min(8).required(),
  password: Yup.string()
    .min(8)
    .matches(
      /^(?=.*[!?$^()@#&*])(?=.*[0-9])(?=.*[a-zA-Z]).{8,20}$/,
      "Password should contain 1 alphabet, 1 digit, 1 special symbol, min length 8 max 20"
    )
    .required("Password must be at least 8 characters"),
  confirmPassword: Yup.string()
    .min(8)
    .required("Password is mandatory")
    .oneOf([Yup.ref("password")], "Passwords does not match"),
});

function onSubmit(values) {
  alert(JSON.stringify(values, null, 2));
}
// upload photo
const imageFile = ref("");
</script>

<style lang="scss">
.profile {
  padding: 20px 0 50px;
  &-items {
    display: flex;
  }
  &-form {
    width: 350px;
    &:first-child {
      margin-right: 30px;
    }
    &__button {
      padding: 16px 32px;
      border-radius: 12px;
      cursor: pointer;
      margin-top: 20px;
      background: #a9c6f75e;
      transition: background 0.3s;
      width: 100%;
      &:hover {
        background: #97baf6;
      }
    }
  }
  &-group__input {
    display: flex;
    max-width: 365px;
  }
}
.container {
  width: 1000px;
  margin: 0 auto;
  max-width: 100%;
}
.title {
  margin: 20px 0;
  font-size: 30px;
  font-weight: 500;
}

@media (max-width: 1128px) {
  .profile {
    padding: 20px 20px 40px;
  }
}
@media (max-width: 1128px) {
  .profile {
    &-items {
      flex-wrap: wrap;
    }
    &-form {
      &:first-child {
        margin-right: 0;
      }
      width: 100%;
    }
  }
}
</style>
