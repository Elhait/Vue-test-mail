<script>
export default {
  name: "modal",
  props: {
    mail: {
      type: Object,
      required: true
    },
    mails: [],
    index: Number
  },
  methods: {
    close() {
      this.$emit("close");
    }
  }
};
</script>

<template>
  <div class="modal-backdrop">
    <div class="modal">
      <header class="modal-header">
        <slot name="header">
          Full mail

          <button type="button" class="btn-close" @click="close">
            x
          </button>
        </slot>
      </header>
      <section class="modal-body">
        <slot name="body">
          <div class="top">
            <span>Title:</span>
            <span>{{ mail.title }}</span>
            <span>Recipient:</span>
            <span>{{ mail.recipient }}</span>
          </div>
          <div class="main">
            <span>Message content:</span>
            <span>{{ mail.textarea }}</span>
          </div>
        </slot>
      </section>
      <!-- <footer class="modal-footer">
        <slot name="footer">
          I'm the default footer!

          <button type="button" class="btn-green" @click="close">
            Close me!
          </button>
        </slot>
      </footer> -->
    </div>
  </div>
</template>

<style lang="sass" scoped>
.modal-body
  .top
    display: grid
    grid-template-columns: auto auto
    grid-column-gap: 2rem
    grid-row-gap: 1rem
    justify-content: start
    text-align: start
    // border-bottom: 1px solid #eeeeee
    padding-bottom: 1rem
  .main
    display: grid
    grid-template-columns: auto
    grid-row-gap: 1rem
    justify-content: start
    text-align: start
</style>
