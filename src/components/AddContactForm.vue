<template>
  <div>
    <add-contact-item @open="openForm" />
    <div v-if="contactForm" class="contact-form">
      <div>
        <label>
          Введіть ім'я контакту
          <input type="text" v-model="newContactFirstName" />
        </label>
      </div>
      <div>
        <label>
          Введіть призвіще контакту
          <input type="text" v-model="newContactLastName" />
        </label>
      </div>
      <div>
        <label>
          Введіть імейл контакту
          <input type="email" v-model="newContactEmail" />
        </label>
      </div>
      <button @click="addContact">Додати контакт</button>
      <button @click="cancelContactAdding">Відмінити</button>
      <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
    </div>
  </div>
</template>

<script>
import AddContactItem from "./AddContactItem.vue";
export default {
  name: "AddContactForm",
  components: { AddContactItem },
  data() {
    return {
      contactForm: false,
      newContactFirstName: null,
      newContactLastName: null,
      newContactEmail: null,
      errorMessage: null,
    };
  },
  methods: {
    openForm() {
      this.contactForm = true;
    },
    cancelContactAdding() {
      this.contactForm = false;
    },
    addContact() {
      if (
        (this.newContactFirstName || this.newContactLastName) &&
        this.newContactEmail
      ) {
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.newContactEmail)) {
          return (this.errorMessage =
            "Мусить бути Email, а не звичайний текст");
        }
        this.$emit("add", {
          first_name: this.newContactFirstName,
          last_name: this.newContactLastName,
          emails: [this.newContactEmail],
          activity_score: Number.parseInt(
            Math.random().toString().slice(2, 17)
          ),
        });

        this.newContactFirstName = null;
        this.newContactLastName = null;
        this.newContactEmail = null;
        this.contactForm = false;
        this.errorMessage = null;
      } else {
        this.errorMessage = "Заповніть принаймні одне поле та поле Email";
      }
    },
  },
};
</script>

<style lang="css" scoped>
.error-message {
  color: red;
}
</style>