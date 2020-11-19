<template>
  <div class="general">
    <h2 class="title">Общая информация</h2>
    <div class="fields">
      <div class="field">
        <div class="input">
          <h3 class="input__title">Имя</h3>
          <input
            class="input__item"
            placeholder="Имя"
            type="text"
            v-model.trim="firstName"
            @blur="$v.firstName.$touch()"
            :class="{
              input__item_invalid: $v.firstName.$dirty && $v.firstName.$invalid,
            }"
          />
          <span
            class="input__invalid"
            v-if="$v.firstName.$dirty && !$v.firstName.required"
          >
            * Это поле обязательно для заполнения
          </span>
          <span
            class="input__invalid"
            v-else-if="$v.firstName.$dirty && !$v.firstName.alpha"
          >
            * Это поле должно содержать только буквы
          </span>
        </div>
      </div>
      <div class="field">
        <div class="input">
          <h3 class="input__title">Фамилия</h3>
          <input
            class="input__item"
            placeholder="Фамилия"
            type="text"
            v-model.trim="lastName"
            @blur="$v.lastName.$touch()"
            :class="{
              input__item_invalid: $v.lastName.$dirty && $v.lastName.$invalid,
            }"
          />
          <span
            class="input__invalid"
            v-if="$v.lastName.$dirty && !$v.lastName.required"
          >
            * Это поле обязательно для заполнения
          </span>
          <span
            class="input__invalid"
            v-else-if="$v.lastName.$dirty && !$v.lastName.alpha"
          >
            * Это поле должно содержать только буквы
          </span>
        </div>
      </div>
      <div class="field">
        <div class="input">
          <h3 class="input__title" for="middleName">Отчество</h3>
          <input
            class="input__item"
            id="middleName"
            placeholder="Отчество"
            type="text"
            v-model.trim="middleName"
            @blur="$v.middleName.$touch()"
            :class="{
              input__item_invalid:
                $v.middleName.$dirty && $v.middleName.$invalid,
            }"
          />
          <span
            class="input__invalid"
            v-if="$v.middleName.$dirty && !$v.middleName.alpha"
          >
            * Это поле должно содержать только буквы
          </span>
        </div>
      </div>
      <div class="group">
        <div class="field field_half">
          <div class="date">
            <h3 class="date__title">Дата рождения</h3>
            <input
              class="date__input"
              type="date"
              name="birthDate"
              v-model="birthDate"
              @blur="$v.birthDate.$touch()"
              :class="{
                date__input_invalid:
                  $v.birthDate.$dirty && !$v.birthDate.required,
              }"
            />
            <span
              class="input__invalid"
              v-if="$v.birthDate.$dirty && !$v.birthDate.required"
            >
              * Это поле обязательно для заполнения
            </span>
          </div>
        </div>
        <div class="field field_half">
          <div class="phone">
            <h3 class="phone__title" for="phone">Номер телефона</h3>
            <div class="phone__item">
              <span class="phone__preholder"> +7 </span>
              <input
                type="tel"
                v-model="phone"
                name="phone"
                id="phone"
                placeholder="(555) 555-5555"
                autocomplete="tel"
                maxlength="14"
                class="phone__input"
                v-phone
                pattern="[(][0-9]{3}[)] [0-9]{3}-[0-9]{4}"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="field">
        <div class="radio">
          <h3 class="radio__title">Пол</h3>
          <div class="radio__items">
            <label for="gender-male" class="radio__label">
              <input
                type="radio"
                name="gender"
                value="male"
                id="gender-male"
                class="radio__input"
                v-model="gender"
              />
              <span>Мужской</span>
            </label>
            <label for="gender-female" class="radio__label">
              <input
                type="radio"
                name="gender"
                class="radio__input"
                value="female"
                id="gender-female"
                v-model="gender"
              />
              <span>Женский</span></label
            >
          </div>
        </div>
      </div>
      <div class="group">
        <div class="field">
          <h3 class="select__title">Группа клиентов</h3>
          <div
            class="select"
            :class="{
              select_invalid: dirty == true && selectGroup.length == 0,
            }"
          >
            <button
              class="select__item"
              type="button"
              @click="
                showGroups = !showGroups;
                dirty = true;
              "
              :class="{
                select__item_invalid: dirty == true && selectGroup.length == 0,
              }"
            >
              <div v-if="selectGroup.length != 0">
                <span v-for="(select, i) in selectGroup" :key="select.id">
                  {{ select.value
                  }}{{ i &lt; selectGroup.length - 1 ? ', ' : '' }}
                </span>
              </div>
              <div v-else>
                <span>Выберите группу</span>
              </div>
            </button>
            <div
              class="select__dropdown"
              :class="{
                select__dropdown_active: showGroups,
              }"
            >
              <ul class="select__list">
                <li
                  v-for="group in clientGroups"
                  :value="group.value"
                  :key="group.id"
                  @click="group.active = !group.active"
                  class="select__option"
                  :class="{
                    select__option_active: group.active,
                  }"
                >
                  {{ group.value }}
                </li>
              </ul>
            </div>
          </div>
          <span
            class="select__invalid"
            v-if="dirty == true && selectGroup.length == 0"
          >
            * Это поле обязательно для заполнения
          </span>
        </div>
        <div class="field">
          <h3 class="select__title">Лечащий врач</h3>
          <div class="select">
            <select v-model="selectDoctor" class="select__item">
              <option hidden disabled selected value="">
                Выберите лечащего врача
              </option>
              <option
                v-for="doctor in doctorList"
                :value="doctor.value"
                :key="doctor.id"
                class="select__option"
              >
                {{ doctor.value }}
              </option>
            </select>
          </div>
        </div>
      </div>
      <div class="field">
        <div class="checkbox">
          <input
            class="checkbox__input"
            id="cbx"
            type="checkbox"
            style="display: none"
          />
          <label class="checkbox__label" for="cbx">
            <span>
              <svg width="12px" height="10px" viewBox="0 0 12 10">
                <polyline points="1.5 6 4.5 9 10.5 1"></polyline>
              </svg>
            </span>
            <span class="checkbox__name">Не отправлять СМС</span>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";

export default {
  name: "general",
  props: {
    dirty: Boolean,
  },
  data: () => ({
    firstName: "",
    lastName: "",
    middleName: "",
    birthDate: "",
    phone: "",
    gender: "",
    clientGroups: [
      {
        id: 1,
        value: "VIP",
        active: false,
      },
      {
        id: 2,
        value: "Проблемные",
        active: false,
      },
      {
        id: 3,
        value: "ОМС",
        active: false,
      },
    ],
    showGroups: false,
    doctorList: [
      {
        id: 1,
        value: "Иванов",
      },
      {
        id: 2,
        value: "Захаров",
      },
      {
        id: 3,
        value: "Чернышева",
      },
    ],
    selectDoctor: "",
    sendSMS: false,
  }),
  validations: {
    firstName: { required, alpha: (val) => /^([а-яё]+|[a-z]+)$/i.test(val) },
    lastName: { required, alpha: (val) => /^([а-яё]+|[a-z]+)$/i.test(val) },
    middleName: {
      alpha: (val) => /^([а-яё]+|[a-z]+)|^([...])*$/i.test(val),
    },
    birthDate: { required },
    phone: { required },
  },
  directives: {
    phone: {
      inserted: function (el) {
        el.oninput = function (e) {
          if (!e.isTrusted) {
            return;
          }
          const x = this.value
            .replace(/\D/g, "")
            .match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
          this.value = !x[2]
            ? x[1]
            : "(" + x[1] + ") " + x[2] + (x[3] ? "-" + x[3] : "");
          el.dispatchEvent(new Event("input"));
        };
      },
    },
  },
  computed: {
    selectGroup() {
      return this.clientGroups.filter((group) => {
        if (group.active == true) return true;
      });
    },
  },
};
</script>

<style lang="sass" scoped>
  .general
    margin-top: 5%
</style>