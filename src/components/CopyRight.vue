<template>
  <p class="copyright">
    This game is a test for me to start learning Vue3 -
    <a href="https://3-d-portfolio-nine-delta.vercel.app/" target="_blank">contact me</a>
  </p>
</template>

<script setup lang="ts"></script>

<style scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
