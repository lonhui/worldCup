<template>
    <!-- Yeay！ 你设法支持你的英雄。 在“JAGOANKU”页面上查看您的状态。 -->
    <div id="yeay" @touchmove.prevent>
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeYeay"></div>
            <p class="p1">Yeay!</p>
            <p class="p2">Kamu berhasil</p>
            <p class="p3">mendukung jagoanmu.</p>
            <p class="p4">Cek statusmu</p>
            <p class="p5">di halaman ‘JAGOANKU’.</p>
        </div>
    </div>
</template>

<script>
export default {
    methods:{
        closeYeay(){
            this.$emit('on-close')
        }
    }
}
</script>

<style scoped>
#yeay{
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
   padding-top: 80px
}
.p2,.p3{
    font-size: 32px;
    font-weight: 600
}
.p4{
    margin-top: 50px;
    font-size: 32px;
    font-weight: 600
}
.p5{
    font-size: 32px;
    font-weight: 600
}
p{
    color: #e13333
}
</style>
