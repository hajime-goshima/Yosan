<template>
  <div id="app">
    <at-menu mode="horizontal" active-name="1">
      <at-menu-item name="1" to="/"><i class="icon icon-home"></i>Home</at-menu-item>
      <at-menu-item name="2" to="/about"><i class="icon icon-help-circle"></i>Abount</at-menu-item>
    </at-menu>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
