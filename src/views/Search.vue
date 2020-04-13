<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
  },
  data() {
    return {
      results: [],
    };
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    justify-content: center;
    padding: 30px;
    width: 100%;
    height: 100vh;
    background-image: url('../assets/heroimage.jpg');
    background-size: cover;
    background-position: 80% 0%;
  }
</style>
