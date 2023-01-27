<template>
  <div class="black-bg" v-if="isModalActive">
    <div class="white-bg">
      <div class="modal-header">
        <h4>상세페이지</h4>
        <button @click="changeModalState">X</button>
      </div>
      <div class="modal-detail">
        <img :src="post.image" />
        <p>{{ post.title }}</p>
        <p>{{ post.content }}</p>
        <button @click="handleAddFavorite">Add Favorite</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalDetail",
  props: {
    isModalActive: { type: Boolean, default: false },
    changeModalState: { type: Function },
    post: { type: Object, default: null },
  },
  methods: {
    handleAddFavorite() {
      this.$emit("editCountFromChild");
    },
  },
};
</script>

<style scoped>
.black-bg {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  display: flex;
}
.white-bg {
  width: 500px;
  background-color: white;
  border-radius: 8px;
  margin: auto;
}

.modal-header {
  display: flex;
  width: 100%;
  padding: 20px 20px 15px 20px;
  border-bottom: 1px solid rgba(128, 128, 128, 0.164);
  justify-content: space-between;
}

.modal-header h4 {
  margin: 0;
}
.modal-detail {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 300px;
  padding: 20px 20px;
}

.modal-detail p:first-of-type {
  font-weight: bold;
}
.modal-detail p:last-of-type {
  margin-top: 0;
}

.modal-detail > img {
  width: 100%;
  border-radius: 4px;
}
</style>
