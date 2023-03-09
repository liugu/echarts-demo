<template>
  <div class="container">
    <!-- <img ref="dot" hidden src="../assets/map-bg.png"> -->
    <div id="myChart" ref="myChart" style="height: 800px"></div>
  </div>
</template>
<script>
import chinaJson from "./china.json";
let valArr = [
  {
    name: "四川省",
    value: 111,
  },
];

export default {
  data() {
    return {
      chart: null,
      options: {},
    };
  },
  mounted() {
    // console.log(chinaJson)

    this.$echarts.registerMap("china", chinaJson);

    // console.log(map)
    this.initOptions();
    this.initCharts();
  },

  methods: {
    initOptions() {
      this.options = {
        backgroundColor: "rgba(0,0,0,1)",
        tooltip: {
          show: true,
        },
        geo3D: {
          map: "china",
          aspectScale: 0.9, //长宽比
          zoom: 0.5,
          selectedMode: false, //是否允许选中多个区域
          label: {
            show: false,
            color: "#fff",
            textStyle: {
              color: "#fff",
            },
            formatter: (params) => {
              if (valArr.find((ele) => ele.name == params.name)) {
                return (
                  params.name +
                  "\n" +
                  valArr.find((ele) => ele.name == params.name).value
                );
              } else {
                return params.name;
              }
            },
            backgroundColor: "rgba(0,0,0,0.5)",
            padding: [5, 5],
            borderRadius: 4,
          },
          itemStyle: {
            color: "transparent",
            // shadowColor: 'rgba(0,243,255,0.2)',
            // shadowOffsetY: 5,
            // shadowBlur: 10,
            borderColor: "transparent",
            // borderWidth: 1,
            opacity: 0,
          },
        },
        series: [
          {
            name: "MAP",
            type: "map3D",
            map: "china",
            label: {
              show: true,
              textStyle: {
                color: "#fff",
              },
              formatter: (params) => {
                if (valArr.find((ele) => ele.name == params.name)) {
                  return (
                    params.name +
                    "\n" +
                    valArr.find((ele) => ele.name == params.name).value
                  );
                } else {
                  return params.name;
                }
              },
              borderRadius: 4,
            },
            itemStyle: {
              color: "#144a69",
              // shadowColor: 'rgba(0,243,255,0.2)',
              // shadowOffsetY: 5,
              // shadowBlur: 10,
              borderColor: "#06767c",
              borderWidth: 1,
              // opacity: 1,
            },

            aspectScale: 0.9, //长宽比
            selectedMode: false, //是否允许选中多个区域
            data: valArr,
          },
        ],
      };
    },
    initCharts() {
      this.chart = this.$echarts.init(document.getElementById("myChart"));
      this.chart.setOption(this.options);
    },
  },
};
</script>
