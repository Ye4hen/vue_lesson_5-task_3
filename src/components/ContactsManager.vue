<template>
  <div class="contacts-container">
    <search-contact-form @clear="clearFilter" @search="searchContacts" />
    <div class="error-message" v-if="searchErrorMessage">
      {{ searchErrorMessage }}
    </div>
    <add-contact-form @add="addContact" />
    <contacts-item
      v-for="(contact, index) in contactsList"
      :key="index"
      :contactsData="contact"
    />
  </div>
</template>

<script>
import AddContactForm from "./AddContactForm.vue";
import ContactsItem from "./ContactsItem.vue";
import SearchContactForm from "./SearchContactForm.vue";
export default {
  name: "ContactsManager",
  components: {
    ContactsItem,
    AddContactForm,
    SearchContactForm,
  },
  props: {
    contactsList: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      searchErrorMessage: null,
    };
  },
  methods: {
    addContact(newContact) {
      const updatedContacts = [...this.contactsList];
      updatedContacts.push(newContact);

      this.$emit("add", updatedContacts);
    },
    searchContacts(searchText) {
      if (!searchText) {
        return (this.searchErrorMessage =
          "Введіть текст перед тим, як натискати кнопку пошуку");
      } else {
        const searchParam = searchText.toLowerCase();
        const filteredList = this.contactsList.filter((contact) => {
          return (
            (contact.first_name &&
              contact.first_name.toLowerCase().includes(searchParam)) ||
            (contact.last_name &&
              contact.last_name.toLowerCase().includes(searchParam)) ||
            (contact.emails &&
              contact.emails.some((email) =>
                email.toLowerCase().includes(searchParam)
              )) ||
            (contact.first_name + " " + contact.last_name)
              .toLowerCase()
              .includes(searchParam) ||
            (contact.activity_score &&
              contact.activity_score.toString().includes(searchParam))
          );
          //   searchText = null;
        });
        this.$emit("searchContact", filteredList);
      }
    },
    clearFilter() {
      this.$emit("clear", this.contactsList);
    },
  },
};
</script>

<style lang="css" scoped>
.contacts-container {
  display: grid;
  gap: 30px;
  justify-content: center;
}
.error-message {
  color: red;
  font-size: 12px;
  margin-top: -15px;
}
</style>