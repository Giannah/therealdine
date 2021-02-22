<template>
  <div>
    <div class="blog p-10 m-8">
      <Nuxt />
    </div>
    <Footer />
  </div>
</template>
<style scoped>
html {
  box-sizing: border-box;
}
body {
  min-height: 100%;
  position: relative;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}
@media screen and (min-width: 280px) and (max-width: 414px) {
  .blog {
    padding: 0;
  }
}
</style>
