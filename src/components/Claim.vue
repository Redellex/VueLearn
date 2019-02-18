<template>
  <div class="claimWrapper">
    <h1 class="claim">Galaxy</h1>
    <p class="subclaim">
      Begin your journey through amaxing galaxy,
      discover places you never heard of.
    </p>
    <p class="subclaim">
      Type anything space-related to start
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style scoped>
  .claimWrapper {
    display:flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .claim {
    font-size: 50px;
    margin: 0px;
  }

  .subclaim {
    margin-top: 25px 0 0 0;
    font-size: 13px
  }
</style>
