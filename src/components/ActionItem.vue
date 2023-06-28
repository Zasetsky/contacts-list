<template>
  <td class="contact-item__actions">
    <button @click="editContact" class="action-button edit-button">
      Редактировать
    </button>
    <b>/</b>
    <button @click="removeContact" class="action-button remove-button">
      Удалить
    </button>
  </td>
</template>

<script lang="ts">
import Vue from "vue";
import { Contact } from "../types";

export default Vue.extend({
  props: {
    contact: {
      type: Object as () => Contact,
      required: true,
    },
  },

  methods: {
    editContact() {
      this.$emit("edit", this.contact);
    },

    removeContact() {
      this.$emit("remove", this.contact.id);
    },
  },
});
</script>

<style scoped lang="scss">
.contact-item__actions {
  display: flex;
  justify-content: center;
  align-items: center;

  b {
    font-size: 1.3rem;
  }

  .action-button {
    padding: 0.3125rem 0.625rem;
    border: none;
    color: #fff;
    border-radius: 0.125rem;
    transition: all 0.3s;
    margin: 0 0.3125rem;

    &:first-child {
      background-color: #0066ff;

      &:hover {
        background-color: #0056e0;
      }
    }

    &:last-child {
      background-color: #f44336;

      &:hover {
        background-color: #d32f2f;
      }
    }
  }
}
</style>
