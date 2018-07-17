<template>
  <div class="hello">
    <button @click="interface_1">按钮1</button>
    <button @click="interface_2">按钮2</button>
    <button @click="interface_3">按钮3</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      url1:'http://192.168.1.186:3445/cup/match',
      url2:'http://192.168.1.186:3445/cup/bets',
      url3:'http://192.168.1.186:3445/cup/bets/12100',
    }
  },
  methods:{
    //get
    interface_1(){
      this.$axios.get(this.url1)
      .then((res)=>{
        console.log(res)
      }).catch(function(error){
        console.log(error)
      })
    },
    //post
    interface_2(){
      this.$axios.post(this.url2,{
        uid:52960041,   //从地址栏获取
        betsTimes:2,      //interface_1返回
        betsPrice:500,    //interface_1返回
        matchTarget:1,     //1 主队  -1 客队  0 平 由用户选择输入
        matchId:1,
        deviceId:'411467355B47CB37C7EB140BEA46E5CA' //从地址栏获取
      },{ headers: {
          'Content-Type':'application/json'
      }},)
      .then(function(res){
        console.log(res)
      }).catch(function(error){
        console.log(error)
      })
    },
    //get
    interface_3(){
      this.$axios.post(this.url3+'?pageNum='+1+'&pageSize='+100)
      .then(function(res){
        console.log(res)
      }).catch(function(error){
        console.log(error)
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>