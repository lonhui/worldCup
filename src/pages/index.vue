<template>
    <div id="index">
        <!-- 主页 -->
        <div class="header"><img src="@/assets/img/CAPIDUN_header.png"></div>
        <div class="button">
            <div class="button1"><img src="@/assets/img/CAPIDUN_button1.png" @click="openDescription"></div>
            <div class="button2"><img src="@/assets/img/CAPIDUN_button2.png" @click="openNeedToKnow"></div>
            <div class="button3"><img src="@/assets/img/CAPIDUN_button3.png" @click="openList"></div>
        </div>
        <div class="content">
            <!-- 1/4半决赛 -->
            <div class="One-fourthFinal">
                <div class="game1">
                    <v-game :data='data1' @on-open="openVote"></v-game>
                </div>
                <div class="game2">
                    <v-game :data='data2' @on-open="openVote"></v-game>
                </div>
                <div class="game3">
                   <v-game :data='data3' @on-open="openVote"></v-game>
                </div>
                <div class="game4">
                    <v-game :data='data4' @on-open="openVote"></v-game>
                </div>
            </div>
            <!-- 半决赛 -->
            <div class="semifinals">
                <div class="game1">
                    <v-game :data='data5' @on-open="openVote"></v-game>
                </div>
                <div class="game2">
                   <v-game :data='data6' @on-open="openVote"></v-game>
                </div>
            </div>
            <!-- 3或4名半决赛框 -->
            <div class="threeOrFourFinals">
                <div class="game1">
                    <v-game :data='data7' @on-open="openVote"></v-game>
                </div>
            </div>
            <!-- 决赛 -->
            <div class="finals">
                <div class="game1">
                    <v-game :data='data8' @on-open="openVote"></v-game>
                </div>
            </div>
        </div>
        <div class="footer">
            <div class="img_trophy"><img src="@/assets/img/1c CAPIDUN (bottom).png"></div>
            <div class="img_logo"><img src="@/assets/img/CAPIDUN_header.png"></div>
        </div>
        <div class="Pop-ups">
            <v-description v-if="descriptionShow" @on-close="closeDescription" :ruleData="ruleData"></v-description>
            <v-needToKnow v-if="needToKnowShow" @on-close="closeNeedToKnow" :ruleData="ruleData"></v-needToKnow>
            <v-vote v-if='voteShow' @on-close="closeVote" :data="idAndPrice"></v-vote>
            <v-list v-if='listShow' @on-close='closeList' :user="user"></v-list>
        </div>
    </div>
</template>

<script>
import description from './description'
import needToKnow from './needToKnow'
import game from './index_game'
import vote from './vote'
import list from './list'


export default {
    data(){
        return{
            descriptionShow:false,
            needToKnowShow:false,
            voteShow:false,
            listShow:false,
            user:{
                uid:null,
                device_id:null,
            },
            idAndPrice:{
                betsPrice:null,
                matchId:null,
                uid:null,
                device_id:null,
                homeImg:null,
                guestImg:null
            },
            data1:{
                time:'21.00 WIB - 6/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1530881400,//2018-07-06 20:50:00
                id:null,
                blackTime:1530655200 //2018-7-4 06:00:00
            },
             data2:{
                time:'01.00 WIB - 7/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1530895800,//2018-07-07 00:50:00
                id:null,
                blackTime:1530655200//2018-7-4 06:00:00
            },
             data3:{
                time:'21.00 WIB - 7/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1530967800,//2018-07-07 20:50:00
                id:null,
                blackTime:1530655200//2018-7-4 06:00:00
            },
             data4:{
                time:'01.00 WIB - 8/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1530982200,//2018-07-08 00:50:00
                id:null,
                blackTime:1530655200//2018-7-4 06:00:00
            },
             data5:{
                time:'01.00 WIB - 11/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1531241400,//2018-07-11 00:50:00
                id:null,
                blackTime:1531000800,//2018-07-08 06:00:00
            },
             data6:{
                time:'01.00 WIB - 12/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1531327800,//2018-07-12 00:50:00
                id:null,
                blackTime:1531000800,//2018-07-08 06:00:00
            },
             data7:{
                time:'21.00 WIB - 14/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1531572600,//2018-07-14 20:50:00
                id:null,
                blackTime:1531346400//2018-07-12 06:00:00
            },
             data8:{
                time:'22.00 WIB - 15/7/2018',
                status:'',
                score:'0:0',
                homeTeam:'',
                homeOdds:'',
                guestTeam:'',
                guestOdds:'',
                homeImg:'',
                guestImg:'',
                endTime:1531662600,//2018-07-15 21:50:00
                id:null,
                blackTime:1531346400//2018-07-12 06:00:00
            },
            datas:[],
            timer:null,
            ruleData:{
                count:0,
                price:null,
            }
            
        }
    },
    mounted(){
        this.getDatas()
        this.getUAndD()
        
        this.getCookie()
        this.setCookie(this.user.uid)

        this.timer = setInterval(()=>{
            this.getDatas()
        },60000)
    },
    components:{
        'v-description':description,
        'v-needToKnow':needToKnow,
        'v-game':game,
        'v-vote':vote,
        'v-list':list
    },
    methods:{
        openList(){this.listShow = true},
        closeList(){this.listShow = false},
        openDescription(){this.descriptionShow = true},
        closeDescription(count){
            if(count === 0){
                this.descriptionShow = false
            }else{
                this.descriptionShow = false
                this.openNeedToKnow()
                this.ruleData.count = 0
            }
            
        },
        openNeedToKnow(){this.needToKnowShow = true},
        closeNeedToKnow(){this.needToKnowShow = false},
        openVote(id,homeImg,guestImg){
            this.idAndPrice.homeImg = homeImg
            this.idAndPrice.guestImg = guestImg
            this.idAndPrice.matchId = id
            this.voteShow = true
        },
        closeVote(){this.voteShow = false},
        getDatas(){
            this.$axios.get('http://campaign.caping.co.id/cup/match')
            .then((res)=>{
                console.log(res)
                for(let i = 0;i < res.data.data.list.length;i++){
                    if(res.data.data.list[i].guestOdds!= null&&res.data.data.list[i].homeOdds!=null){
                        res.data.data.list[i].guestOdds =  Math.floor(res.data.data.list[i].guestOdds*100)/100
                        res.data.data.list[i].homeOdds = Math.floor(res.data.data.list[i].homeOdds*100)/100
                    }
                    if(res.data.data.list[i].homeImg === null){
                        res.data.data.list[i].homeImg = '@/assets/img/round.png'
                    }
                    if(res.data.data.list[i].guestImg === null){
                        res.data.data.list[i].guestImg = '@/assets/img/round.png'
                    }
                }
                this.datas = res.data.data.list
                this.idAndPrice.betsPrice = res.data.data.price
                this.ruleData.price = res.data.data.price
                this.getNewData()
            }).catch(function(error){
                console.log(error)
            })
        },
        getNewData(){
            for(let i = 0;i < this.datas.length;i++){
                if(i === 0){
                    this.data1.homeTeam = this.datas[i].homeTeam
                    this.data1.homeOdds = this.datas[i].homeOdds
                    this.data1.guestTeam = this.datas[i].guestTeam
                    this.data1.guestOdds = this.datas[i].guestOdds
                    this.data1.homeImg = this.datas[i].homeImg
                    this.data1.guestImg = this.datas[i].guestImg
                    this.data1.id = this.datas[i].id
                    this.data1.score = this.datas[i].matchPoint
                }else if(i === 1){
                    this.data2.homeTeam = this.datas[i].homeTeam
                    this.data2.homeOdds = this.datas[i].homeOdds
                    this.data2.guestTeam = this.datas[i].guestTeam
                    this.data2.guestOdds = this.datas[i].guestOdds
                    this.data2.homeImg = this.datas[i].homeImg
                    this.data2.guestImg = this.datas[i].guestImg
                    this.data2.id = this.datas[i].id
                    this.data2.score = this.datas[i].matchPoint
                }else if(i === 2){
                    this.data3.homeTeam = this.datas[i].homeTeam
                    this.data3.homeOdds = this.datas[i].homeOdds
                    this.data3.guestTeam = this.datas[i].guestTeam
                    this.data3.guestOdds = this.datas[i].guestOdds
                    this.data3.homeImg = this.datas[i].homeImg
                    this.data3.guestImg = this.datas[i].guestImg
                    this.data3.id = this.datas[i].id
                    this.data3.score = this.datas[i].matchPoint
                }else if(i === 3){
                    this.data4.homeTeam = this.datas[i].homeTeam
                    this.data4.homeOdds = this.datas[i].homeOdds
                    this.data4.guestTeam = this.datas[i].guestTeam
                    this.data4.guestOdds = this.datas[i].guestOdds
                    this.data4.homeImg = this.datas[i].homeImg
                    this.data4.guestImg = this.datas[i].guestImg
                    this.data4.id = this.datas[i].id
                    this.data4.score = this.datas[i].matchPoint
                }else if(i === 4){
                    this.data5.homeTeam = this.datas[i].homeTeam
                    this.data5.homeOdds = this.datas[i].homeOdds
                    this.data5.guestTeam = this.datas[i].guestTeam
                    this.data5.guestOdds = this.datas[i].guestOdds
                    this.data5.homeImg = this.datas[i].homeImg
                    this.data5.guestImg = this.datas[i].guestImg
                    this.data5.id = this.datas[i].id
                    this.data5.score = this.datas[i].matchPoint
                }else if(i === 5){
                    this.data6.homeTeam = this.datas[i].homeTeam
                    this.data6.homeOdds = this.datas[i].homeOdds
                    this.data6.guestTeam = this.datas[i].guestTeam
                    this.data6.guestOdds = this.datas[i].guestOdds
                    this.data6.homeImg = this.datas[i].homeImg
                    this.data6.guestImg = this.datas[i].guestImg
                    this.data6.id = this.datas[i].id
                    this.data6.score = this.datas[i].matchPoint
                }else if(i === 6){
                    this.data7.homeTeam = this.datas[i].homeTeam
                    this.data7.homeOdds = this.datas[i].homeOdds
                    this.data7.guestTeam = this.datas[i].guestTeam
                    this.data7.guestOdds = this.datas[i].guestOdds
                    this.data7.homeImg = this.datas[i].homeImg
                    this.data7.guestImg = this.datas[i].guestImg
                    this.data7.id = this.datas[i].id
                    this.data7.score = this.datas[i].matchPoint
                }else if(i === 7){
                    this.data8.homeTeam = this.datas[i].homeTeam
                    this.data8.homeOdds = this.datas[i].homeOdds
                    this.data8.guestTeam = this.datas[i].guestTeam
                    this.data8.guestOdds = this.datas[i].guestOdds
                    this.data8.homeImg = this.datas[i].homeImg
                    this.data8.guestImg = this.datas[i].guestImg
                    this.data8.id = this.datas[i].id
                    this.data8.score = this.datas[i].matchPoint
                }
            }
        },
        getUAndD(){
            const url = window.location.href
            let a = url.indexOf('?')//得到？的下标
            if(a>=0){
                let b = url.substring(a+1)//得到？后面的字符串
                let e = b.lastIndexOf('&')//得到最后一个&的下标
                let c = b.indexOf('u=')//得到u=的下标
                if(c>=0){
                    if(c<e){
                        let uid = b.substring(c).substring(2,b.substring(c).indexOf('&'))
                        this.user.uid = uid
                    }else{
                        let uid = b.substring(c+2)
                        this.user.uid = uid
                    }
                }
                let d = b.indexOf('c=')//得到d=的下标
                if(d>=0){
                    if(d<e){
                        let device_id = b.substring(d).substring(2,b.substring(d).indexOf('&'))
                        this.user.device_id = device_id
                    }else{
                        let device_id = b.substring(d+2)
                        this.user.device_id = device_id
                    }
                }
            }
            this.idAndPrice.uid = this.user.uid
            this.idAndPrice.device_id = this.user.device_id
            
        },
        //设置cookie
        setCookie(uid,exdays){
            var exdate = new Date();//获取时间
            exdate.setTime(exdate.getTime()+24*60*60*1000*exdays)//保存天数
            window.document.cookie="uid"+ "=" +uid+";path=/;expires="+exdate.toGMTString();
        },
        //读取cookie
         getCookie() {
            if (document.cookie.length>0) {
                var arr=document.cookie.split('; ');//这里显示的格式需要切割一下自己可输出看下
                for(var i=0;i<arr.length;i++){
                    var arr2=arr[i].split('=');//再次切割
                    var aa = 0
                    //判断查找相对应的值
                    if(arr2[0]==='uid'){
                        aa = aa + 1
                        if(this.user.uid != arr2[1]){
                            this.ruleData.count = 1
                            this.openDescription()
                        }
                    }
                }
                if(aa === 0){
                    this.ruleData.count = 1
                    this.openDescription()
                }
            }else{
                this.ruleData.count = 1
                this.openDescription()
            }
            
        },
        //清除cookie
        clearCookie:function () {
            this.setCookie("","","","",-1);
        }
    }
}
</script>

<style scoped>
#index{
    width: 748px;
    height: 1330px;
    margin: 0 auto;
    overflow:scroll;
    background: url("../assets/img/CAPIDUN_background.png") no-repeat;
    background-size: 100% 100%;
    background-size:cover
}

.header{
    width: 530px;
    height: 185px;
    margin: 75px auto 0
}
.header img{
    width: 100%;
    height: 100%
}
.button{
    width: 670px;
    height: 50px;
    margin: 30px auto 0
}
.button .button1{
    width: 210px;
    height: 40px;
    float: left
}
.button .button2{
    width: 210px;
    height: 40px;
    float: left;
    margin-left: 20px
}
.button .button3{
    width: 210px;
    height: 40px;
    float: left;
    margin-left: 20px
}
.button img{
    width: 100%;
    height: 100%
}
/* 1/4半决赛框 */
.One-fourthFinal{
    width: 650px;
    height: 1560px;
    margin: 20px auto 0;
    background: url("../assets/img/One-fourthFinal_background.png") no-repeat;
    background-size: 100% 100%;
    overflow: hidden
}
.game1{
    margin-top: 85px
}

/* 半决赛框 */
.semifinals{
    width: 650px;
    height: 825px;
    margin: 20px auto 0;
    background: url("../assets/img/semifinals_background.png") no-repeat;
    background-size: 100% 100%;
    overflow: hidden
}
/* 3或4名半决赛框 */
.threeOrFourFinals{
    width: 650px;
    height: 455px;
    margin: 20px auto 0;
    background: url("../assets/img/threeOrFourFinals_background.png") no-repeat;
    background-size: 100% 100%;
    overflow: hidden
}
/* 决赛 */
.finals{
    width: 650px;
    height: 455px;
    margin: 20px auto 0;
    background: url("../assets/img/finals_background.png") no-repeat;
    background-size: 100% 100%;
    overflow: hidden;
    position: relative
}
.img_trophy{
    width: 100%;
    height: 300px;
    margin-top: 40px
}
.img_trophy img{
    width: 100%;
    height: 100%
}
.img_logo{
    width: 400px;
    height: 120px;
    margin: 20px auto 50px
   
}
.img_logo img{
    width: 100%;
    height: 100%
}
.footer{
    padding-bottom: 80px
}
</style>
