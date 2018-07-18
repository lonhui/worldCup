<template>
    <div id="vote" @touchmove.prevent>
        <!-- 投票窗口 -->
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeVote"></div>
            <div class="text">
                <div class="header">
                    <h2>PILIH JAGOANMU</h2>
                    <p>DENGAN CARA KLIK BENDERA</p>
                </div>
                <div class="team">
                    <div class="home">
                        <img :src="this.data.homeImg" class="flag" @click="upbollHome">
                        <img src="@/assets/img/footboll.png" class="boll" v-show="matchTarget===1">
                    </div>
                    <div class="vs"><p>VS</p></div>
                    <div class="Visiting">
                        <img :src="this.data.guestImg" @click="upbollVisiting">
                        <img src="@/assets/img/footboll.png" class="boll" v-show="matchTarget===-1">
                    </div>
                </div>
                <div class="t"><h3>MASUKKAN JUMLAH DUKUNGAN</h3></div>
                <div class="num">
                    <div class="trophy"><img src="@/assets/img/Trophy.png"></div>
                    <div class="input">
                        <p class="Less" @click="lessCount">-</p>
                        <input type="number" onkeyup="this.value=this.value.replace(/\D/g,'')" onafterpaste="this.value=this.value.replace(/\D/g,'')" v-model="count">
                        <p class="add" @click="addCount">+</p>
                    </div>
                </div>
                <div class="Rp">
                    <p>Rp {{RpNum}}</p>
                </div>
                <div class="button">
                    <img src="@/assets/img/button_SUBMIT.png" v-if="!buttonShow">
                    <img src="@/assets/img/button_vote_.png" @click="getParameter" v-if="buttonShow">
                </div>
            </div>
        </div>
        <div class="Pop-ups">
            <v-useRp v-if="useRpShow" @on-close="closeUseRp" :RpNum="RpNum"></v-useRp>
            <v-yeay v-if="yeayShow" @on-close="closeYeay"></v-yeay>
            <v-insufficientPoints v-if="insufficientPointsShow" @on-close="closeInsufficientPoints"></v-insufficientPoints>
            <v-networkError v-if="networkErrorShow" @on-close="closeNetworkError"></v-networkError>
            <v-loginPrompt v-if="loginPromptShow" @on-close="closeLoginPrompt"></v-loginPrompt>
            <v-userNotExist v-if="userNotExistShow" @on-close="closeUserNotExist"></v-userNotExist>
            <v-beyondBettingTime v-if="beyondBettingTimeShow" @on-close="closeBeyondBettingTime"></v-beyondBettingTime>
        </div>
    </div>
</template>

<script>
import useRp from './useRp'
import yeay from './yeay'
import insufficientPoints from './insufficientPoints'
import networkError from './networkError'
import loginPrompt from './loginPrompt'
import userNotExist from './userNotExist'
import beyondBettingTime from './beyondBettingTime'

export default {
    data(){
        return{
            count:0,
            RpNum:0,
            matchTarget:null,//选择队伍
            buttonShow:false,
            useRpShow:false,//使用Rp提示框
            yeayShow:false,//投注成功
            insufficientPointsShow:false,//积分不足提示框
            networkErrorShow:false,//网络错误
            loginPromptShow:false,//未登录提示
            userNotExistShow:false,//用户不存在
            beyondBettingTimeShow:false//超出下注时间
        }
    },
    props:['data'],
    components:{
        'v-useRp':useRp,
        'v-yeay':yeay,
        'v-insufficientPoints':insufficientPoints,
        'v-networkError':networkError,
        'v-loginPrompt':loginPrompt,
        'v-userNotExist':userNotExist,
        'v-beyondBettingTime':beyondBettingTime
    },
    methods:{
        closeVote(){
            this.$emit('on-close')
        },
        openUseRp(){this.useRpShow = true},
        closeUseRp(num){
            if(num===1){
                this.useRpShow = false
                this.vote()
            }else{
                this.useRpShow = false
            }
        },
        openYeay(){this.yeayShow = true},
        closeYeay(){
            this.yeayShow = false
            this.closeVote()
        },
        openInsufficientPoints(){this.insufficientPointsShow = true},
        closeInsufficientPoints(){this.insufficientPointsShow = false},
        openNetworkError(){this.networkErrorShow = true},
        closeNetworkError(){this.networkErrorShow = false},
        openLoginPrompt(){this.loginPromptShow = true},
        closeLoginPrompt(){this.loginPromptShow = false},
        openUserNotExist(){this.userNotExistShow = true},
        closeUserNotExist(){this.userNotExistShow = false},
        openBeyondBettingTime(){this.beyondBettingTimeShow = true},
        closeBeyondBettingTime(){this.beyondBettingTimeShow = false},
        addCount(){
            if(this.count < 100){
                this.count = Number(this.count) + 1
            }   
        },
        lessCount(){
            if(this.count>0){
                this.count = Number(this.count) - 1
            }
        },
        upbollHome(){
            this.matchTarget = 1
        },
        upbollVisiting(){
            this.matchTarget = -1
        },
        //得到参数
        getParameter(){
            if(this.data.uid===null||this.data.device_id===null){
                    this.openLoginPrompt()//提示用户未登录
            }else{
                this.openUseRp()
            }
        },
        getImg(){
            if(this.data.homeImg===null){
                this.data.homeImg = '@/assets/img/Home team.png'
            }
            if(this.data.guestImg===null){
                this.data.guestImg = '@/assets/img/Visiting team.png'
            }
        },
        //下注
        vote(){
            this.$axios.post('http://campaign.caping.co.id/cup/bets',{
                uid:Number(this.data.uid),   //从地址栏获取
                betsTimes:this.count,      //interface_1返回
                betsPrice:this.data.betsPrice, //interface_1返回
                matchTarget:this.matchTarget,     //1 主队  -1 客队  0 平 由用户选择输入
                matchId:this.data.matchId,
                deviceId:this.data.device_id+'' //从地址栏获取
            },{ headers: {
                'Content-Type':'application/json'
            }},)
            .then((res)=>{
                console.log(res)
                if(res.data.code === 0){
                    this.openYeay()
                }else if(res.data.code === 306){
                    this.openInsufficientPoints()
                }else if(res.data.code === 605){
                    this.openBeyondBettingTime()
                }else if(res.data.code === 301){
                    this.openLoginPrompt()
                }
            }).catch((error)=>{
                console.log(error)
                this.openNetworkError()
            })
        },
    },
    watch:{
        'matchTarget':function(){
            if(this.matchTarget!=null&&this.count>0){
                this.buttonShow = true
            }else{
                this.buttonShow = false
            }
        },
        'count':function(){
            if(this.matchTarget!=null&&this.count>0){
                this.buttonShow = true
            }else{
               this.buttonShow = false 
            }
            this.RpNum = this.data.betsPrice * Number(this.count)
            if(this.count>100){
                this.count = 100
            }
        }
    }
}
</script>

<style scoped>
#vote{
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
    height: 850px;
    margin: 200px auto 0;
    background: url("../assets/img/vote_background.png") no-repeat;
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
.header{
    width: 600px
}
.header h2{
    color: #fff;
    font-size: 38px;
    font-weight: 600;
    padding-top: 60px
}
.header p{
    color: #fff;
    font-size: 26px;
    margin-top: 5px
}
.team{
    width: 500px;
    height: 200px;
    margin: 50px auto 0
}
.team .home{
    width: 180px;
    height: 200px;
    float: left;
    position: relative
}
.team .home .flag{
    width: 100%;
    height: 100%;
}
.team .home .boll{
    width: 100px;
    height: 100px;
    position: absolute;
    left: 110px;
    top: 110px
}
.team .vs{
    width: 130px;
    height: 200px;
    float: left
}
.team .vs p{
    color: #fff;
    font-size: 60px;
    font-weight: 800;
    margin-top: 50px
} 
.team .Visiting{
    width: 180px;
    height: 200px;
    float: right;
    position: relative
}
.team .Visiting .boll{
    width: 100px;
    height: 100px;
    position: absolute;
    left: 110px;
    top: 110px
}
.team .Visiting img{
    width: 100%;
    height: 100%
}
.t{
    width: 500px;
    margin:50px auto 0
}
.t h3{
    color: #fff;
    font-size: 30px;
    font-weight: 700
}
.num{
    width: 500px;
    height: 120px;
    margin: 40px auto 0
}
.num .trophy{
    width: 90px;
    height: 120px;
    float: left;
    margin-left: 30px
}
.num .trophy img{
    width: 100%;
    height: 100%
}
.num .input{
    width: 330px;
    height: 120px;
    float: right
}
.num .input input{
    color: #b60000;
    width: 140px;
    height: 50px;
    margin-top: 30px;
    border: 0px;
    float: left;
    margin-left: 10px;
    background: url("../assets/img/input_background.png") no-repeat;
    background-size: 100% 100%;
    position: relative;
    text-align: center;
    font-size: 30px;
    font-weight: 600
}
.num .input .Less{
    color: #fff;
    font-size: 80px;
    width: 70px;
    float: left
}
.num .input .add{
    color: #fff;
    font-size: 60px;
    width: 70px;
    float: left;
    margin-top: 20px;
    margin-left: 10px
}
.button{
    width: 250px;
    height: 70px;
    margin: 50px auto 0
}
.button img{
    width: 100%;
    height: 100%
}
.Rp{
    width: 150px;
    float: right;
    color: #fff;
    font-size: 30px;
    margin-right: 50px
    
}
</style>
