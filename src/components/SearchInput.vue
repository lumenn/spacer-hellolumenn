<template>
    <input 
        id="search" 
        name="search"
        :class="{ dark }"
        :value="value"
        @input="handleChange"
    />
</template>

<script>  
export default {
    name: 'SearchInput',
    props:{
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
}
</script>


<style lang="scss" scoped>
    input {
      margin-top: 50px;
      display: flex;
      width: 300px;   
      font-family: 'Quicksand', sans-serif;
      font-weight: 400;
      text-align: center;
      font-size: 1.5rem;
      height: 30px;
      border-width: 0;
      border-bottom-width: 1px;
      border-bottom-color: rgb(175, 255, 208);
      background: none;
      color: rgb(175, 255, 208);
      transition: box-shadow .5s;
        @media (min-width: 768px) {
            height: 3rem;
            font-size: 2rem;
        }
    }
    input:focus{
        outline: none;
        box-shadow: 0 5px 15px -8px rgba(175, 255, 208, .7);
    }

    .dark {
        color: black;
        border-bottom-color: black;
        //box-shadow: 0 5px 15px -8px rgba(0, 0, 0);
    }
    .dark:focus {
        color: black;
        box-shadow: 0 5px 15px -8px rgba(0, 0, 0, .7);
    }
</style>
