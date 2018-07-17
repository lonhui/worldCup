<template>
    <div id="needToKnow">
        <!-- 活动须知 -->
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeNeedToKnow"></div>
            <div class=title><h2>Syarat & Ketentuan CAPIDUN</h2></div>
            <div class="text">
                <div><p>{{text1}}</p></div>
                <div><p>{{text2}}</p></div>
                <div><p>{{text3}}</p></div>
                <div><p>{{text4}}</p></div>
                <div><p>{{text5}}</p></div>
                <div><p>{{text6}}</p></div>
                <div><p>{{text7}}{{ruleData.price}}.</p></div>
                <div><p>{{text8}}</p></div>
                <div><p>{{text9}}</p></div>
                <div><p>{{text10}}</p></div>
                <div><p>{{text11}}</p></div>
                <div><p>{{text12}}</p></div>
                <div><p>{{text13}}</p></div>
                <div><p>{{text14}}</p></div>
                <div><p>{{text15}}</p></div>
                <div><p>{{text16}}</p></div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    props:['ruleData'],
    data(){
        return{
            text1:'1.	Periode event 6-15 Juli 2018',
            text2:'2.	Peserta yang ikutan, wajib menggunakan Caping versi terupdate.',
            text3:'3.	Peserta hanya bisa ikutan apabila sudah login ke akun Caping.',
            text4:'4.	Untuk bisa ikutan kamu harus memiliki tabungan yang cukup (dapatkan tabungan dari poin yang kamu raih melalui aktivitas di Caping. Kamu dapat melihat cara mengumpulkan poin pada halaman FAQ).',
            text5:'5.	Setiap harinya selama periode event berlangsung, kamu dapat memilih negara jagoan yang akan kamu dukung dengan memberikan ‘PIALA’ kepada jagoanmu tersebut.',
            text6:'6.	Kamu dapat mendukung negara jagoanmu dengan memberikan minimal satu PIALA. Semakin banyak PIALA yang kamu kasih, akan semakin besar pula reward yang nanti akan kamu dapatkan.',
            text7:'7.	Satu PIALA setara dengan tabungan Caping Rp ',
            text8:'8.	Pastikan kamu memiliki tabungan Caping yang cukup, karena untuk mendukung negara jagoanmu dengan PIALA, akan membutuhkan tabungan Capingmu.',
            text9:'9.	Kamu bisa memberikan dukungan ke negara jagoanmu sebanyak-banyaknya selama periode voting masih dibuka.',
            text10:'10.	Periode voting akan ditutup ketika pertandingan dimulai.',
            text11:'11.	Kamu bisa melihat daftar riwayat jagoan yang kamu dukung, jumlah dukungan yang kamu beri, dan jumlah reward yang kamu dapat di menu ‘JAGOANKU’. Cek menu ini secara berkala selama periode event berlangsung.',
            text12:'12.	Kamu hanya akan mendapatkan reward tabungan Caping apabila negara jagoan yang kamu dukung menang.',
            text13:'13.	Untuk reward tabungan Caping, tabungan akan secara otomatis ditambahkan ke akun Caping pemenang dalam jangka waktu 2x24 jam.',
            text14:'14.	Peserta yang terbukti melakukan kecurangan dalam mengikuti event ini akan otomatis didiskualifikasi dan akunnya  akan masuk dalam daftar hitam.',
            text15:'15.	Peserta yang mengikuti event ini dianggap telah setuju dengan syarat & ketentuan yang berlaku.',
            text16:'16.	Syarat & ketentuan dapat berubah sewaktu-waktu tanpa pemberitahuan lebih lanjut. Mohon cek halaman syarat & ketentuan ini secara berkala.'
        }
    },
    methods:{
         closeNeedToKnow(){
            this.$emit('on-close')
        }
    }
}
</script>

<style scoped>
#needToKnow{
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
h2{
    font-size: 30px;
    font-weight: 800;
    color: #1594c3;
    line-height: 60px;
}
.title{
    width: 500px;
    margin: 0 auto;
    padding-top: 50px;
    border-bottom: #1594c3 4px solid;
}
.text{
    width: 100%;
    height: 850px;
    margin: 20px auto 0;
    overflow:scroll;
}
.text div{
    width: 550px;
    margin: 20px auto 0;
}
.text p{
    font-size: 28px;
    color: #1594c3;
    text-align:left;
}
</style>
