<template>
  <button class="btn" :class="color" @click="$emit('action')">
    <slot />
  </button>
</template>

<script>
export default {
  emits: ["action"],
  props: {
    color: {
      type: String,
      default: '',
      validator(value) {
        ['', "primary", "danger"].includes(value);
      },
    },
  },
  methods: {
    btnLog(){
      console.log('Btn log')
    }
  }
};
</script>

<style scoped></style>
