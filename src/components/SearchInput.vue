<template>
  <input
    id="search"
    name="search"
    :value="value"
    :class="{ dark }"
    @input="handleChange"
    autocomplete="off"
  />
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
  input {
    display: flex;
    margin-top: 50px;
    flex-direction: column;
    width: 250px;
    color: white;
    font-size: 18px;
    font-weight: 300;
    text-align: center;
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid white;
    transition: box-shadow .5s;
    @media (min-width: 1024px) {
      font-weight: 400;
    }
  }
  input:focus {
    outline: none;
    box-shadow: 0 10px 10px -10px white;
  }
  .dark {
    color: #1e3d4a;
    border-bottom-color: #1e3d4a;
  }
  .dark:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
  }
</style>
