<template>
  <md-table-row>
    <md-table-cell>{{ index + 1 }}</md-table-cell>
    <md-table-cell>{{ mail.title }}</md-table-cell>
    <!-- <md-table-cell>{{ mail.recipient }}</md-table-cell> -->
    <md-table-cell>
      <md-button class="md-raised md-primary" type="button" @click="showModal">
        Open
      </md-button>
      <md-button
        class="md-raised md-accent"
        v-on:click="$emit('remove-mail', mail.id)"
      >
        Delete
      </md-button>
      <ModalMail
        v-show="isModalVisible"
        @close="closeModal"
        :mail="mail"
        :key="mail.id"
      />
    </md-table-cell>
  </md-table-row>
</template>

<script>
import ModalMail from "@/components/ModalMail";
export default {
  data() {
    return {
      isModalMailVisible: true,
      isModalVisible: false
    };
  },
  props: {
    mail: {
      type: Object,
      required: true
    },
    mails: [],
    index: Number
  },
  methods: {
    showModalMail() {
      this.isModalMailVisible = true;
    },
    closeModalMail() {
      this.isModalMailVisible = false;
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
  components: {
    ModalMail
  }
};
</script>

<style lang="sass" scoped>
li
  border: 1px solid #ccc
  display: grid
  grid-template-columns: auto auto auto auto
  align-items: center
  justify-content: left
  grid-column-gap: 20px
  padding: .5rem 2rem
  margin-bottom: 1rem
// .rm
//   width: 20px
//   height: 20px
//   background: red
//   color: #fff
//   border-radius: 50%
//   font-weight: bold
//   display: grid
//   align-items: center
//   justify-content: center

input
  margin-right: 1rem

.done
  text-decoration: line-through
</style>
