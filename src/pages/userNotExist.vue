<template>
    <!-- 该用户不存在 -->
    <div id="userNotExist" @touchmove.prevent>
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeUserNotExist"></div>
            <p class="p1">Maaf,  </p>
            <p class="p2">pengguna tidak ada,</p>
            <p class="p3">silakan masuk lagi.</p>
        </div>
    </div>
</template>

<script>
export default {
    methods:{
        closeUserNotExist(){
            this.$emit('on-close')
        }
    }
}
</script>

<style scoped>
#userNotExist{
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
    position: relative
}
.end{
    width: 70px;
    height: 70px;
    position: absolute;
    left: 550px;
    top: -20px
}
.end img{
    width: 100%;
    height: 100%
}
.p1{
   font-size: 50px;
   font-weight: 600;
   padding-top: 120px
}
.p2,.p3{
    font-size: 32px;
    font-weight: 600
}
p{
    color: #e13333
}
</style>
