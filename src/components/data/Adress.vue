<template>
  <div class="adress">
    <h2 class="title">Адрес</h2>
    <div class="fields">
      <div class="field">
        <div class="input">
          <h3 class="input__title" for="index">Индекс</h3>
          <input
            class="input__item"
            placeholder="Индекс"
            type="number"
            maxlength="6"
            v-model.trim="adress.index"
          />
        </div>
      </div>
      <div class="group">
        <div class="field">
          <div class="input">
            <h3 class="input__title">Страна</h3>
            <input
              class="input__item"
              placeholder="Страна"
              type="text"
              v-model.trim="adress.country"
            />
          </div>
        </div>
        <div class="field">
          <div class="input">
            <h3 class="input__title">Область</h3>
            <input
              class="input__item"
              placeholder="Область"
              type="text"
              v-model.trim="adress.region"
            />
          </div>
        </div>
      </div>
      <div class="group">
        <div class="field">
          <div class="input">
            <h3 class="input__title">Город</h3>
            <input
              class="input__item"
              placeholder="Город"
              type="text"
              v-model.trim="adress.city"
              @blur="$v.adress.city.$touch()"
              :class="{
                input__item_invalid:
                  $v.adress.city.$dirty && $v.adress.city.$invalid,
              }"
            />
            <span
              class="input__invalid"
              v-if="$v.adress.city.$dirty && !$v.adress.city.required"
            >
              * Это поле обязательно для заполнения
            </span>
          </div>
        </div>
        <div class="field">
          <div class="input">
            <h3 class="input__title">Улица</h3>
            <input
              class="input__item"
              placeholder="Улица"
              type="text"
              v-model.trim="adress.street"
            />
          </div>
        </div>
        <div class="field">
          <div class="input">
            <h3 class="input__title">Дом</h3>
            <input
              class="input__item"
              placeholder="Дом"
              type="text"
              v-model.trim="adress.house"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";

export default {
  name: "adress",
  data: () => ({
    adress: {
      index: "",
      country: "",
      region: "",
      city: "",
      street: "",
      house: "",
    },
  }),
  validations: {
    adress: {
      city: {
        required,
      },
    },
  },
};
</script>

<style lang="sass" scoped>
  .adress 
    margin-top: 5%
</style>