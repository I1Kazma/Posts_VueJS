<template>
    <button>
        <slot></slot>
    </button>
</template>

<script>
export default{
    name:'my-button',
}
</script>

<style scoped>
button{
    width:150px;
    height:50px;
    border:1px solid green;
    color:green;
    background-color:white;
  }
</style>