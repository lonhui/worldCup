<template>
    <div id="list">
        <!-- 下注状态列表 -->
        <div class="content">
            <div class="end"><img src="@/assets/img/button_end.png" @click="closeList"></div>
            <div class="title"><h2>DAFTAR JAGOANKU</h2></div>
            <div class="header">
                <table>
                    <tr>
                        <td>Waktu</td>
                        <td>Jagoan</td>
                        <td>Dukungan</td>
                        <td>Reward</td>
                    </tr>
                </table>
            </div>
            <div class="text">
                 <table>
                    <tr v-for="item in list" :key="item.index">
                        <td class="td"><div class="p p1"><p>{{item.waktu}}</p></div></td>
                        <td class="td"><div class="p p2"><p>{{item.jagoan}}</p></div></td>
                        <td class="td">
                            <div class="img">
                                <div class="p p3"><p class="pp">{{item.dukungan}}</p></div>
                                <div class="td_img"><img src='@/assets/img/Trophy.png'></div>
                            </div>
                        </td>
                        <td><div class="p p4"><p>{{item.reward}}</p></div></td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['user'],
    data(){
        return{
            list:[
               
            ]
        }
    },
    mounted(){
        this.getList()
    },
    methods:{
        closeList(){
            this.$emit('on-close')
        },
        getList(){
            this.$axios.post('http://campaign.caping.co.id/cup/bets/'+this.user.uid+'?pageNum='+1+'&pageSize='+100)
            .then((res)=>{
                this.list=[]
                console.log(res)
                for(let i = 0;i < res.data.data.data.length;i++){
                    const list={
                        waktu:null,
                        jagoan:null,
                        dukungan:null,
                        reward:null
                    }
                    list.waktu = res.data.data.data[i].createTime
                    const team = res.data.data.data[i].matchName.split(' vs ')
                    if(res.data.data.data[i].matchTarget===1){
                        list.jagoan = team[0]
                    }else{
                        list.jagoan = team[1]
                    }
                    list.dukungan = res.data.data.data[i].betsTimes
                    if(res.data.data.data[i].matchResult!=0){
                        //比赛结束
                        if(res.data.data.data[i].matchResult === 1){
                            //中奖
                            list.reward = '+Rp ' + res.data.data.data[i].betsWinMoney
                        }else{
                            //未中奖
                            list.reward = '+Rp 0'
                        }
                    }else{
                        //比赛未结束
                        list.reward = ''
                    }
                    this.list.push(list)
                }
                //this.list = res.data.data.data
            }).catch(function(error){
                console.log(error)
            })
        }
    }
}
</script>

<style scoped>
#list{
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
    margin: 150px auto 0;
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
    color: #1594c3;
    font-size: 40px;
    font-weight: 800;
    padding-top: 50px
}
.header{
    color: #1594c3;
    font-size: 30px;
    width: 550px;
    margin: 20px auto 0;
    border: #1594c3 2px solid;
    border-radius:30px 30px 30px 30px
}
.header table{
    width: 550px;
    margin: 0 auto;
    text-align: center
}
.header table td{
    width: 135px
}
.text{
    color: #1594c3;
    font-size: 24px;
    line-height: 30px;
    width: 550px;
    height: 780px;
    margin: 20px auto 0;
    overflow:scroll

}
.text table{
    width: 550px;
    margin: 0 auto;
    text-align: center
}
.text table .td{
    width: 135px;
    height: 100px;
    border-right: #1594c3 4px solid
} 
.text table td .p{
    margin-top:30px; 
}
.text table td .img{
    width: 85px;
    margin: 0 auto
}

.text table td .img .pp{
    width: 50px;
    margin-top: 20px;
}
.text table .td_img img{
    width: 30px;
    height: 40px;
    margin-left: 4px;
    position: relative;
    top:-40px;
    left: 28px
}
</style>
