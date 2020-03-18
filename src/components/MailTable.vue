<template>
  <div>
    <md-table>
      <md-table-row>
        <md-table-head>№</md-table-head>
        <md-table-head>Title</md-table-head>
        <!-- <md-table-head>Recipient</md-table-head> -->
        <md-table-head>Button</md-table-head>
      </md-table-row>

      <MailItem
        v-for="(mail, i) of mails"
        :mail="mail"
        :index="i"
        :key="mail.id"
        v-on:remove-mail="removeMail"
      />
    </md-table>
  </div>
</template>

<script>
import MailItem from "@/components/MailItem";
export default {
  name: "list",
  props: ["mails"],
  components: {
    MailItem
  },
  methods: {
    removeMail(id) {
      this.$emit("remove-mail", id);
    }
  }
};
</script>

<style lang="sass" scoped>
ul
  list-style: none
  margin: 0
  padding: 0
.md-table-head
  text-align: center
</style>
