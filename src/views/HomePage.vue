<template>
  <div id="searchBoard" class="d-flex justify-content-center align-items-center flex-column">
    <h1 id="title">Search</h1>
    <SearchBox/>
  </div>
</template>

<script>
import SearchBox from "@/components/SearchBox";
export default {
  name: "HomePage",
  components: {
    SearchBox,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@media (min-width: 800px) {
  #title {
    font-size: 6rem !important;
  }
}
#searchBoard { 
  background-image: url('@/assets/background.jpg');
  background-size: cover;
  width: 100vw;
  height: 100vh;
}
#title {
  font-size: 4.5rem;
}
</style>
