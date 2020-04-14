<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="!loading && step === 1 && results">
      <Item v-for="item in results" :item="item"
            :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
    </div>
    <Loader v-if="loading === true && step === 1" />
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import HeroImage from '@/components/HeroImage.vue';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';
import Loader from '@/components/Loader.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line func-names
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.loading = false;
          this.step = 1;
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
    Item,
    Modal,
    Loader,
  },
  data() {
    return {
      modalItem: null,
      modalOpen: false,
      loading: false,
      step: 0,
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
    &.flexStart {
      justify-content: flex-start;
    }
    .fade-enter-active, .fade-leave-active {
      transition: opacity .5s ease;
    }
    .fade-enter, .fade-leave-to {
      opacity: 0;
    }
    .slide-enter-active, .slide-leave-active {
      transition: margin-top .3s ease;
    }
    .slide-enter, .slide-leave-to {
      margin-top: -15px;
    }
    .logo {
      position: absolute;
      top: 30px;
    }
    .results {
      margin-top: 50px;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 20px;
      @media(min-width: 425px) {
        grid-template-columns: 1fr 1fr;
      }
      @media(min-width: 768px) {
        margin-left: auto;
        margin-right: auto;
        margin-top: 50px;
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
  }
</style>
