<template>
  <div>
    <form class="form" @submit.prevent="onSubmit()">
      <General :dirty="selectDirty" ref="general" />
      <Adress ref="adress" />
      <Passport ref="passport" />
      <button
        class="submit-button"
      >
        <span class="pre-state-msg">Отправить</span>
      </button>
    </form>
    <Modal v-show="successModal" @close="successModal = false"/>
  </div>
</template>

<script>
import General from "./data/General.vue";
import Adress from "./data/Adress.vue";
import Passport from "./data/Passport.vue";
import Modal from "./Modal.vue";

export default {
  name: "login",
  data: () => ({
    stateId: 0,
    selectDirty: false,
    successModal: false,
  }),
  components: {
    General,
    Adress,
    Passport,
    Modal,
  },
  methods: {
    onSubmit() {
      this.selectDirty = true;
      if (
        this.$refs.general.$v.$invalid ||
        this.$refs.adress.$v.$invalid ||
        this.$refs.passport.$v.$invalid
      ) {
        this.$refs.adress.$v.$touch();
        this.$refs.passport.$v.$touch();
        this.$refs.general.$v.$touch();
        return;
      }
     this.successModal = true;
    },
  },
};
</script>

<style lang="sass">


.field
  display: flex
  flex-direction: column
  justify-content: flex-start
  padding: 10px
  align-items: flex-start
  text-align: left
  width: 100%
  &_half
    width: 50%

.fields
  padding-top: 3%

.group
  display: flex
  justify-content: space-between

@media (max-width: 650px) 
  .group
    flex-wrap: wrap
  .field_half
    width: 100%

</style>
