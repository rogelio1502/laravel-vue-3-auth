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

    <div id="new-post-footer">
      <a
        id="show-new-post-form"
        @click="() => {
            showAddForm()
            }"
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
  methods: {
    showAddForm() {
      let posTop = document.getElementById("add-post").offsetTop; //Get the position of the element you want to scroll to
      window.scrollTo(posTop, 0);
      this.showNewPostForm = true;
    },
  },
};
</script>

<style>
#new-post-footer {
  position: fixed;
  bottom: 0;
  right: 0;
  background-color: black;
  height: 50px;
  width: 50px;
  margin-right: 20px;
  margin-bottom: 15px;
  padding-left: 10px;
  padding-top: 2px;
}
#show-new-post-form {
  color: white;
  cursor: pointer;
}
</style>
