<template>
  <footer class="footer border-t-4 border-yellow-400 text-center p-1 w-full">
    <p>
      TheRealDine@2021 - Tous droits réservés<span
        ><fa :icon="['far', 'copyright']" class="ml-0.5 h-2 align-middle"
      /></span>
    </p>
  </footer>
</template>
<style scoped>
@media screen and (min-width: 280px) and (max-width: 414px) {
  .footer {
    position: absolute;
    bottom: 0;
    font-size: 0.75rem;
  }
}
</style>
