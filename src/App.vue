<template>
  <div>
    <contacts-manager
      :contactsList="contacts"
      @add="updateContacts"
      @searchContact="handleSearch"
      @clear="clearFilter"
    />
  </div>
</template>

<script>
import ContactsManager from "./components/ContactsManager.vue";
import { contacts } from "./constants/7_data_contacts";
export default {
  name: "App",
  components: { ContactsManager },
  data() {
    return {
      contacts,
    };
  },
  computed: {
    // handleSearch() {},
  },
  methods: {
    updateContacts(updatedContacts) {
      this.contacts = updatedContacts;
    },
    handleSearch(filteredList) {
      this.contacts = filteredList;
    },
    clearFilter() {
      this.contacts = contacts;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
