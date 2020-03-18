<template>
  <div id="app">
    <h1>Mail</h1>
    <div class="box">
      Send mail:
      <md-button
        class="md-raised md-primary"
        type="button"
        @click="showModalForm"
      >
        Open Modal!
      </md-button>
    </div>
    <ModalForm
      v-show="isModalFormVisible"
      @close="closeModalForm"
      @add-mail="AddMail"
    />
    <MailTable
      v-if="mails.length"
      v-bind:mails="mails"
      @remove-mail="removeMail"
    />
    <md-table v-else>
      <md-table-row>
        <md-table-head>№</md-table-head>
        <md-table-head>Title</md-table-head>
        <!-- <md-table-head>Recipient</md-table-head> -->
        <md-table-head>Button</md-table-head>
      </md-table-row>
      <md-table-row>
        <md-table-head>Not found mails</md-table-head>
      </md-table-row>
    </md-table>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view /> -->
  </div>
</template>

<script>
import ModalForm from "@/components/ModalForm.vue";
import MailTable from "@/components/MailTable.vue";
export default {
  data() {
    return {
      mails: [],
      showModal: false,
      loading: true,
      isModalFormVisible: false
    };
  },
  mounted() {
    if (localStorage.getItem("mails")) {
      try {
        this.mails = JSON.parse(localStorage.getItem("mails"));
      } catch (e) {
        localStorage.removeItem("mails");
      }
    }
    console.log("title", this.title);
  },
  methods: {
    removeMail(id) {
      this.mails = this.mails.filter(m => m.id !== id);
    },
    AddMail(mail) {
      this.mails.push(mail);
    },
    showModalForm() {
      this.isModalFormVisible = true;
    },
    closeModalForm() {
      this.isModalFormVisible = false;
    }
  },
  components: {
    MailTable,
    ModalForm
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

<style lang="sass" scoped>
.box
  display: grid
  grid-template-columns: auto auto
  align-items: center
  justify-content: center
  margin: 20px
</style>
