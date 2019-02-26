<template>
    <div class="searchWrapper">
      <input 
        id="search" 
        name="search" 
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
</template>

<script>  
export default {
    name: 'SearchInput',
}
</script>


<style lang="scss" scoped>
  .searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 300px;


    input {
      height: 30px;
      border-width: 0;
      border-bottom-width: 1px;
      border-bottom-color: rgb(175, 255, 208);
      background: none;
      color: rgb(175, 255, 208);
    }
  }
</style>
