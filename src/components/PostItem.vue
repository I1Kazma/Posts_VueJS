<template>
    <div class="post">
        <div>
            <div>{{ post.id }}</div>
            <div>Название:{{ post.title }}</div>
            <div>Описание: {{ post.body }}</div>
        </div>
        <div class="post_btns">
            <my-button @click="$router.push(`/posts/${post.id}`)" style="margin-right:30px;"> Открыть </my-button>
            <my-button @click="$emit('remove', post)"> Удалить </my-button>
        </div>


    </div>
</template >

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true,
        }
    },
    methods: {

    }
}
</script>

<style>
.post {
    border: 2px solid green;
    margin: 15px;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.post_btns {
    display: flex;
}
</style>
                        