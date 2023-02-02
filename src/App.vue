<template>
  <modal-detail
    :isModalActive="isModalActive"
    :changeModalState="changeModalState"
    :post="getContent"
    @editCountFromChild="editCount"
  />

  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{ menu }} test</a>
  </div>
  <section>
    <div
      v-for="(post, i) in posts"
      :key="post.id"
      class="card"
      @click="changeModalState(i)"
    >
      <div class="image">
        <img :src="post.image" />
      </div>
      <div class="description">
        <h4>{{ post.title }}</h4>

        <div class="optional">
          <span>🎀 {{ post.count }}</span>
          <div class="price">
            <span v-if="post.count >= 5" class="badge">인기</span>
            <span>{{ post.price.toLocaleString("ko-KR") }}억</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import data from "./data/post";
import ModalDetail from "./components/ModalDetail.vue";

export default {
  name: "App",
  data() {
    return {
      isModalActive: false,
      activeCard: -1,
      posts: data,
      menus: ["HOME", "SHOP", "ABOUT"],
    };
  },
  methods: {
    editCount() {
      return this.posts[this.activeCard].count++;
    },
    changeModalState(i) {
      this.activeCard = i;
      this.isModalActive = !this.isModalActive;
    },
  },
  computed: {
    getContent() {
      if (this.activeCard < 0 || !this.isModalActive) return;
      return this.posts[this.activeCard];
    },
  },
  components: {
    ModalDetail,
  },
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: rgba(70, 139, 61, 0.87);
  padding: 15px;
  display: grid;
  grid-auto-flow: column;
  justify-content: center;
  grid-gap: 10px;
}

.menu a {
  color: white;
  padding: 10px;
  cursor: pointer;
  border: 2px dashed rgba(255, 255, 255, 0.5);
  border-radius: 5px;
}

.menu a:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.card {
  height: 230px;
  width: 280px;
  border: 1px solid rgba(128, 128, 128, 0.164);
  border-radius: 5px;
  cursor: pointer;
}

.card:hover {
  box-shadow: 5px 5px 3px rgba(102, 102, 102, 0.096);
}

.card img {
  width: 100%;
}
.card > .description {
  margin: 10px 8px;
}

.description h4 {
  text-align: left;
  margin: 0;
  min-height: 40px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; /* 라인수 */
  -webkit-box-orient: vertical;
  word-wrap: break-word;
}

.description > .price {
  text-align: right;
  margin-bottom: 5px;
}

.badge {
  color: red;
  font-size: small;
  vertical-align: top;
  margin-right: 5px;
}

.optional {
  display: flex;
  justify-content: space-between;
}

section {
  padding: 20px 0;
  display: grid;
  justify-content: center;
  grid-gap: 20px;
  grid-template-columns: 280px 280px 280px;
}
</style>
