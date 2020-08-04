<template>
    <div class="recommend">
        <div v-for="item in recommends" class="recommend-item">
            <a :href="item.link">
                <img :src="item.image">
                <div>{{item.title}}</div>
            </a>
        </div>
    </div>
</template>

<script>
export default {
    name:'HomeRecommendView',
    props:{
        recommends:{
            type:Array,
            default(){
                return []
            }
        }
    }
};
</script>

<style scoped>
    .recommend{
        display: flex;
        width: 100%;
        text-align: center;
        padding: 10px 0 20px; /*上 左右 下  */
        border-bottom: 8px solid #999;
    }
    .recommend-item{
        flex:1;
        font-size: 12px;
    }
    .recommend-item img{
        width: 70px;
        height: 70px;
        margin-bottom:5px ;
    }
</style>
