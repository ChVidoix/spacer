<template>
  <input
    id="search"
    name="search"
    :value="value"
    @input="handleChange"
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
</style>
