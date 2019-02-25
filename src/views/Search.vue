<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input 
        id="search" 
        name="search" 
        v-model="searchValue"
        @input="handleInput"
      />
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
            <p>{{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
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
};
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 300px;

    label {
      font-family: Tahoma, sans-serif;
    }

    input {
      height: 30px;
      border-width: 0;
      border-bottom-width: 1px;
      border-bottom-color: black;
    }
  }
</style>

