<template>
    <div class="nav-bar">
        <div class="left1"><slot name="left"></slot></div>
        <div class="center"><slot name="center"></slot></div>
        <div class="right1"><slot name="right"></slot></div>
    </div>
</template>

<script>
export default {
    name:"NavBar"
};
</script>

<style scoped>
    .nav-bar{
        display: flex;
        height: 44px;
        line-height: 44px;
        text-align: center;
        box-shadow: 0 1px 1px rgba(100,100,100,0.1);
    }
    .left1, .right1{
        width: 60px;

    }
    .center{
        flex:1;

    }

</style>
