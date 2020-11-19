<template>
  <div class="passport">
    <h2 class="title">Паспорт</h2>
    <div class="fields">
      <div class="field">
        <h3 class="select__title">Тип документа</h3>
        <div
          class="select"
          :class="{
            select_invalid:
              $v.passport.selectType.$dirty && !$v.passport.selectType.required,
          }"
        >
          <select
            v-model="passport.selectType"
            class="select__item"
            :class="{
              select__item_invalid:
                $v.passport.selectType.$dirty &&
                !$v.passport.selectType.required,
            }"
          >
            <option hidden disabled selected value="">
              Выберите тип документа
            </option>
            <option
              v-for="(type, index) in passport.types"
              :value="type"
              :key="index"
              class="select__option"
            >
              {{ type }}
            </option>
          </select>
        </div>
        <span
          class="select__invalid"
          v-if="
            $v.passport.selectType.$dirty && !$v.passport.selectType.required
          "
        >
          * Это поле обязательно для заполнения
        </span>
      </div>
      <div class="group">
        <div class="field">
          <div class="input">
            <h3 class="input__title">Серия</h3>
            <input
              class="input__item"
              placeholder="Серия"
              type="number"
              v-model.trim="passport.series"
            />
          </div>
        </div>
        <div class="field">
          <div class="input">
            <h3 class="input__title">Номер</h3>
            <input
              class="input__item"
              placeholder="Номер"
              type="number"
              v-model.trim="passport.number"
            />
          </div>
        </div>
      </div>
      <div class="field">
        <div class="textarea">
          <h3 class="textarea__title">Кем выдан</h3>
          <textarea
            class="textarea__item"
            placeholder="Кем выдан"
            type="textarea"
            v-model.trim="passport.given"
            rows="3"
          />
        </div>
      </div>
      <div class="field">
        <div class="date">
          <h3 class="date__title">Дата выдачи</h3>
          <input
            class="date__input"
            placeholder="Номер"
            type="date"
            v-model.trim="passport.givenDate"
            @blur="$v.passport.givenDate.$touch()"
            :class="{
              date__input_invalid:
                $v.passport.givenDate.$dirty && !$v.passport.givenDate.required,
            }"
          />
        </div>
        <span
          class="input__invalid"
          v-if="$v.passport.givenDate.$dirty && !$v.passport.givenDate.required"
        >
          * Это поле обязательно для заполнения
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";

export default {
  data: () => ({
    passport: {
      types: ["Паспорт", "Свидетельство о рождении", "Вод. удостоверение"],
      selectType: "",
      series: "",
      number: "",
      given: "",
      givenDate: "",
    },
  }),
  validations: {
    passport: {
      selectType: {
        required,
      },
      givenDate: {
        required,
      },
    },
  },
};
</script>

<style lang="sass" scoped>
  .passport
    margin-top: 5%
</style>