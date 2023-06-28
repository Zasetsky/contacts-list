<template>
  <div v-if="open" class="contact-form" @click="handleClickOutside">
    <div class="contact-form__dialog" @click.stop>
      <h1>Контакт</h1>
      <div class="contact-form__fields">
        <input v-model="contact.name" placeholder="Имя" />
        <input
          v-model="contact.phone"
          placeholder="Телефон"
          @keypress="isNumber($event)"
        />
      </div>
      <div class="contact-form__buttons">
        <button @click.stop="save">Сохранить</button>
        <button @click.stop="close">Отменить</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Contact } from "../types";

export default Vue.extend({
  props: {
    modelValue: {
      type: Object as () => Contact | null,
      default: null,
    },
  },

  data() {
    return {
      contact: { ...(this.modelValue || {}) },
      open: this.modelValue !== null,
    };
  },

  watch: {
    modelValue(value) {
      this.contact = value ? { ...value } : {};
      this.open = value !== null;
    },
  },

  methods: {
    close() {
      this.$emit("update:modelValue", null);
      this.open = false;
    },

    save() {
      if (this.contact && this.contact.name && this.contact.phone) {
        this.$emit("save", { ...this.contact });
        this.close();
      }
    },

    handleClickOutside(event: MouseEvent) {
      if (event.target === event.currentTarget) {
        this.close();
      }
    },

    isNumber(event: KeyboardEvent) {
      const char = event.key;
      const isNumberChar = char >= "0" && char <= "9";

      if (!isNumberChar) {
        event.preventDefault();
      }
    },
  },
});
</script>

<style lang="scss" scoped>
.contact-form {
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 10%;
  background: rgba(0, 0, 0, 0.5);
  overflow-y: auto;

  &__dialog {
    background: #fff;
    padding: 1.25rem;
    box-shadow: 0px 0px 0.625rem rgba(0, 0, 0, 0.1);
    width: 18.75rem;
    display: flex;
    flex-direction: column;
    align-items: center;

    h1 {
      color: #0066ff;
    }
  }

  &__fields {
    margin-bottom: 1.25rem;
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;

    input {
      width: 80%;
      padding: 0.5rem;
      border: 0.0625rem solid #ccc;
      border-radius: 0.25rem;
      margin-bottom: 0.625rem;
      background-color: #f3f3f3;
      transition: all 0.3s;

      &:hover,
      &:focus {
        border-color: #0066ff;
        background-color: #e6e6e6;
      }
    }
  }

  &__buttons {
    display: flex;
    justify-content: space-between;
    width: 100%;

    button {
      padding: 0.5rem 1rem;
      border: none;
      color: #fff;
      border-radius: 0.25rem;
      transition: all 0.3s;
      margin-right: 1rem;

      &:first-child {
        background-color: #4caf50;

        &:hover {
          background-color: #45a049;
        }
      }

      &:last-child {
        background-color: #f44336;

        &:hover {
          background-color: #d32f2f;
        }
      }

      &:last-of-type {
        margin-right: 0;
      }
    }
  }
}
</style>
