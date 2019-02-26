<template>
  <div class="wrapper">
    <BackgroundImage />
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import BackgroundImage from '@/components/BackgroundImage.vue';
const API = 'https://images-api.nasa.gov';

export default {
  name: 'search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
      .then((response) => {
        this.results = response.data.collection.items;
        console.log(response);
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
  }
</style>

