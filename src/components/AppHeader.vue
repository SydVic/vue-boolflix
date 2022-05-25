<template>
  <section class="header">
    <div class="logo">
      boolflix
    </div>
    <!-- WRAPPER DELLA RICERCA -->
    <div class="search-wrapper">
      <input 
      class="search-input" 
      type="text" 
      placeholder="titolo o parola chiave"
      v-model="searchInput">

      <button 
      class="search-btn"
      @click="$emit('modifiedInput', searchInput)"
      >Premi per avviare la ricerca</button>
    </div>
    <!-- /WRAPPER DELLA RICERCA -->
  </section>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchInput: "",
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.header {
  height: $header-height;
  background-color: rgb(36, 35, 35);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;

  .logo {
    color: red;
    text-transform: uppercase;
    font-size: 2rem;
    font-weight: bolder;
  }

  .search-input {
    padding: .3rem .3rem;
    margin-right: .3rem;
    border-radius: 5px;
  }

  .search-btn {
    padding: .3rem .3rem;
    border-radius: 5px;
  }
}
</style>