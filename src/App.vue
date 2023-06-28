<template>
  <div>
    <ContactList
      :contacts="contacts"
      @add="addContact"
      @edit="editContact"
      @remove="removeContact"
    />

    <ContactForm
      v-if="selectedContact"
      :modelValue="selectedContact"
      @save="saveContact"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import ContactList from "./components/ContactList.vue";
import ContactForm from "./components/ContactForm.vue";
import { Contact } from "./types";

export default Vue.extend({
  components: { ContactList, ContactForm },

  data(): { contacts: Contact[]; selectedContact: Contact | null } {
    return {
      contacts: [],
      selectedContact: null,
    };
  },

  methods: {
    addContact() {
      this.selectedContact = { id: "", name: "", phone: "" };
    },

    editContact(contact: Contact) {
      this.selectedContact = { ...contact };
    },

    removeContact(id: string) {
      this.contacts = this.contacts.filter((c) => c.id !== id);
      this.selectedContact = null;
    },

    saveContact(contact: Contact) {
      const index = this.contacts.findIndex((c) => c.id === contact.id);
      if (index >= 0) {
        this.contacts = [
          ...this.contacts.slice(0, index),
          contact,
          ...this.contacts.slice(index + 1),
        ];
      } else {
        this.contacts.push({
          ...contact,
          id: Math.random().toString(36).substring(7),
        });
      }
      this.selectedContact = null;
    },
  },
});
</script>
