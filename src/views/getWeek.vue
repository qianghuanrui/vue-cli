<template>
  <div>
    <div :style="style.title">根据输入日期计算周一到周日的日期</div>
    <div>请输入日期 <input type="text" v-model="today" placeholder="yyyy-mm-dd" /></div>
    <div>今天是{{getWeek}}</div>
    <div>周一是{{monDay}}</div>
    <div>周日是{{sunDay}}</div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      today: '2021-06-23',
      style: {
        title: {
          fontSize: '18px',
          fontWeight: 600,
        }
      }
    }
  },
  computed: {
    getWeek(){
      const arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五','星期六']
      return arr[this.myDate]
    },
    myDate: function () {
      return new Date(this.today).getDay(); //获取周几 0-6 0是周日
    },
    monDay: function(){
      const num = this.myDate == 0 ? 6 : this.myDate-1; //距离周一的天数
      const date = new Date(new Date(this.today).getTime() - num*24*3600*1000);  // num天前
      return this.getDateTiem(date);
    },
    sunDay: function(){
      const num = this.myDate == 0 ? 0 : 7-this.myDate; //距离周日的天数
      const date = new Date(new Date(this.today).getTime() + num*24*3600*1000);  // num天后
      return this.getDateTiem(date);
    }
  },
  methods: {
    // 根据时间戳获取年月日
    getDateTiem(date){
      var year=date.getFullYear();
      var month=date.getMonth()+1>9?date.getMonth()+1:"0"+(date.getMonth()+1);
      var day=date.getDate()>9?date.getDate():"0"+date.getDate();
      const newDay=year+"-"+month+"-"+day;
      return newDay;
    }
  }
}
</script>

<style scoped>
</style>