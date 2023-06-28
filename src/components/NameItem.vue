<template>
  <td class="contact-item__name">{{ name }}</td>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    name: {
      type: String,
      required: true,
    },
  },
});
</script>
