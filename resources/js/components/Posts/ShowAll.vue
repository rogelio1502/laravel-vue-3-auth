<template>
  <div>
    <div
      v-if="posts.length > 0"
      class="row d-flex justify-content-center"
    >
      <div class="col-12 text-center">
        <h3>Posts Publicados</h3>
      </div>
      <div class="col-12">
        <ul
          v-for="post in posts"
          :key="post.id"
        >
          <li>
            <div class="card">
              <div class="card-body">
                <h3 class="card-title">
                  <a
                    href="#"
                    class="card-link"
                  >{{post.title}}</a>

                </h3>
                <p class="fs-6">
                  Publicado el {{format(post.created_at).date}} a las {{format(post.created_at).hour}}
                </p>

                <p class="card-text fs-4">
                  {{post.description}}
                </p>
                <div v-if="userId == post.created_by">
                  <Btn
                    :btnTxt="'Eliminar'"
                    :btnAction="removePost"
                    :btnType="'remove'"
                  ></Btn>

                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div
      v-else
      class="text-center"
    >
      <p class="fs-2 text">No hay ningún post publicado aún</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import Btn from "../Forms/Btn.vue";
export default {
  components: {
    Btn,
  },
  data() {
    return {
      posts: [],
      userId: null,
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    format(date) {
      return {
        date: moment(date).format("MM/DD/YYYY"),
        hour: moment(date).format("hh:ss A"),
      };
    },
    getPosts() {
      axios
        .get("/api/posts")
        .then((r) => {
          this.posts = [];
          this.posts = r.data.posts;
          this.userId = r.data.userId;
        })
        .catch((e) => {});
    },
    removePost() {},
  },
};
</script>

<style>
li {
  list-style: none;
}
a {
  text-decoration: none;
}
</style>
