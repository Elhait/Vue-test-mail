<template>
  <div class="modal-backdrop">
    <div class="modal">
      <header class="modal-header">
        <slot name="header">
          <button type="button" class="btn-close" @click="close">
            x
          </button>
        </slot>
      </header>
      <section class="modal-body">
        <slot name="body">
          <form @submit.prevent="onSubmit">
            <md-field>
              <label>Title</label>
              <md-input v-model="title"></md-input>
              <span class="md-helper-text">Example: White forest</span>
            </md-field>
            <md-field>
              <label>Recipient</label>
              <md-input v-model="recipient" autocomplete="email"></md-input>
              <span class="md-helper-text">Example: example@gmail.com</span>
            </md-field>
            <md-field>
              <label>Textarea</label>
              <md-textarea v-model="textarea" class="textarea"></md-textarea>
            </md-field>
            <md-button class="md-raised md-primary" type="submit">
              Submit and save
            </md-button>
          </form>
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

<script>
export default {
  name: "modalFrom",
  data() {
    return { mails: [], title: "", recipient: "", textarea: "" };
  },
  methods: {
    close() {
      this.$emit("close");
    },
    sendMails() {
      const parsed = JSON.stringify(this.mails);
      localStorage.setItem("mails", parsed);
    },
    onSubmit() {
      if (!this.title) {
        return;
      }
      const newMail = {
        id: Date.now(),
        title: this.title,
        recipient: this.recipient,
        textarea: this.textarea
      };
      this.mails.push(newMail);
      this.$emit("add-mail", newMail);
      this.title = "";
      this.recipient = "";
      this.textarea = "";
      this.sendMails();
    }
  }
};
</script>

<style>
form {
  display: grid;
  grid-template-rows: auto auto;
  grid-row-gap: 10px;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  /* width: 90%; */
  max-width: 700px;
  width: 600px;
  margin: 20px auto;
}

.modal-header,
.modal-footer {
  padding: 5px;
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  justify-content: space-between;
}

.modal-header {
  border-bottom: 1px solid #eeeeee;
  padding: 20px;
  color: #4aae9b;
  justify-content: center;
  position: relative;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  position: absolute;
  right: 0px;
  padding: 20px;
  border: none;
  font-size: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>
