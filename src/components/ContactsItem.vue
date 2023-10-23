<template>
  <div class="contact-container">
    <div class="logo-container">
      <div
        v-if="contactsData.first_name || contactsData.last_name"
        class="logo-name"
      >
        {{ firstLettersName() }}
      </div>
      <div v-else-if="contactsData.emails" class="logo-email">
        {{ firstLettersEmail() }}
      </div>
      <div v-else class="logo-unknown">
        <img src="https://static.thenounproject.com/png/4154905-200.png" />
      </div>
    </div>
    <div class="main-container">
      <h5
        v-if="contactsData.first_name || contactsData.last_name"
        class="contact-name"
      >
        {{ contactsData.first_name }} {{ contactsData.last_name }}
      </h5>
      <a
        v-if="contactsData.emails"
        href="mailto:{{contactsData.emails[0]}}"
        class="contact-email"
      >
        {{ contactsData.emails[0] }}
      </a>
      <div v-else>{{ contactsData.activity_score }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactsItem",
  props: {
    contactsData: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    firstLettersName() {
      if (this.contactsData.first_name && this.contactsData.last_name) {
        return this.contactsData.first_name[0] + this.contactsData.last_name[0];
      } else if (!this.contactsData.last_name) {
        return this.contactsData.first_name.slice(0, 2);
      } else {
        return this.contactsData.last_name.slice(0, 2);
      }
    },
    firstLettersEmail() {
      return this.contactsData.emails[0].slice(0, 2);
    },
  },
};
</script>

<style lang="css" scoped>
a {
  text-decoration: none;
  color: #333;
}
.contact-container {
  display: flex;
  align-items: center;
  gap: 10px;
}
.logo-container {
}
.logo-name {
  background-color: green;
  color: white;
  text-transform: uppercase;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}
.logo-email {
  background-color: red;
  color: white;
  text-transform: uppercase;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}
.logo-unknown {
  background-color: #ccc;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}
.logo-unknown img {
  width: 30px;
}
.main-container {
}
.contact-name {
  margin-top: 0px;
}
.contact-email {
}
</style>