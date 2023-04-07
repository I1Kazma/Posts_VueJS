/*Разметка*/
<template>
    <div>
        <h1 style="padding-left:20px;">Страница с постами</h1>
        <my-input v-focus type="text" v-model="searchQuery" placeholder="Поиск...." />

        <div class="app__btns">
            <my-button @click="showDialog">Добавить пост</my-button>
            <my-select v-model="selectedSort" :options="sortOptions" />
        </div>

        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost" />
        </my-dialog>

        <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading" />

        <div v-else style="padding-left:20px;">
            Идет загрузка...
        </div>
        <div class="observer" v-intersection="loadMorePosts"></div>

    <!-- <div class="page__wrapper">
      <div v-for="pageNumber in totalPages" :key="pageNumber" class="page"
        :class="{ 'current-page': page === pageNumber }" @click="changePage(pageNumber)">
        {{ pageNumber }}</div>
                                                                                                  </div>-->
    </div>
</template>

/*Логика*/
<script>
import PostForm from '@/components/PostForm.vue'
import PostList from '@/components/PostList.vue'
import MySelect from '@/components/UI/MySelect.vue'
import MyButton from '@/components/UI/MyButton.vue'
import MyDialog from '@/components/UI/MyDialog.vue'
import MyInput from '@/components/UI/MyInput.vue'
import axios from 'axios'
export default {
    components: {
        PostList, PostForm, MyDialog,
        MyButton, MySelect, MyInput,
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOptions: [
                { value: 'title', name: ' По названию' },
                { value: 'body', name: ' По описанию' },
            ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },

        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },

        showDialog() {
            this.dialogVisible = true;
        },

        //changePage(pageNumber) {
        //   this.page = pageNumber;
        // },

        async fetchPosts() {
            try {
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = response.data;
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostsLoading = false;
            }
        },

        async loadMorePosts() {
            try {
                this.page += 1;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                this.posts = [...this.posts, ...response.data];
            } catch (e) {
                alert('Ошибка')
            }
        }

    },
    mounted() {
        this.fetchPosts();
        // let options = {
        //     rootMargin: "0px",
        //     threshold: 1.0,
        // };

        // const callback = (entries, observer) => {
        //     if (entries[0].isIntersecting && this.page < this.totalPages) {
        //         this.loadMorePosts()
        //     }
        // };

        // let observer = new IntersectionObserver(callback, options);

        // observer.observe(this.$refs.observer)
    },

    computed: {

        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
            })
        },

        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },

    watch: {
        // page() {
        //   this.fetchPosts();
        // }
    }
}


</script>

/*Стиль*/
<style>
* {
    margin: 0;
    padding: 0;
}

.app__btns {
    margin-left: 20px;
    display: flex;
    justify-content: space-between;
}

.page__wrapper {
    display: flex;
    margin-top: 15px;
}

.page {
    border: 1px solid black;
    padding: 5px;

}

.current-page {
    border: 1px solid green;
    color: green;
}

.observer {
    height: 30px;

}
</style>
