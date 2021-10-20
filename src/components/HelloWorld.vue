<template>
  <div class="hello">
    <!-- 准备具有宽高的容器 -->
    <div style="width: 600px; height: 600px" ref="chart"></div>
    <div ref="test" id="main" style="width: 650px; height: 600px">这是一个test用例</div>
  </div>
</template>

<script>
let Echarts = require("echarts/lib/echarts"); //基础实例 注意不要使用import
import * as echarts from "echarts";

export default {
  data() {
    return { chart: null,chart1: null };
  },
  mounted() {
    this.init();
    this.init1();
    // 窗口变化 触发addEventListener事件
    window.addEventListener("resize", () => {
      console.log(11111111111);
      
      this.chart.resize();
      this.chart1.resize();
    });
  },
  methods: {
    init() {
      //2.初始化
      this.chart = Echarts.init(this.$refs.chart);
      console.log("获取到的ref", this.$refs.test);
      //3.配置数据
      let option = {
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        }, //X轴
        yAxis: { type: "value" }, //Y轴
        series: [{ data: [120, 200, 150, 80, 70, 110, 130], type: "bar" }] //配置项
      };
      // 4.传入数据
      this.chart.setOption(option);
    },
    init1() {
      this.chart1 = Echarts.init(this.$refs.test);
      console.log("获取到的ref", this.$refs.test);
      var chartDom = document.getElementById("main");
      var myChart = echarts.init(chartDom);
      var option;
      const data = genData(50);
      option = {
        title: {
          text: "同名数量统计",
          subtext: "纯属虚构",
          left: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          type: "scroll",
          orient: "vertical",
          right: 10,
          top: 20,
          bottom: 20,
          data: data.legendData
        },
        series: [
          {
            name: "姓名",
            type: "pie",
            radius: "55%",
            center: ["40%", "50%"],
            data: data.seriesData,
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      function genData(count) {
        // prettier-ignore
        const nameList = [
        '赵', '钱', '孙', '李', '周', '吴', '郑', '王', '冯', '陈', '褚', '卫', '蒋', '沈', '韩', '杨', '朱', '秦', '尤', '许', '何', '吕', '施', '张', '孔', '曹', '严', '华', '金', '魏', '陶', '姜', '戚', '谢', '邹', '喻', '柏', '水', '窦', '章', '云', '苏', '潘', '葛', '奚', '范', '彭', '郎', '鲁', '韦', '昌', '马', '苗', '凤', '花', '方', '俞', '任', '袁', '柳', '酆', '鲍', '史', '唐', '费', '廉', '岑', '薛', '雷', '贺', '倪', '汤', '滕', '殷', '罗', '毕', '郝', '邬', '安', '常', '乐', '于', '时', '傅', '皮', '卞', '齐', '康', '伍', '余', '元', '卜', '顾', '孟', '平', '黄', '和', '穆', '萧', '尹', '姚', '邵', '湛', '汪', '祁', '毛', '禹', '狄', '米', '贝', '明', '臧', '计', '伏', '成', '戴', '谈', '宋', '茅', '庞', '熊', '纪', '舒', '屈', '项', '祝', '董', '梁', '杜', '阮', '蓝', '闵', '席', '季', '麻', '强', '贾', '路', '娄', '危'
    ];
        const legendData = [];
        const seriesData = [];
        for (var i = 0; i < count; i++) {
          var name =
            Math.random() > 0.65
              ? makeWord(4, 1) + "·" + makeWord(3, 0)
              : makeWord(2, 1);
          legendData.push(name);
          seriesData.push({
            name: name,
            value: Math.round(Math.random() * 100000)
          });
        }
        return {
          legendData: legendData,
          seriesData: seriesData
        };
        function makeWord(max, min) {
          const nameLen = Math.ceil(Math.random() * max + min);
          const name = [];
          for (var i = 0; i < nameLen; i++) {
            name.push(
              nameList[Math.round(Math.random() * nameList.length - 1)]
            );
          }
          return name.join("");
        }
      }

      option && myChart.setOption(option);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  display: flex;
}
</style>
