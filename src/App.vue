<template>
  <div class="app">
    <h1>Posts page</h1>
    <my-input v-model="searchQuery" placeholder="Search"></my-input>
    <div class="app__btns">
      <my-button @click="showDialog">Create post</my-button>
      <div class="sort">
        <p>Sort posts:</p>
        <my-select v-model="selectedSort" :options="sortOptions" />
      </div>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list
      v-if="!isPostsLoading || page > 1"
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
    />
    <div v-else>Loading...</div>
    <h2 v-if="!isPostsLoading && posts.length === 0" style="color: red">
      Posts not fount
    </h2>
    <div
      v-show="!isPostsLoading && posts.length > 0"
      ref="observer"
      class="observer"
    ></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import { Post } from "@/typings";

enum SortType {
  title = "title",
  body = "body",
  id = "id",
}

export default defineComponent({
  name: "app",
  components: {
    PostForm,
    PostList,
  },
  data: () => {
    return {
      posts: [] as Post[],
      title: "",
      body: "",
      dialogVisible: false,
      isPostsLoading: true,
      selectedSort: SortType.id,
      searchQuery: "",
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        { value: SortType.id, name: "By id" },
        { value: SortType.title, name: "By title" },
        { value: SortType.body, name: "By body" },
      ],
    };
  },
  methods: {
    createPost(post: Post): void {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post: Post): void {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog(): void {
      this.dialogVisible = true;
    },
    async fetchPosts(): Promise<void> {
      try {
        this.isPostsLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _page: this.page,
              _limit: this.limit,
            },
          }
        );
        this.totalPages = Math.ceil(
          (response.headers["x-total-count"]
            ? parseInt(response.headers["x-total-count"])
            : 0) / this.limit
        );
        this.page === 0
          ? (this.posts = response.data)
          : (this.posts = [...this.posts, ...response.data]);
      } catch (e) {
        alert(e);
      } finally {
        this.isPostsLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
    const options = {
      rootMargin: "0px",
      threshold: 1.0,
    };
    const callback = (
      entries: IntersectionObserverEntry[],
      observer: IntersectionObserver
    ): void => {
      if (entries[0].isIntersecting && this.page < this.totalPages) {
        this.page++;
        console.log(this.page);
      }
    };
    const observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer as Element);
  },
  computed: {
    sortedPosts(): Post[] {
      return [...this.posts].sort((post1, post2) =>
        this.selectedSort !== "id"
          ? post1[this.selectedSort].localeCompare(post2[this.selectedSort])
          : post1[this.selectedSort] - post2[this.selectedSort]
      );
    },
    sortedAndSearchedPosts(): Post[] {
      return this.sortedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  watch: {
    page: function () {
      this.fetchPosts();
    },
  },
});
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.sort {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 15px;
}
</style>
