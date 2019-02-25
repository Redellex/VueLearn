<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">    </transition>
     <img src="./assets/logo.png" class="logo" v-if="step === 1"/>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results"
            :item="item"  :key="item.data[0].nasa_id"
            @click.native="handleModalOpen(item)"/>
    </div>
    <div class="lds-ellipsis" v-if="step ===1 && loading"/>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'App',
  components: {
    HeroImage,
    Claim,
    SearchInput,
    Item,
    Modal,
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

  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>
<style lang="scss" scoped>

  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,800,800');
  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: 'Montserrat',sans-serif;
    margin: 0;
    padding: 0;
  }

  .wrapper{
    display: flex;
    min-height: 100vh;
    flex-direction: column;
    align-items: center;
    margin: 0;
    position: relative;
    padding: 30px;
    height: 100vh;
    width: 100%;
    justify-content: center;

    &.flexStart {
      justify-content: flex-start;
    }

    .fade-enter-active, .fade-leave-active{
      transition: opacity .3s ease;
    }

    .fade-enter, .fade-leave-to{
      opacity: 0;
    }
  }

  .logo {
    position: absolute;
    top: 30px;
    height: 50px;
    width: 50px;
  }

  .slide-enter-active, .fade-leave-active{
    transition: margin-top .3s ease;
  }

  .slide-enter, .fade-leave-to{
    margin-top: -50px;
  }

  .lds-ellipsis {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
  }
  .lds-ellipsis div {
    position: absolute;
    top: 27px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: #fff;
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
  }
  .lds-ellipsis div:nth-child(1) {
    left: 6px;
    animation: lds-ellipsis1 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(2) {
    left: 6px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(3) {
    left: 26px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(4) {
    left: 45px;
    animation: lds-ellipsis3 0.6s infinite;
  }
  @keyframes lds-ellipsis1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes lds-ellipsis3 {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }
  @keyframes lds-ellipsis2 {
    0% {
      transform: translate(0, 0);
    }
    100% {
      transform: translate(19px, 0);
    }
  }


  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;


    @media(min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
