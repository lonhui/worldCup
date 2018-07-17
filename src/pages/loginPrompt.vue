<template>
    <!-- 提示未登录 -->
    <div id="loginPrompt" @touchmove.prevent>
        <div class="content">
            <p class="p1">Maaf,</p>
            <p class="p2">kamu harus</p>
            <p class="p3">login dahulu untuk ikutan.</p>
            <div class="button"><img src="@/assets/img/button k.png" @click="closeLoginPrompt"></div>
        </div>
    </div>
</template>

<script>
export default {
    methods:{
        closeLoginPrompt(){
            this.$emit('on-close')
        }
    }
}
</script>

<style scoped>
#loginPrompt{
    position: fixed;
    z-index: 100;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(7, 17, 27, 0.8)
}
.content{
    width: 600px;
    height: 450px;
    margin: 400px auto 0;
    background: url("../assets/img/yeay_background.png") no-repeat;
    background-size: 100% 100%;
    position: relative;
}
.p1{
   font-size: 50px;
   font-weight: 600;
   padding-top: 80px; 
}
.p2,.p3{
    margin-top: 10px;
    font-size: 32px;
    font-weight: 600;
}
p{
    color: #e13333;
}
.button{
    width: 200px;
    height: 60px;
    margin: 100px auto 0;
}
.button img{
    width: 100%;
    height: 100%;
}
</style>
