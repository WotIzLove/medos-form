<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal">
        <header class="modal__header">
          Уведомление
        </header>
        <section class="modal__body">
          <p class="modal__text">Ваши данные успешно отправлены!</p>
        </section>
        <footer class="modal__footer">
          <button type="button" class="submit-button" @click="close">
            <span class="pre-state-msg">Закрыть</span>
          </button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "modal",
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="sass">

.modal-backdrop
    position: fixed
    top: 0
    bottom: 0
    left: 0
    right: 0
    background-color: rgba(0, 0, 0, 0.3)
    display: flex
    justify-content: center
    align-items: center
    z-index: 10000
.modal
    width: 500px
    border-radius: 10px
    background: #FFFFFF
    box-shadow: 2px 2px 20px 1px
    overflow-x: auto
    display: flex
    flex-direction: column
    &__header
        padding: 15px
        display: flex
        border-bottom: 1px solid #eeeeee
        color: #00b0ff
        justify-content: space-between
    &__footer
        padding: 15px
        display: flex
        border-top: 1px solid #eeeeee
        justify-content: flex-end
    &__body
        position: relative
        padding: 20px 10px
        font-size: 20px

.modal-fade-enter,
.modal-fade-leave-active
    opacity: 0

.modal-fade-enter-active,
.modal-fade-leave-active
    transition: opacity .5s ease

@media (max-width: 650px)
  .modal
    width: 300px

</style>