<template>
  <dir>
    
    <!-- <v-app></v-app>  これを使うと、component配置で上下の感覚がバカ広くなってしまうのでdirに変更-->
    <!-- <v-btn class="red" @click="redirect">Redirectテスト</v-btn> -->
    <!-- <p class="pink--text text--lighten-2 font-weight-bold overline">{{getProgressSeconds}}秒経過</p>
      <p class="green--text text--lighten-2 font-weight-bold subtitle">{{getStopWatchSecondsArray}}</p> -->
    <!-- <v-card width=420px height="280px" elevation="15" color="grey lighten-1"> -->
    <!-- <v-card class="mt-n12 mx-auto" width=300px height="420px" elevation="20" > -->
    <v-card
      class="mt-1 mb-1 py-0 mx-auto"
      width="300px"
      height="650px"
      elevation="20"
    >
      <!-- <v-btn @click='Methods_calcMachineRate'>test</v-btn> -->
      <!-- <v-btn @click='btnPie'>test</v-btn>
      <v-btn @click='testtest'>testtest</v-btn> -->
      <!-- <v-btn @click='testtest'>Detail</v-btn> -->
      {{getmachineHourCut}}
      <v-container class="my-0 py-0 grey lighten-5">
          <p class="my-0 text-right">
            {{CycleTimeNokori}}---{{ getSensingStTime }}〜
          </p>
        <v-row justify="center" class="mt-0" >
          <div
            class="mt-0 green-circle btnLamp"
            v-if="getStatusData == 1"
            @click="redirect"
          >
            {{ name }} 運転中【CT {{ getCycleTimeByouArryString }}】
            <!-- {{ name }} 運転中 {{ getSensingStTime }}〜 -->
          </div>
          <div
            class="mt-0 red-circle btnLamp"
            v-else-if="getStatusData == 2"
            @click="redirect"
          >
            {{ name }} 異常発生中 【CT {{ getCycleTimeByouArryString }}】
          </div>
          <div
            class="mt-0 yellow-circle btnLamp"
            v-else-if="getStatusData == 3"
            @click="redirect"
          >
            {{ name }} 段取中 【CT {{ getCycleTimeByouArryString }}】
          </div>
          <div
            class="mt-0 pink-circle btnLamp"
            v-else-if="getStatusData == 4"
            @click="redirect"
          >
            {{ name }} 計画停止中 【CT {{ getCycleTimeByouArryString }}】
          </div>
          <div class="mt-0 black-circle btnLamp" v-else @click="redirect">
            {{ name }} 停止中【CT {{ getCycleTimeByouArryString }}】
          </div>
        </v-row>
        <div class="mt-3 ml=2 text-left caption font-size=12px" :class="{ contentTgt: isTgt }">
          {{ getCurrentTarget }}
        </div>
        <!-- <v-btn @click='RstTgt'>Reseet</v-btn> -->

        <v-row no-gutters class="mt-0 mb-0 pa-0">
          <v-col cols="4" fluid class="mt-0 mb-0 pa-0">

          </v-col>

          <v-col cols="8" class="mt-0">

            <v-row class="mt-0 pa-0">
              <p
                class="indigo--text ml-15 mt-1 mb-0 mr-1 pa-0 text-right text--lighten-2 font-weight-bold headline"
              >
                {{ getStopWatchArray }}
              </p>

            </v-row>
            <v-row class="mt-1   pa-0">
              <v-col class="my-0 pa-0">
                <p
                  class="orange--text my-0 mr-1 text-right text--lighten-1 font-weight-bold headline"
                >
                  {{ getCycleCounterDataDDR }}回
                </p>
              </v-col>
              <v-col class="my-1 pa-0">
                <p
                  class="orange--text my-0 mr-1 text-right  text--lighten-1 font-weight-bold headline"
                >
                  {{ calcMachineRateDDR }}%
                </p>
              </v-col>
            </v-row>
            <v-row class="mt-0 pa-0">
              <v-col class="my-0 pa-0">
                <p
                  class="green--text my-0 mr-1 text-right text--lighten-1 font-weight-bold headline"
                >
                  {{ getCountData }}回
                </p>
              </v-col>
              <v-col class="my-0 pa-0">
                <p
                  class="green--text my-0 mr-1 text-right text--lighten-1 font-weight-bold headline"
                >
                  {{ calcMachineRate }}%
                </p>
              </v-col>
            </v-row>
          </v-col>
        </v-row >

            <v-row class="mt-0 ml-2 pa-0">
              <v-col class="my-0 ml-2 pa-0">
                <p
                    class="my-5 mr-5 text-center text--lighten-1 font-weight-bold headline ObjStyleA"
                    v-bind:style="Beki"
                >
                   可動率  {{ calc_BekiDouRitsu }}%({{calc_ShinChokuKaisu(false)}})
                </p>

              </v-col>
              <!-- <v-col class="my-0 pa-0">
                  <p
                  class="green--text my-2 mr-1 text-right  text--lighten-1 font-weight-bold headline"
                >
                  {{ calcMachineRate }}%
                </p>
              </v-col> -->
            </v-row>
        <!-- {{getM}} -->
        <svg width="500" height="100" my-5>

          <rect x="5" y="9" width="240" height="25" :fill=myColor3 stroke="blue" stroke-width="2" />

          <!-- <rect x="5" y="29" :width="200" height="25" :fill=myColor stroke="blue" stroke-width="2" /> -->
          <rect x="5" y="9" :width=myWidth2 height="25" :fill=myColor stroke="blue" stroke-width="2" />

        </svg>




        <v-row class="mt-0 pa-0">
          <v-col class="my-0 ml-5 pa-0 text-center">
             マシン
          </v-col>
          <v-col class="my-0 pa-0  text-center">
            脱着
          </v-col>
          <v-col class="my-0 pa-0  text-center" >
            段取
          </v-col>
        </v-row>
        <v-row class="mt-0 pa-0">
          <v-col class="my-1 ml-5 pa-0  text-center">
            {{MachineHour}}
          </v-col>
          <v-col class="my-1 pa-0  text-center">
            {{DacchakuJikan}}
          </v-col>
          <v-col class="my-1 pa-0  text-center">
            {{DandoriJikan}}
          </v-col>
        </v-row>

        <p class="grey--text mt-1 mb-0 ml-3 text-center  text--darken-1 font-weight-bold subtitle2">
          <!-- {{current_MH}} -->

          <!-- {{ chokuzenSW }} -->
        </p>
<v-btn @click="test">Wait</v-btn>
<v-btn @click="test2">RUN</v-btn>
<svg width="500" height="800" viewBox="0 0 200 200" background='lightgray'>
  <rect x="0" y="50" width="100" height="100" fill='lightgray' stroke="blue" stroke-width="1" />
  <path :d=path fill="none" stroke="gray" stroke-width="6"  v-for="(path, idx) in getGuntArryWait" :key="idx"/>
  <path :d=path2 fill="none" stroke="rgb(0,255,0)" stroke-width="6"  v-for="(path2, idx2) in getGuntArryRUN" :key="idx2"/>
  <path :d=path3 fill="none" stroke="yellow" stroke-width="6"  v-for="(path3, idx3) in getGuntArryDDR" :key="idx3"/>

</svg>


        



        <!-- <p class="pink--text text--lighten-2 font-weight-bold">エラー時間
            :{{getTimeDataErr}}秒</p>
          <p class="pink--text text--lighten-2 font-weight-bold ">エラー発生回数：{{getCountErrData}}回</p> -->
          <!-- <img :src="image_src" width="100%" -->
          
          <!-- <v-card-title>Top 10 Australian beaches</v-card-title> -->
    <!-- <v-img
      mt-2
      class="white--text align-end"
      height="200px"
      src="~/assets/img/BM15.png"
    >
      <v-card-title>Top 10 Australian beaches</v-card-title>
    </v-img> -->
      </v-container>
    </v-card>
  </dir>
</template>

<style>
.ObjStyleA{
  outline:1px solid grey;
  border-radius: 15px; /* まるみ */
}



.contentTgt {
  /* animation: flash 1s linear infinite; */
  animation: flash 1s linear;
  animation-fill-mode: backwards;
  width: 220px;
  /* height:30px; */
  /* background:#0091EA; */
  background: white;
  margin: 5px;
}

@keyframes flash {
  0%,
  35%,
  60%,
  100% {
    opacity: 0;
  }

  25% {
    opacity: 1;
    background: #7fff00;
  }

  50% {
    opacity: 1;
    background: #0091ea;
  }

  75% {
    opacity: 1;
    background: #ff1493;
  }
}
/* @keyframes flash {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
} */

.cont {
  color: blue;
  font-size: 2em;
  text-align: center;
}

.btnLamp {
  cursor: pointer;

  display: inline-block; /* センター寄せ用 */
  border-radius: 10px; /* まるみ */
  height: 40px; /* 円の大きさ */
  width: 240px; /* 円の大きさ */
  margin-right: 10px;
  margin-bottom: 5px;
  margin-top: 20px;
  text-align: center;
  line-height: 40px;
  user-select: none;
}
.btnLamp:active {
  margin-top: 25px;
  margin-bottom: 0px;
}

.btnLamp:hover {
  opacity: 0.8;
}
.redCollor {
  color: red;
  background: #7fff00;
  
}
.green-circle {
  background-color: rgb(0, 255, 0); /* ベースカラー */
  box-shadow: 0 0 3px 3px rgb(37, 112, 4),
    3px 3px 5px 3px rgb(200, 255, 0) inset; /* 外側のカラー・左上のカラー */

  /* 以下はそろえるだけの為のmargin */
  border-color: red;
}
.red-circle {
  /* display: inline-block; */
  color: white;
  
  background-color: rgb(255, 0, 0);
  box-shadow: 0 0 3px 3px rgb(78, 3, 3),
    3px 3px 5px 3px rgb(238, 161, 147) inset;
}
.yellow-circle {
  /* display: inline-block; */
  color: black;
  background-color: rgb(255, 255, 0);
  box-shadow: 0 0 3px 3px rgb(136, 80, 7),
    3px 3px 5px 3px rgb(247, 238, 161) inset;

}
.pink-circle {
  /* display: inline-block; */
  color: black;
  background-color: rgb(247, 174, 234);
  box-shadow: 0 0 3px 3px rgb(122, 56, 106),
    3px 3px 5px 3px rgb(243, 146, 240) inset;

}
.black-circle {
  /* display: inline-block; */
  color: black;
  background-color: silver;
  box-shadow: 0 0 3px 3px rgb(54, 53, 53),
    3px 3px 5px 3px rgba(172, 169, 169, 0.5) inset;
  /* height:40px;
    width:240px; */
  /* border-radius:10px;
    margin-right: 10px;
    margin-bottom: 5px;
    margin-top: 20px;
    text-align: center;
    line-height: 40px;
    user-select: none; */
}
</style>

<script>
import Vue from "vue";
import Vuex from "vuex";
// import BarChart from "@/components/BarChart.vue";
// import LineChart from "@/components/LineChart.vue";
// import MachineH_Porogress from "@/components/MachineH_Progress.vue";

const gradients = [
  ["#222"],
  ["#42b3f4"],
  ["red", "orange", "yellow"],
  ["purple", "violet"],
  ["#00c6ff", "#F0F", "#FF0"],
  ["#f72047", "#ffd200", "#1feaea"]
];
export default {
  // tgtMachine:"",
  props: ["name"],
  // props:{
  //   nameA:"name"
  // },
  data() {
    return {
      A_Data:0,
      myWidth:10,
      // myColor:"rgb(0,255,0)",
      // myColorBack:"lightgray",
      // imgSrcString:"https://cdn.vuetifyjs.com/images/cards/docks.jpg",
      ObjStyleBool:[true,false,false,false,false,false,false],
      isRed:true,
      isBlue:false,
      MachineHour:"",
      DacchakuJikan:"",
      DandoriJikan:"",
      ar:[],
      styleObject:{
            color:"gray",
            background:"white",
        },
      
      // nameAB:'MC027'
      // testData:'',
      // btnName: '追加',
      // isRed: false,
      isTgt: false,
      nameAB: this.name, //propsからdataに移すことで、
      //変数として利用できるようになる。
      // imgSrcString:require('~/assets/img/MC031.jpg'),
      chokuzenSW: "aaa",
      labels: [
        "8am",
        "9am",
        "10am",
        "11am",
        "1pm",
        "2pm",
        "3pm",
        "4pm",
        "5pm",
        "6pm"
      ],
      // value: [200, 675, 410, 390, 310, 460, 250, 240, 240, 3600],

      width: 2,
      radius: 10,
      padding: 8,
      lineCap: "round",
      gradient: gradients[5],
      // value: [10, 8, 3, 9, 7, 10, 3, 2, 0, 0, 1, 3, 2, 2, 0],
      // value2: {LN034:[2, 2, 2, 2, 7, 10, 3, 2, 0, 0],MC027:[10, 8, 8, 9, 7, 10, 3, 2, 0, 8]},
      defferenceTime: 0,
      KeikaJikanTime: "00:00:00",

      //TypeB
      // TypeB = {};
      // TypeB['hoge'] = {fuga : 'piyo'};
      // alert(TypeB['hoge']['fuga']);

      gradientDirection: "top",
      gradients,
      fill: false,
      type: "trend",
      autoLineWidth: false,
      // 円グラフで使用するデータセット**********************************
      chartData: {
        labels: [],
        // データ詳細
      },
      //**********************************
        // backgroundColor: "rgba(54,162,235,0.2)",
        
        // データ詳細
      //**********************************
      //=********************************************************************
    };
  },
  components: {
    // BarChart,
    // LineChart,
    // MachineH_Porogress
  },
  computed: {
    getGuntArryWait() {
      return this.$store.getters["timeBank/getGuntArryWait"](this.nameAB);
    },
    getGuntArryRUN() {
      return this.$store.getters["timeBank/getGuntArryRUN"](this.nameAB);
    },
    getGuntArryDDR() {
      return this.$store.getters["timeBank/getGuntArryDDR"](this.nameAB);
    },
    getGuntArryERR() {
      return this.$store.getters["timeBank/getGuntArryERR"](this.nameAB);
    },
    getGuntArryKKT() {
      return this.$store.getters["timeBank/getGuntArryKKT"](this.nameAB);
    },
    getStopWatchArray() {
      if (this.getCountData == 0) {
        return "0分00秒";
      } else {
        return this.$store.getters["timeBank/getStopWatchArray"](this.nameAB);
      }
    },
    tmp_cut(){
      return this.$store.getters["timeBank/getmachineHourCutArry"](this.nameAB);
    },
    getmachineHourCut(){
      return this.$store.getters['timeBank/getmachineHourCutArry'](this.nameAB)
    },
     myWidth2(){
        this.A_Data = this.$store.getters["timeBank/getmachineHourCutArry"](this.nameAB);
        console.log(this.nameAB+"の　A_Dataは、" + this.A_Data);
        // console.log("Cutの値は、" + this.nameAB + "で、" +this.$store.getters["timeBank/getmachineHourCutArry"](this.nameAB));
        let Max_Value=0;
        try{
           //例外が発生する可能性のある処理
          Max_Value= this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB)[0];
        }catch(e){
            //例外が発生した場合の処理
          console.log(e);
          Max_Value= this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB);
        };
        // let Max_Value= this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB)[0];
        // let Max_Value= this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB);
        let xxx = 240 / Max_Value;

        console.log("Max_Valueは、" + Max_Value + "倍率は、" + xxx);

        if(this.A_Data<=0){
          this.A_Data=1;
        }
        this.myWidth = this.A_Data * xxx ;
        return this.myWidth;
     },
     myColor(){
        if(this.$store.getters["timeBank/getStatus"](this.nameAB)== 1){
          return 'rgb(0,255,9)';
        }else{
          return 'lightgray';
        }
     },
     myColor3(){
        if(this.$store.getters["timeBank/getStatus"](this.nameAB)== 1){
            switch (true){
              case this.A_Data<5:
                    return 'deeppink';
                    break;
              case this.A_Data<15:
                    // return 'darkorange';
                    return 'pink';
                    break;
              case this.A_Data<30:
                    return 'rgba(255, 215, 0,0.9)';
                    break;
              default: 
                return 'lightgray';
            };
              


          }else{
              return 'lightgray';
          }
        },

     Beki(){
       let NowChinchoku = this.getCountData - this.calc_BekiKaisu;
      //  console.log("答ーえは！"+NowChinchoku);
        // for(const elm of this.ObjStyleBool){
        //   elm=false;
        // };
        // console.log("色分けは、"+newD);
        switch(true) {
            case NowChinchoku <= -21:
                return{
                  color:"red",
                  background:"black"
                }
                break;
            case NowChinchoku >= -20 && NowChinchoku <= -6:
                return{
                  color:"white",
                  background:"red"
                }
                break;
            case NowChinchoku >= -5 && NowChinchoku < -3:
                return{
                  color:"black",
                  background:"yellow"
                }
                break;
            case NowChinchoku >= -3 && NowChinchoku < 3 :
                return{
                  color:"grey",
                  background:"white"
                }
                break;
            case NowChinchoku >= 3 && NowChinchoku < 7 :
                return{
                  color:"gray",
                  background:"aqua"
                }
                break;
            case NowChinchoku >= 7 && NowChinchoku < 20 :
                return{
                  color:"white",
                  background:"blue"
                }
                break;
            case NowChinchoku >= 21:
                return{
                  color:"#ff1493",
                  background:"blue"
                }
                break;
            default:
                //=============================
                //======================================
        }
    },

    CycleTimeNokori(){
      // getStopWatchArraySinceStart
        // return this.$store.getters["timeBank/getStopWatchArraySinceStart"](this.nameAB)[1];
        // a = this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB);
        // b = this.$store.getters["timeBank/getStopWatchSecondsArry"](this.nameAB);
        // b = this.$store.getters["timeBank/getSensingTimeStart"](this.nameAB);
        // return a-b;
    },
    // getSensingTimeStart(){
    //   return this.$store.getters['timeBank/getSensingTime'](this.nameAB)
    // },
    image_src(){
      return require("~/assets/img/"+this.nameAB+".jpg");
    },
    getCycleTimeByouArry:function(){

      return this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB);
    },
    getcycleTimeDoughnut:function(){

      return this.$store.getters["timeBank/getcycleTimeDoughnut"](this.nameAB);
    },
    getCycleTimeByouArryString:function(){
      let m = Math.floor(this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB)/60);
      let s = this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB)%60;
      let s_String = s.toString().padStart(2,"0");
      return `${m}分${s_String}秒`
      S.toString().padStart(2, "0") + "秒"
      // return this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB);
    },
    calc_BekiKaisu:function(){
      // console.log(this.getProgressSeconds);
      // console.log(this.getCycleTimeByouArry);

      return Math.round(this.getProgressSeconds / this.getCycleTimeByouArry*100)/100;
    },

    calc_ShinChokuKaisu:function(){
      //普通computedに引数を渡すことはできませんが、返り値を関数にして、そこに引数を書けば渡すことができます。
      return function(isV){
        let calc_result = Math.round((this.getCountData - this.calc_BekiKaisu));
  
        if(isV){  
          //Valur数値の場合
          return calc_result;
        }else{
          //文字列の場合
          if(calc_result<0){
              return `▲${Math.abs(calc_result)}`;
          }else if(calc_result==0){
              return `±${Math.abs(calc_result)}`;
            }else{
              return `+${calc_result}`;
          };
        }

      }
      
    },
    calc_BekiDouRitsu:function(){
      let calc_result = Math.round((this.getCountData / this.calc_BekiKaisu) *100);
    
          // console.log(calc_result);
          return calc_result;

      
    },

    current_MH:function(){
      console.log("AAAAAAAA"+this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB));
      return this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB,0);
      // let ar = [];
      // this.ar= this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB,0)[0]
      // ar = this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB)[0];
      // console.log(this.ar);
      // console.log(ar.length);
      // console.log("マシンは、" + ar.shift());
      // return ar;
      // if (this.getCountData == 0) {
      //   return "0分00秒";
      // } else {
      //   return this.$store.getters["timeBank/getStopWatchArray"](this.nameAB);
      // }
    },
    current_Dacchaku:function(){
      this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB,1)
    },
    current_Dandori:function(){
      this.$store.getters["timeBank/getmachineHourArryTgt"](this.nameAB,2)
    },


    getCurrentTarget: function() {
      return this.$store.getters["timeBank/getCurrentTarget"](this.nameAB);
    },
    getCycleArray: function() {
      return this.$store.getters["timeBank/ getCycleArray"](this.nameAB);
    },
    getProgressSeconds: function() {
      return this.$store.getters["timeBank/getProgressSeconds"];
    },
    getSensingStTime() {
      return this.$store.getters["timeBank/getSensingStTime"](this.nameAB);
    },

    getStopWatchSecondsArray() {
      return this.$store.getters["timeBank/getStopWatchSecondsArray"](
        this.nameAB
      );
    },
    // StopWatch(){
    //   return this.$store.getters['timeBank/getStopWatchArray'](this.nameAB)
    // },
    value3() {
      return this.$store.getters["timeBank/getSpark"](this.nameAB);
    },

    getStatusData() {
      return this.$store.getters["timeBank/getStatus"](this.nameAB);
    },



    //機械の稼働時間秒数
    //運転中は時間が加算されるようにして、稼働率を正確に把握する
    //マシンアワーの長いものでは特に有効となる
    getTimeData() {
      let RunningTime = 0;
      if (this.$store.getters["timeBank/getStatus"](this.nameAB) == 1) {
        RunningTime = this.$store.getters["timeBank/getStopWatchSecondsArray"](
          this.nameAB);
      } else {
        RunningTime = 0;
      }
      let CycleTimeTotal = this.$store.getters["timeBank/getCycleArray"](
        this.nameAB);
      return CycleTimeTotal + RunningTime;
    },

    getTimeDataMS() {
      let M = Math.floor(this.getTimeData / 60);
      let S = this.getTimeData % 60;

      return M + "分" + S.toString().padStart(2, "0") + "秒";
    },

    calcMachineRate() {
      //機械の現在稼働率
      // let UntenSeconds = this.$store.getters['timeBank/getCycleArray'](this.nameAB);
      let UntenSeconds = this.getTimeData;
      let KadouSeconds = this.$store.getters["timeBank/getProgressSeconds"];
      // console.log(UntenSeconds);
      // return (Math.round((UntenSeconds/KadouSeconds)*100000))/10000
      return (((UntenSeconds / KadouSeconds) * 10000) / 100).toFixed(1);
    },
    calcMachineRateDDR() {
      //段取り時間の率
      // let UntenSeconds = this.$store.getters['timeBank/getCycleArray'](this.nameAB);
      let DandoriSeconds = this.$store.getters["timeBank/getCycleArrayDDR"](
        this.nameAB
      );
      let KadouSeconds = this.$store.getters["timeBank/getProgressSeconds"];
      // return (Math.round((UntenSeconds/KadouSeconds)*100000))/10000
      return (((DandoriSeconds / KadouSeconds) * 10000) / 100).toFixed(1);
    },

    // getTimeDataErr_generateMS(){//機械のエラー時間秒数
    //   return this.$store.getters['timeBank/getCycleArrayErr'](this.nameAB)
    //   // return this.$store.getters['timeBank/getCycleArray2'](this.nameAB)
    // },
    getTimeDataErr_generateMS() {
      //機械のエラー時間秒数
      let M = Math.floor(
        this.$store.getters["timeBank/getCycleArrayErr"](this.nameAB) / 60
      );
      let S =
        this.$store.getters["timeBank/getCycleArrayErr"](this.nameAB) % 60;

      return M + "分" + S.toString().padStart(2, "0") + "秒";
    },
    getTimeDataDDR_generateMS() {
      //機械の段取り時間秒数
      let M = Math.floor(
        this.$store.getters["timeBank/getCycleArrayDDR"](this.nameAB) / 60
      );
      let S =
        this.$store.getters["timeBank/getCycleArrayDDR"](this.nameAB) % 60;

      return M + "分" + S.toString().padStart(2, "0") + "秒";
    },

    getCountData() {
      return this.$store.getters["timeBank/getCycleCounterData"](this.nameAB);
    },
    getCountErrData() {
      return this.$store.getters["timeBank/getCycleCounterDataErr"](
        this.nameAB
      );
    },
    getCycleCounterDataDDR() {
      return this.$store.getters["timeBank/getCycleCounterDataDDR"](
        this.nameAB
      );
    },

    getSensingTime() {
      //やめよう！
      // const d= this.$store.getters['timeBank/getSensingTime'](this.nameAB);
      //  console.log(d);
      //純粋な引き算のストップウォッチなので、UTC時間（世界標準で時差考慮せず）を使用する
      // const h = String(d.getUTCHours()).padStart(2,'0');
      // const m = String(d.getUTCMinutes()).padStart(2,'0');
      // const s = String(d.getUTCSeconds()).padStart(2,'0');
      // console.log(`時間は、${h}:${m}:${s}`);
      // return `${h}:${m}:${s}`;
    }
    // getSensingTimeStart(){
    //   return this.$store.getters['timeBank/getSensingTime'](this.nameAB)

    // }
  },
  watch: {
    // calc_BekiDouRitsu:function(newD,oldD){
    
    // console.log("これはどうだ！" + this.calc_BekiDouRitsu);
    // console.log(newD);
    //   this.Beki(newD);
    // },
    getCurrentTarget: function(newTgt, oldTgt) {
      // alert(newTgt);

      this.isTgt = true;

      // this.isTgt=false;
      // this.isRed=true;
      // this.sleep(2, function() {
      // // console.log('5秒経過しました！');

      //   this.isTgt=false;
      //   // alert('5秒経過しました！');
      // });
    },
    getStatusData: function(newStatus, oldStatus) {
      this.graphUD();
    }
  },
  mounted: function() {
    
    // this.graphUD();
    // this.Beki(calc_BekiDouRitsu);
    // this.Beki(this.calc_BekiDouRitsu);
  },
  methods: {
    test(){
      let round1=Math.round(Math.random()*1000);
      let round2=Math.round(Math.random()*1000);
      let round3=Math.round(Math.random()*100);

      // this.$store.commit('timeBank/GuntArryWaitPush',{GuntStart:round1,GuntHorizon:round2,y:round3});
      this.$store.commit('timeBank/GuntArryWaitPush',{GuntStart:round1,GuntHorizon:round2,y:round3,machine:this.nameAB});
      //  console.log(this.getStatusData());
    },
    test2(){
      let round1=Math.round(Math.random()*1000);
      let round2=Math.round(Math.random()*1000);
      let round3=Math.round(Math.random()*100);

      // this.$store.commit('timeBank/GuntArryWaitPush',{GuntStart:round1,GuntHorizon:round2,y:round3});
      this.$store.commit('timeBank/GuntArryRUNPush',{GuntStart:round1,GuntHorizon:round2,y:round3,machine:this.nameAB});
      //  console.log(this.getStatusData());
    },
    JikanHenkan:function(NowSeconds){
      let m = Math.floor(NowSeconds / 60);
      let s = "00" + String(NowSeconds % 60);
      
      return `${m}分${s.slice(-2)}秒`
    },


    redirect: function() {
      this.$router.push("/next?pageName=" + this.name);
    },
   
    graphUD: function() {
      console.log(this.nameAB +"======>"+this.current_MH);
      this.MachineHour = this.JikanHenkan(this.current_MH[0]);
      this.DacchakuJikan = this.JikanHenkan(this.current_MH[1]);
      this.DandoriJikan = this.JikanHenkan(this.current_MH[2]);
      
    },
    
  }
};
</script>
