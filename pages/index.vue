<template>
  <div class="container mt-5 text-center">
        <img class="travel" src="../assets/images/MYTIGATE-Logo.svg" />
        <h1 class="mt-5">Covid tracker</h1>
        <p> Find covid information, statistics and the safer countries  </p>
        <NuxtLink to="/dashboard"> <button class="btn btn-primary">  Discover </button> </NuxtLink>
    
  </div>
</template>

<script>
export default {}
</script>

<style scoped>

@media screen and (min-width: 768px) {

.travel{
  width: 50%;
  height: auto;
}
}
</style>
