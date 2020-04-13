<template>
  <div class="wrapper">
    <HeroImage />
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput" />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import HeroImage from '@/components/HeroImage.vue';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  methods: {
    // eslint-disable-next-line func-names
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    500),
  },
  components: {
    Claim,
    SearchInput,
    HeroImage,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&display=swap');
  $font-weight-light: 300;
  $font-weight-normal: 400;
  $font-weight-bold: 600;
  $font-weight-black: 800;
  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .wrapper {
    margin: 0;
    position: relative;
    width: 100%;
    min-height: 100vh;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>
