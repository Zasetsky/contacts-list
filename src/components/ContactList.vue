<template>
  <div class="contact-list">
    <table class="contact-list__table text-center">
      <thead>
        <tr>
          <th>Имя</th>
          <th>Телефон</th>
          <th>Действия</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts" :key="index">
          <NameItem :name="contact.name" />
          <PhoneItem :phone="contact.phone" />
          <ActionItem :contact="contact" @edit="edit" @remove="remove" />
        </tr>
      </tbody>
    </table>
    <button @click="add" class="add-button">Добавить контакт</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import NameItem from "./NameItem.vue";
import PhoneItem from "./PhoneItem.vue";
import ActionItem from "./ActionItem.vue";
import { Contact } from "../types";

export default Vue.extend({
  components: { NameItem, PhoneItem, ActionItem },

  props: {
    contacts: {
      type: Array as () => Contact[],
      required: true,
    },
  },

  methods: {
    add() {
      this.$emit("add");
    },

    edit(contact: Contact) {
      this.$emit("edit", contact);
    },

    remove(id: string) {
      this.$emit("remove", id);
    },
  },
});
</script>

<style scoped lang="scss">
.contact-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 3.125rem;

  &__table {
    width: 60%;
    border-collapse: collapse;
    box-shadow: 0px 0px 1.25rem rgba(0, 0, 0, 0.1);
    border-radius: 0.625rem;
    overflow: hidden;

    th,
    td {
      border: 0.0625rem solid #ddd;
      padding: 0.625rem;
      text-align: left;
    }

    th {
      background-color: #4caf50;
      color: #fff;
    }

    tr:nth-child(even) {
      background-color: #f2f2f2;
    }

    th:nth-of-type(1) {
      width: 30%;
    }

    th:nth-of-type(2) {
      width: 40%;
    }

    th:nth-of-type(3) {
      width: 30%;
    }
  }

  .add-button {
    margin-top: 1.25rem;
    padding: 0.625rem 1.25rem;
    border: none;
    color: #fff;
    border-radius: 0.25rem;
    transition: all 0.3s;
    background-color: #4caf50;

    &:hover {
      background-color: #45a049;
    }
  }
}
</style>
