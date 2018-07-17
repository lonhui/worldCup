<template>
    <div id="game">
        <!-- 比赛场次情况 -->
        <div class="game">
            <div class="time"><p>{{data.time}}</p></div>
            <div class="score">
                <div class="left">
                    <div class="round">
                        <p class="teamName">{{data.homeTeam}}</p>
                        <img :src="data.homeImg" class="round_left">
                        <p class="odds">×{{data.homeOdds}}</p>
                    </div>
                    <div class="White"><img src="@/assets/img/White strip.png" class="White_left"></div>
                    <div class="num"><p>{{this.score[0]}}</p></div>
                </div>
                <div class="VS"><p>VS</p></div>
                <div class="right">
                    <div class="num"><p>{{this.score[1]}}</p></div>
                    <div class="White"><img src="@/assets/img/White strip.png" class="White_right"></div>
                    <div class="round">
                        <p class="teamName">{{data.guestTeam}}</p>
                        <img :src="data.guestImg" class="round_right">
                        <p class="odds">×{{data.guestOdds}}</p>
                    </div>
                </div>
            </div>
            <div class="button_game1"><img src="@/assets/img/button_game.png" v-if="buttonShow" @click="openVote"></div>
            <div class="status"><p>{{status}}</p></div>
            <div class="black" v-if="blackShow"></div>
        </div> 
    </div>
    
</template>

<script>
export default {
    data(){
        return{
            score:[],
            buttonShow:true,
            status:'',
            timer:null,
            blackShow:false,
        }
    },
    props:['data'],
    mounted(){
        this.getScore()
        this.timer = setInterval(()=>{
            this.getScore()
        },1000)
        this.time()
        this.closeBlack()
    },
    methods:{
        getScore(){
            this.score = this.data.score.split(':')
        },
        openVote(){
            this.$emit('on-open',this.data.id,this.data.homeImg,this.data.guestImg)
        },
        //倒计时s
        time(){
            this.timer = setInterval(()=>{
                var leftTime = this.data.endTime - (new Date())/1000    //获取时间戳差（结束时间-当前时间），单位秒
                if(leftTime > 0){
                    var d = parseInt(leftTime / 60 / 60 / 24 , 10)  //获得天数
                    var h = parseInt(leftTime / 60 / 60 % 24 , 10)  //获得小时
                    var m = parseInt(leftTime / 60 % 60, 10)    //获得分钟
                    var s = parseInt(leftTime % 60, 10)     //获得秒钟
                    //将天数转换为小时显示（需求绝定）
                    if(d > 0){
                        h = d * 24 + h
                    }
                    //格式化时分秒
                    if(h < 10){
                        h = '0' + h
                    }
                    if(m < 10){
                        m = '0' + m
                    }
                    if(s < 10){
                        s = '0' + s
                    }
                    
                    this.status = 'SISA WAKTU VOTING | ' + h + ':' + m + ':' + s    //倒计时格式  时：分：秒
                }else{
                    //倒计时结束后显示
                    this.buttonShow = false
                    this.status = 'VOTING SUDAH DITUTUP'    
                }
            },1000) //每秒执行一次，实现秒钟倒数
        },
        closeBlack(){
            const bt = this.data.blackTime*1000-(new Date())
            if(bt>0){
                this.blackShow = true
            }
        }
    }
}
</script>

<style scoped>
.game{
    width: 600px;
    height: 350px;
    margin: 20px auto 0;
    background: url("../assets/img/White_background.png") no-repeat;
    background-size: 100% 100%;
    overflow: hidden;
}
#game{
    position: relative;
}
.black{
    width: 600px;
    height: 350px;
    position: absolute;
    top: 0px;
    background: rgba(7, 17, 27, 0.5);
    border-radius:28px 25px 25px 27px;
}
.time{
    width: 300px;
    font-size: 28px;
    margin: 20px auto 0;
    background-color: #fff;
    border-radius:10px 10px 10px 10px;
}
.score{
    width: 550px;
    height: 80px;
    margin: 50px auto 0;
}
.status{
    width: 500px;
    height: 20px;
    margin: 20px auto 0;
    font-size: 28px;
    color: #fff;
}
/* game1样式 */
.button_game1{
    width: 220px;
    height: 60px;
    margin: 40px auto 0;
}
.button_game1 img{
    width: 100%;
    height: 100%;
}
/* 左 */
.game .score .left{
    width: 225px;
    height: 80px;
    float: left;
    position: relative;
}
.game .score .VS{
    width: 100px;
    height: 80px;
    font-size: 60px;
    color: #fff;
    float: left;
}
.game .score .VS p{
    text-align: center;
    margin-top: 10px;
}
.game .score .left .round{
    position: relative;
}
.game .score .left .round .teamName{
    color:  #fff;
    width: 200px;
    position: absolute;
    left: 15px;
    top: -35px;
}
.game .score .left .round .odds{
    color:  #fff;
    width: 100px;
    position: absolute;
    left: 55px;
    top: 90px;
}
.game .score .left .round img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 0;
    top: 0;
}
.game .score .left .num{
    width: 80px;
    height: 80px;
    background-color: #fff;
    float: right;
    border-radius:30px 30px 30px 30px;
    position: absolute;
    left: 145px;
    top: 0;
}
.game .score .left .White img{
    width: 90px;
    height: 40px;
    margin: 20px auto 0;
}
/* 右 */
.game .score .right{
    width: 225px;
    height: 80px;
    float: left;
    position: relative;
}
.game .score .right .White img{
    width: 90px;
    height: 40px;
    margin: 20px auto 0;
}
.game .score .right .num{
    width: 80px;
    height: 80px;
    background-color: #fff;
    float: right;
    border-radius:30px 30px 30px 30px;
    position: absolute;
    left: 0;
    top: 0;
}
.game .score .right .round img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 145px;
    top: 0;
}
.num p{
    font-size: 46px;
    font-weight: 600;
    margin-top: 10px;
    text-align: center;
    color: #3b882b;
}
.game .score .right .round{
    position: relative;
    top: -65px;
}
.game .score .right .round .teamName{
    color: #ffffff;
    width: 200px;
    position: absolute;
    right: 10px;
    top: -35px;
}
.game .score .right .round .odds{
    color: #fff;
    width: 100px;
    position: absolute;
    right: 60px;
    top: 90px;
}
</style>


