<template>
  <div class="hello">
    <div>
      <h2>{{ msg }}</h2>
    </div>
    <div class="row">
      <div class="column">
        <div class="pad20 mar-l-2 left-content">
          <table>
            <tr>
              <th>Id</th>
              <th>Title</th>
              <th>UserId</th>
              <th></th>
            </tr>
            <tr>
              <td colspan="4"><hr /></td>
            </tr>
            <tr v-for="postData in postDatas.posts" :key="postData.id">
              <td>{{ postData.id }}</td>
              <td class="left">{{ postData.title }}</td>
              <td>{{ postData.userId }}</td>
              <td>
                <button @click="userComments(postData.id)">Details</button>
              </td>
            </tr>
          </table>
        </div>
      </div>
      <div class="column">
        <div class="row left">
          <div class="column">
            <h3 v-if="postId">Post id: {{ postId }}</h3>
          </div>
          <div class="column">
            <h3 v-if="totalCount">
              Total comments for this post : {{ totalCount }}
            </h3>
          </div>
          <div class="pad20 mar-l-2 bottom-content">
            <u v-if="postId"><b>Comments</b></u>
            <ul>
              <li v-for="comments in allComments" :key="comments.id">
                {{ comments.body }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "BlogPosts",
  props: ["msg"],
  data() {
    return {
      postDatas: "",
      postId: "",
      allComments: [],
      totalCount: "",
    };
  },
  mounted() {
    this.getPostData();
  },
  methods: {
    async getPostData() {
      await axios
        .get("https://dummyjson.com/posts")
        .then((response) => {
          console.log(response);
          this.postDatas = response.data;
        })
        .catch((error) => {
          return error;
        });
    },
    async userComments(id) {
      this.postId = id;
      const commentsUrl = "https://dummyjson.com/posts/" + id + "/comments";
      await axios
        .get(commentsUrl)
        .then((response) => {
          this.totalCount = response.data.comments.length;
          this.allComments = response.data.comments;
        })
        .catch((error) => {
          return error;
        });
    },
  },
};
</script>

<style scoped>
.left-content {
  max-height: 450px;
  overflow: scroll;
}
.pad20 {
  padding-top: 20px;
}
.mar-l-2 {
  margin-left: 20px;
}
.left {
  text-align: left;
  padding-left: 20px;
}
.bottom-content {
  padding-right: 20px;
  float: left;
  text-align: left;
  width: 100%;
}
.column {
  float: left;
  width: 50%;
}
/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
</style>
