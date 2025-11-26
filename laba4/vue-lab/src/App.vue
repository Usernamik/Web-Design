<template>
  <div id="app">
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
      <RouterLink to="/contact">Contact</RouterLink>
    </nav>

    <RouterView />
  </div>
</template>

<script setup lang="ts"></script>

<style>
nav {
  display: flex;
  gap: 12px;
  padding: 12px;
}
</style>