<template>
    <div class="navbar">
        <div @click="$router.push('/')">Vue 3</div>
        <div class="navbar__btns">
            <my-button @click="$router.push('/posts')">Посты</my-button>
            <my-button style="margin-left:30px;" @click="$router.push('/about')"> О приложении</my-button>
            <my-button style="margin-left:30px;" @click="$router.push('/store')"> Store</my-button>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.navbar {
    height: 75px;
    background-color: teal;
    box-shadow: 2px 2px 4px gray;
    display: Flex;
    align-items: center;
    padding: 0 15px;
}

.navbar__btns {
    margin-left: auto;
}
</style>