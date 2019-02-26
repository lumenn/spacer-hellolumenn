<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="fade">
      <BackgroundImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
    </div>
    <div class="lds-ellipsis" v-if="step === 1 && loading"><div></div><div></div><div></div><div></div></div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import BackgroundImage from '@/components/BackgroundImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'search',
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
    handleInput: debounce(function() {
      this.loading = true;
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
      .then((response) => {
        this.results = response.data.collection.items;
        //console.log(response);
        this.loading = false;
        this.step = 1;
      })
      .catch((error) => {
        console.log(error);
      });
    }, 500),
  },
  components: {
    Claim,
    SearchInput,
    BackgroundImage,
    Item,
    Modal,
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    min-height: 100vh;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    &.flexStart {
      justify-content: flex-start;
    }
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .results {
    margin-top: 25px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    @media (min-width: 768px){
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

.lds-ellipsis {
  margin-top: 50px;
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
  
  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
.lds-ellipsis div {
  position: absolute;
  top: 27px;
  width: 11px;
  height: 11px;
  border-radius: 50%;
  background: #000;
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

</style>

