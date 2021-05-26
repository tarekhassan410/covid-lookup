<template>
    <div>
        <div class="logo-area">
            <img src="../assets/images/logo.png" fluid />
        </div>
        <ul class="list-unstyled pl-2 mt-5">
            <li class="d-flex align-items-center text-white">
                <span class="material-icons mr-2">home</span>
                <NuxtLink to="/" class="d-flex align-items-center text-white">   Home </NuxtLink>
            </li>
            <li class="mt-3 d-flex align-items-center text-white">
                <span class="material-icons mr-2"> dashboard </span>
                <NuxtLink to="/dashboard" class="text-white">  Dashboard </NuxtLink>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style>
</style>