<template>
  <div id="add-post"></div>
  <div>
    <div
      class="mb-5"
      v-show="showNewPostForm"
    >
      <AddPost
        @newPost="(msg) => reload = msg"
        @hideForm="(msg) => showNewPostForm = false"
      ></AddPost>
    </div>
    <div>
      <ShowAll ref="showAllChild"></ShowAll>
    </div>

    <div id="foo">
      <a
        @click="() => {showNewPostForm = true}"
        href="#new-post"
      >New Post</a>
    </div>
  </div>
</template>

<script>
import AddPost from "./AddForm.vue";
import ShowAll from "./ShowAll.vue";

export default {
  components: {
    AddPost,
    ShowAll,
  },
  data() {
    return {
      reload: "",
      showNewPostForm: false,
    };
  },
  watch: {
    reload(newV, oldV) {
      if (newV == "reload") {
        this.$refs.showAllChild.getPosts();
        this.showNewPostForm = false;
        this.reload = "";
      }
    },
  },
};
</script>

<style>
#foo {
  position: fixed;
  bottom: 0;
  right: 0;
  background-color: black;
  height: 50px;
  width: 50px;
  margin-right: 5px;
  margin-bottom: 5px;
  padding-left: 10px;
  padding-top: 2px;
}
</style>
