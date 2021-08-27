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
      height="600px"
      elevation="20"
    >
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

        <v-row no-gutters class="mt-0 mb-0 pa-0">
          <v-col cols="4" fluid class="mt-0 mb-0 pa-0">

          </v-col>

          <v-col cols="8" class="mt-0">

            <v-row class="mt-0 pa-0">
              <v-col class="my-0 pa-0">
                <p class="indigo--text ml-15 mt-1 mb-0 mr-1 pa-0 text-center text--lighten-2 font-weight-bold headline"> {{ getStopWatchArray }}</p>
              </v-col>
               
             

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
            </v-row>
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
            <!-- {{MachineHour}} -->
            {{JikanHenkan(getNowMachineHour)}}
          </v-col>
          <v-col class="my-1 pa-0  text-center">
            {{JikanHenkan(getNowDacchaku)}}
            <!-- {{DacchakuJikan}} -->
            <!-- {{current_MH}} -->
          </v-col>
          <v-col class="my-1 pa-0  text-center">
            {{JikanHenkan(getNowDandori)}}
            <!-- {{DandoriJikan}} -->
            <!-- {{current_MH}} -->
          </v-col>
        </v-row>
        <!-- {{getM}} -->
        <v-row my-0>

          <svg width="500" height="50" my-5>

            <rect x="25" y="9" width="245" height="25" :fill=myColor3 stroke="blue" stroke-width="2" />

            <rect x="25" y="9" :width=myWidth2 height="25" :fill=myColor stroke="blue" stroke-width="2" />
            <text x="145" y="30" font-size="20" fill="rgva(0,255,0,0.5)" stroke="black" text-anchor="middle" stroke-width="0.1" >
              {{JikanHenkan(getmachineHourCut)}}
            </text>

          </svg>
        </v-row>

      <v-row my-0>

        <svg width="320" height="300"  viewBox="0 0 300 300" mt-0>
          <rect x="10" y="0" width="272" height="230" fill='#EEEEEE' stroke="blue" stroke-width="1" />
          <!-- <text x="0" y="0" font-family="Verdana" font-size="12" fill="gray">基準</text> -->

          <line x1="50" y1="28" x2="50" y2="220" stroke="darkgray" />
          <line x1="107.5" y1="28" x2="107.5" y2="220" stroke="darkgray" />
          <line x1="165" y1="28" x2="165" y2="220" stroke="darkgray" />
          <line x1="222.5" y1="28" x2="222.5" y2="220" stroke="darkgray" />

          <text x="46" y="20" font-family="Verdana" font-size="12" fill="gray">0</text>
          <text x="100" y="20" font-family="Verdana" font-size="12" fill="gray">15</text>
          <text x="157.5" y="20" font-family="Verdana" font-size="12" fill="gray">30</text>
          <text x="215" y="20" font-family="Verdana" font-size="12" fill="gray">45</text>

          <text x="15" y="50" font-family="Verdana" font-size="12" fill="gray">AM 7</text>
          <text x="38" y="64" font-family="Verdana" font-size="12" fill="gray">8</text>
          <text x="38" y="79" font-family="Verdana" font-size="12" fill="gray">9</text>
          <text x="32" y="95" font-family="Verdana" font-size="12" fill="gray">10</text>
          <text x="32" y="110" font-family="Verdana" font-size="12" fill="gray">11</text>
          <text x="15" y="125" font-family="Verdana" font-size="12" fill="gray">PM12</text>
          <text x="38" y="140" font-family="Verdana" font-size="12" fill="gray">1</text>
          <text x="38" y="155" font-family="Verdana" font-size="12" fill="gray">2</text>
          <text x="38" y="170" font-family="Verdana" font-size="12" fill="gray">3</text>
          <text x="38" y="185" font-family="Verdana" font-size="12" fill="gray">4</text>
          <text x="38" y="200" font-family="Verdana" font-size="12" fill="gray">5</text>
          <text x="38" y="216" font-family="Verdana" font-size="12" fill="gray">6</text>
          <!-- <text x="15" y="108" font-family="Verdana" font-size="12">8:00</text>
          <text x="15" y="108" font-family="Verdana" font-size="12">8:00</text>
          <text x="15" y="108" font-family="Verdana" font-size="12">8:00</text>
          <text x="15" y="108" font-family="Verdana" font-size="12">8:00</text>
          <text x="15" y="108" font-family="Verdana" font-size="12">8:00</text> -->

          <path :d=path fill="none" stroke="gray" stroke-width="9"  v-for="(path, idx) in getGuntArryWait" :key="idx"/>
          <path :d=path2 fill="none" stroke="rgb(0,255,0)" stroke-width="9"  v-for="(path2, idx2) in getGuntArryRUN" :key="idx2"/>
          <path :d=path3 fill="none" stroke="yellow" stroke-width="9"  v-for="(path3, idx3) in getGuntArryDDR" :key="idx3"/>
          <path :d=path3 fill="red" stroke="deeppink" stroke-width="9"  v-for="(path3, idx3) in getGuntArryKKT" :key="idx3"/>
          <path :d=path3 fill="red" stroke="deeppink" stroke-width="9"  v-for="(path3, idx3) in getGuntArryERR" :key="idx3"/>


          <line x1="12" y1="38" x2="280" y2="38" stroke="darkgray" />
          <line x1="12" y1="53" x2="280" y2="53" stroke="darkgray" />
          <line x1="10" y1="68" x2="280" y2="68" stroke="darkgray" />
          <line x1="10" y1="83" x2="280" y2="83" stroke="darkgray" />
          <line x1="10" y1="98" x2="280" y2="98" stroke="darkgray" />
          <line x1="10" y1="113" x2="280" y2="113" stroke="darkgray" />
          <line x1="10" y1="128" x2="280" y2="128" stroke="darkgray" />
          <line x1="10" y1="143" x2="280" y2="143" stroke="darkgray" />
          <line x1="10" y1="158" x2="280" y2="158" stroke="darkgray" />
          <line x1="10" y1="173" x2="280" y2="173" stroke="darkgray" />
          <line x1="10" y1="188" x2="280" y2="188" stroke="darkgray" />
          <line x1="10" y1="203" x2="280" y2="203" stroke="darkgray" />
         
        </svg>
      </v-row>


        <p class="grey--text mt-1 mb-0 ml-3 text-center  text--darken-1 font-weight-bold subtitle2">
          <!-- {{current_MH}} -->

          <!-- {{ chokuzenSW }} -->
        </p>



        



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
}
</style>

<script>
import Vue from "vue";
import Vuex from "vuex";

// const gradients = [
//   ["#222"],
//   ["#42b3f4"],
//   ["red", "orange", "yellow"],
//   ["purple", "violet"],
//   ["#00c6ff", "#F0F", "#FF0"],
//   ["#f72047", "#ffd200", "#1feaea"]
// ];
export default {
  props: ["name"],
  data() {
    return {
      A_Data:0,
      myWidth:10,

      // ObjStyleBool:[true,false,false,false,false,false,false],
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
      

      isTgt: false,
      nameAB: this.name, //propsからdataに移すことで、
      //変数として利用できるようになる。
      // imgSrcString:require('~/assets/img/MC031.jpg'),
      chokuzenSW: "aaa",
      // labels: [
      //   "8am",
      //   "9am",
      //   "10am",
      //   "11am",
      //   "1pm",
      //   "2pm",
      //   "3pm",
      //   "4pm",
      //   "5pm",
      //   "6pm"
      // ],
      width: 2,
      radius: 10,
      padding: 8,
      lineCap: "round",
      // gradient: gradients[5],
      defferenceTime: 0,
      KeikaJikanTime: "00:00:00",


      // gradientDirection: "top",
      // gradients,
      fill: false,
      type: "trend",
      autoLineWidth: false,
 
      //**********************************
        // データ詳細
      //**********************************
      //=********************************************************************
    };
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
        let xxx = 245 / Max_Value;

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
        // return this.$store.getters["timeBank/getStopWatchArraySinceStart"](this.nameAB)[1];
        return this.$store.getters["timeBank/getStopWatchArraySinceStart"](this.nameAB);
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
    // getcycleTimeDoughnut:function(){

    //   return this.$store.getters["timeBank/getcycleTimeDoughnut"](this.nameAB);
    // },
    getCycleTimeByouArryString:function(){
      let m = Math.floor(this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB)/60);
      let s = this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB)%60;
      let s_String = s.toString().padStart(2,"0");
      return `${m}分${s_String}秒`
      S.toString().padStart(2, "0") + "秒"
      // return this.$store.getters["timeBank/getCycleTimeByouArry"](this.nameAB);
    },
    calc_BekiKaisu:function(){
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

          return calc_result;

      
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
      let UntenSeconds = this.getTimeData;
      let KadouSeconds = this.$store.getters["timeBank/getProgressSeconds"];
      return (((UntenSeconds / KadouSeconds) * 10000) / 100).toFixed(1);
    },
    calcMachineRateDDR() {
      //段取り時間の率
      let DandoriSeconds = this.$store.getters["timeBank/getCycleArrayDDR"](
        this.nameAB
      );
      let KadouSeconds = this.$store.getters["timeBank/getProgressSeconds"];
      // return (Math.round((UntenSeconds/KadouSeconds)*100000))/10000
      return (((DandoriSeconds / KadouSeconds) * 10000) / 100).toFixed(1);
    },

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

    getNowMachineHour(){
      return this.$store.getters["timeBank/getNowMachineHour"](
        this.nameAB
      );
    },
    getNowDacchaku(){
      return this.$store.getters["timeBank/getNowDacchaku"](
        this.nameAB
      );
    },
    getNowDandori(){
      return this.$store.getters["timeBank/getNowDandori"](
        this.nameAB
      );
    },
  },
 
  methods: {

    JikanHenkan:function(NowSeconds){
      let m=0;
      let s=0;
      if(NowSeconds>0){ //処理のタイミングにより数秒マイナスになってしまうときの表示の適切化 2021/8/25
        m = Math.floor(NowSeconds / 60);
        s = "00" + String(NowSeconds % 60);
        return `${m}分${s.slice(-2)}秒`
      }else{
        m = Math.ceil(NowSeconds / 60);
        s = "00" + String(Math.abs(NowSeconds) % 60);
        return `−${m}分${s.slice(-2)}秒`
      }
      
    },


    redirect: function() {
      this.$router.push("/next?pageName=" + this.name);
    },
       
  }
};
</script>
