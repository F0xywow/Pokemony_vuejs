<script setup>
import { RouterLink, RouterView } from 'vue-router'
import pikachuIcon from '@/assets/pikachu.png'

</script>

<template>
  <header>
    <div class="navbar">
      <div class="navbar-left">
        <img :src="pikachuIcon" alt="zmiana" />
      </div>
      <div class="navbar-right">
        <div class="wrapper">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </div>
      </div>
    </div>
  </header>
  <div id="content">
    <RouterView />
  </div>
</template>

<style scoped>
.navbar {
  position: fixed;
  z-index: 200;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 70px;
  background-color: aquamarine;
}

.navbar-left {
  margin-left: 20px;
}

.wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  height: 100%;
  padding-right: 20px;
}

.wrapper a {
  margin-left: 20px;
}
</style>
