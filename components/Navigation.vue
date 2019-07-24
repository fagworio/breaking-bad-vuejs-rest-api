<template>
  <section class="is-primary is-bold">
    <!-- Hero header: will stick at the top -->
    <div class="hero-head">
      <nav class="navbar">
        <div class="navbar-brand">
          <nuxt-link class="navbar-item" to="/">
            <img src="breaking-bad.png" class="logo" alt="Logo" />
          </nuxt-link>
          <div class="navbar-burger" @click="showNav = !showNav" :class="{ 'is-active': showNav }">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </div>
        <div class="navbar-menu" :class="{ 'is-active': showNav }">
          <div class="navbar-end">
            <nuxt-link class="navbar-item" to="/">Personagens</nuxt-link>
            <nuxt-link class="navbar-item" to="/episodios">Episódio</nuxt-link>
            <nuxt-link class="navbar-item" to="/sugestao">Sugestão</nuxt-link>
          </div>
        </div>
      </nav>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      showNav: false
    };
  }
};
</script>
<style scoped>
.navbar-item img {
  max-height: 4rem !important;
}
.navbar-burger {
  height: 5rem !important;
  width: 5rem !important;
}
</style>

