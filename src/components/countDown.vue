<template>
 <div>
   <div class="board">
       <span class="card">{{days}}天</span>:<span class="card">{{hours}}时</span>:<span class="card">{{minutes}}分</span>:<span class="card">{{seconds}}秒</span>
   </div>
 </div>
</template>
<script>
 export default {
  name: "countDown",
  props: {
   time: {
     type: Number
   },
  },
  data() {
   return {
    days:0,
    hours:0,
    minutes:0,
    seconds:0,
    curTime: this.time,
   }
  },
   computed: {
   disabled() {
    return !(this.start && !this.end && !this.done);
   }
  },
  created() { 
   this.updateState();
   this.timeInterval=setInterval(()=>{
    this.updateState()
   },1000)
  },
  updated(){
   if(this.end||this.done){
    clearInterval(this.timeInterval)
   }
  },
  methods: {
   updateState() {
    const time = this.curTime - 1000;
    this.curTime = time;
    [this.days,this.hours,this.minutes,this.seconds] = this.getDuration(this.curTime);
    this.judgeStop(this.curTime);
   },
    judgeStop(time){
      if(time === 0){
        this.$emit('end','倒计时结束');
        clearInterval(this.timeInterval)
      }
    },
    getDuration(my_time) {  
      var days    = my_time / 1000 / 60 / 60 / 24;
      var daysRound = Math.floor(days);
      var hours = my_time / 1000 / 60 / 60 - (24 * daysRound);
      var hoursRound = Math.floor(hours);
      var minutes = my_time / 1000 / 60 - (24 * 60 * daysRound) - (60 * hoursRound);
      var minutesRound = Math.floor(minutes);
      var seconds = Math.floor(my_time / 1000 - (24 * 60 * 60 * daysRound) - (60 * 60 * hoursRound) - (60 * minutesRound));
      return [this.twoDigits(daysRound),this.twoDigits(hoursRound),this.twoDigits(minutesRound),this.twoDigits(seconds)];
    },
    twoDigits(num){
      if(num<10){
        return '0'+ num
      }else{
        return num;
      }
    },
    
  },
  beforeDestroy() {
   clearInterval(this.timeInterval)
  }
 }
</script>
<style scoped>
 .board{
    font-size: 50px;
 }
 .card{
    background-color: #ffffff;
 }
</style>