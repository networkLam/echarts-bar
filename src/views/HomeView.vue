<template>
  <div class="home">
    <div class="main" ref="main" style="width: 700px;height: 400px;"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import * as echarts from 'echarts'
export default {
  name: 'HomeView',
  data() {
    return {
      main: null,
    }
  },
  mounted() {
    console.log(this.$refs.main)
    var myChart = echarts.init(this.$refs.main);
    let option = {
      title: {
        // text: 'Accumulated Waterfall Chart'
      },
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'shadow'
        },
        formatter: function (params) {
          let tar;
          if (params[1] && params[1].value !== '-') {
            tar = params[1];
          } else {
            tar = params[2];
          }
          return tar && tar.name + '<br/>' + tar.seriesName + ' : ' + tar.value + '天';
        }
      },
      legend: {
        data: ['']
      },
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
      },
      xAxis: {
        type: 'value',
        data: (function () {
          let list = [];
          for (let i = 1; i <= 11; i++) {
            list.push('Nov ' + i);
          }
          return list;
        })(),

      },
      yAxis: {
        type: 'category',
        inverse: true,
        data: ['开始侦办', '侦办中', '侦办结束', '支付举报费']
      },
      series: [
        {
          name: 'Placeholder',
          type: 'bar',
          stack: 'Total',
          silent: false,
          itemStyle: {
            borderColor: 'transparent',
            color: 'transparent'
          },
          emphasis: {
            itemStyle: {
              borderColor: 'transparent',
              color: 'transparent'
            }
          },
          data: [0, 1, 11, 13]
        },
        {
          name: '2024-12-10 - 2024-12-10 ',
          type: 'bar',
          stack: 'Total',
          label: {
            show: true,
            position: 'inside',
            formatter(params){
              console.log(params)
              return params.value+"天"
            }
          },
          data: [1]
        }, {
          name: '2024-12-10 - 2024-12-11 ',
          type: 'bar',
          stack: 'Total',
          label: {
            show: true,
            position: 'inside',
            formatter(params){ //格式化展示的数据
              // console.log(params)
              return params.value+"天"
            }
          },
          data: ["-", 10]
        }, {
          name: '2024-12-10 - 2024-12-11',
          type: 'bar',
          stack: 'Total',
          label: {
            show: true,
            position: 'inside',
            formatter(params){
              console.log(params)
              return params.value+"天"
            }
          },
          color: "yellow",
          data: ["-", "-", 2,]
        },
        {
          name: '2024-12-10 - 2024-12-11',
          type: 'bar',
          stack: 'Total',
          label: {
            show: true,
            position: 'inside',
            formatter(params){
              console.log(params)
              return params.value+"天"
            }
          },
          color: "red",
          data: ["-", "-", '-', 7]
        }
      ]
    };
    option && myChart.setOption(option);
  },
  components: {
    HelloWorld
  }
}
</script>
