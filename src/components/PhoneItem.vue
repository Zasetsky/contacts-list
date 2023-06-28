<template>
  <td class="contact-item__phone">{{ phone }}</td>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    phone: {
      type: String,
      required: true,
    },
  },
});
</script>
