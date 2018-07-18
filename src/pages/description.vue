<template>
    <div id="description" @touchmove.prevent>
        <!-- 活动描述 -->
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeDescription"></div>
            <div class=title><h2>Cara Ikutan CAPIDUN</h2></div>
            <div class="text">
                <div><p>1.	Dukung negara jagoanmu di setiap pertandingan yang terdapat di halaman utama</p></div>
                <div><p>2.	Untuk mendukung jagoanmu, dibutuhkan sejumlah tabungan Caping minimum Rp {{ruleData.price}}, pastikan kamu memiliki tabungan yang cukup</p></div>
                <div><p>3.	Apabila negara jagoan yang kamu dukung menang, kamu akan mendapatkan reward koin yang berlipat</p></div>
                <div><p>4.	Untuk informasi lebih lanjut, cek halaman syarat & ketentuan</p></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['ruleData'],
    methods:{
        closeDescription(){
            this.$emit('on-close',this.ruleData.count)
        }
    }
}
</script>

<style scoped>
#description{
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
    height: 1000px;
    margin: 80px auto 0;
    background: url("../assets/img/Pop-ups_background.png") no-repeat;
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
h2{
    font-size: 36px;
    font-weight: 800;
    color: #1594c3;
    line-height: 60px
}
.title{
    width: 450px;
    margin: 0 auto;
    padding-top: 50px;
    border-bottom: #1594c3 4px solid
}
.text div{
    width: 480px;
    margin: 60px auto 0
}
.text div p{
    font-size: 32px;
    color: #1594c3;
    text-align:left
}
</style>
