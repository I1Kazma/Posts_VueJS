<template>
  <form @submit.prevent>
    <my-input v-focus type="text" placeholder="Название" v-model:modelValue="post.title" />
    <my-input type="text" placeholder="Описание" v-model:modelValue="post.body" />
    <my-button @click="createPost" class="btn">Добавить пост</my-button>
  </form>
</template>

<script>

export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now(),
        this.$emit('create', this.post),
        this.post = {
          title: '',
          body: '',

        }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 500px;
  padding: 20px;
}
</style>