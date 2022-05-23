<template>
  <div id="app">
    <div class="search-wrapper">
      <input 
      class="search-input" 
      type="text" 
      placeholder="titolo film o parola chiave"
      v-model="searchInput">

      <button 
      class="search-btn"
      @keyup.enter="startSearch">Avvia ricerca</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  },
  data: function() {
    return {
      searchInput: "",
    }
  }
}
</script>

<style lang="scss">

</style>
