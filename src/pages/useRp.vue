<template>
    <div id="userRp" @touchmove.prevent>
        <!-- 您确定要使用Rp 下注吗？ -->
        <div class="content">
            <div class="text">
                <p>Apakah kamu yakin ingin menggunakan tabungan Rp {{RpNum}} untuk mendukung jagoanmu?</p>
            </div>
            <div class="button">
                <div class="yes"><img src="@/assets/img/button_ya.png" @click="closeUseRpAndVote"></div>
                <div class="no"><img src="@/assets/img/button_tidak.png" @click="closeUseRp"></div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    props:['RpNum'],
    methods:{
        closeUseRp(){
            this.$emit('on-close',0)
        },
        closeUseRpAndVote(){
            this.$emit('on-close',1)
        }
    }
}
</script>

<style scoped>
#userRp{
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
    height: 600px;
    margin: 300px auto 0;
    background: url("../assets/img/useRp_background.png") no-repeat;
    background-size: 100% 100%;
    position: relative;
}
.end{
    width: 70px;
    height: 70px;
    position: absolute;
    left: 550px;
    top: -20px;
}
.end img{
    width: 100%;
    height: 100%;
}
.text p{
    width: 500px;
    margin: 0 auto;
    color: #e13333;
    font-size: 44px;
    font-weight: 600;
    padding-top: 80px;
}
.button{
    width: 500px;
    height: 65px;
    margin: 120px auto 0;
}
.yes{
    width: 220px;
    height: 65px;
    float: left;
}
.no{
    width: 220px;
    height: 65px;
    float: right;
}
.yes img,.no img{
    width: 100%;
    height: 100%;
}
</style>
