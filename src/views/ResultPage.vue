<template>
  <div>
    <header class="d-flex justify-content-center">
      <a id="searchIcon" href="/" class="d-none d-md-block mr-4">Search</a>
      <SearchBox :searchText="text" />
    </header>
    <div id="resultPage" class="container d-flex justify-content-center">
      <div class="row row-cols-1 row-cols-lg-2 p-1 w-100">
        <template v-for="(content, key) in contentList">
          <CarCard
            v-if="content.type == 'car'"
            :key="key"
            :itemKey="key"
            :content="content"
          />
          <PoemCard
            v-if="content.type == 'poem'"
            :key="key"
            :itemKey="key"
            :content="content"
          />
          <BookCard
            v-if="content.type == 'book'"
            :key="key"
            :itemKey="key"
            :content="content"
          />
          <MedicineCard
            v-if="content.type == 'medicine'"
            :key="key"
            :itemKey="key"
            :content="content"
          />
        </template>
      </div>
    </div>
    <div v-if="contentList == null" class="d-flex justify-content-center">
      搜索中，请稍候⋯⋯
    </div>
    <div v-else-if="contentList.length == 0" class="d-flex justify-content-center">
      找不到符合搜寻条件的信息。
    </div>
  </div>
</template>

<script>
import Request from "@/utils/communication";
import SearchBox from "@/components/SearchBox";
import CarCard from "@/components/CarCard";
import BookCard from "@/components/BookCard";
import PoemCard from "@/components/PoemCard";
import MedicineCard from "@/components/MedicineCard";

export default {
  name: "ResultPage",
  components: {
    SearchBox,
    CarCard,
    BookCard,
    PoemCard,
    MedicineCard,
  },
  data() {
    return {
      text: "",
      contentList: [],
    };
  },
  mounted: function () {
    this.contentList = null;
    this.text = this.$route.params.querystring;
    console.log(this.$route.params.querystring);
    Request.query(this.querySucceed, this.getResult, this.text);
  },
  methods: {
    querySucceed(bool) {
      if (!bool) {
        alert("查询失败！");
      }
    },
    getResult(res) {
      this.contentList = res;
      if (res != null) {
        this.contentList = this.contentList
          .filter((content) => content != "")
          .map((content) => JSON.parse(content));
      } else {
        this.contentList = [];
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#searchIcon {
  font-size: 1.8rem;
  font-weight: bold;
  color: black;
  margin: 0 20px;
  text-decoration: none;
}

#resultPage {
  display: flex;
}

header {
  background-image: url("@/assets/background.jpg");
  background-size: cover;
  width: 100vw;
  height: 60px;
  /* display: flex; */
  align-items: center;
  margin: 0;
  padding: 10px;
}
</style>