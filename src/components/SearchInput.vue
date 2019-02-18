<template>
  <div class="searchWrapper">
    <Claim/>
    <div class="search">
      <label for="search">Search</label>
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>

<style scoped>
  .searchWrapper{
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px
  }

  label{
    font-family: Montserrat, sans-serif;
  }
  input{
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid black;
  }
</style>
