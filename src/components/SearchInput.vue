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
    value:{
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods:{
    handleChange(e){
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style scoped>
  label{
    font-family: Montserrat, sans-serif;
  }
  input{
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;
    color: white;
    text-align: center;
    font-size: 18px;
    font-weight: 300;
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid white;
    trainsition: box-shadow .3s ease-out;
  }

  input:focus {
    outline: none;
    box-shadow: 0 5px 10px -10px rgba(255,255,255,.3);
  }

  .dark {
    color: #1e3d4a;
    border-bottom-color: #1e3d4a;
  }

  .dark:focus{
    box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
  }
</style>
