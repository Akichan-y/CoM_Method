<template>
  <div>
    <nuxt-link to="/index_Senwohiku">  先をひくSVG</nuxt-link>
  <v-row justify="center" align="center">

    <v-col>
<svg id="svg" width="500" height="500">
    <!-- <path id="target_path" d="
			M 10,250
			L 490,250 Z"
    stroke="#000" fill="none" /> -->
    <path id="target_path" d="
		M 10,250
		L 490,250 490,490 10,490 Z"
    stroke="#000" fill="none"/>
   <circle id="move_circle" cx="0" cy="0" r="10" fill="red">
       <animateMotion dur="10s" repeatCount="indefinite">
         <mpath xlink:href="#target_path"></mpath>
       </animateMotion>

   </circle>
</svg>
       <label>
        <span>
          お名前:
        </span>
        <input
          type="text"
          v-model="user.name"
        >
      </label>
      <label>
        <span>
          email:
        </span>
        <input
          type="text"
          v-model="user.email"
        >
      </label>
    </v-col>
   <button
     type="button"
     @click="submit"
   >
     Submit
   </button>
  <v-col>
    <svg viewBox="0 0 200 200">
      <circle cx="100" cy="100" r="50"
      fill="rgba(0,0,0,0)"
      stroke="#c09"
      stroke-width="100"
      stroke-dasharray="10,10"
      />
    </svg>

  </v-col>


    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-card-text>
          <p>Vuetify is a progressive Material Design component framework for Vue.js. It was designed to empower developers to create amazing applications.</p>
          <p>
            For more information on Vuetify, check out the <a
              href="https://vuetifyjs.com"
              target="_blank"
              rel="noopener noreferrer"
            >
              documentation
            </a>.
          </p>
          <p>
            If you have questions, please join the official <a
              href="https://chat.vuetifyjs.com/"
              target="_blank"
              rel="noopener noreferrer"
              title="chat"
            >
              discord
            </a>.
          </p>
          <p>
            Find a bug? Report it on the github <a
              href="https://github.com/vuetifyjs/vuetify/issues"
              target="_blank"
              rel="noopener noreferrer"
              title="contribute"
            >
              issue board
            </a>.
          </p>
          <p>Thank you for developing with Vuetify and I look forward to bringing more exciting features in the future.</p>
          <div class="text-xs-right">
            <em><small>&mdash; John Leider</small></em>
          </div>
          <hr class="my-3">
          <a
            href="https://nuxtjs.org/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt Documentation
          </a>
          <br>
          <a
            href="https://github.com/nuxt/nuxt.js"
            target="_blank"
            rel="noopener noreferrer"
          >
            Nuxt GitHub
          </a>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
{{getGuntArryWait}}
<v-row>
    <v-btn @click="test">Pushテスト</v-btn>
</v-row>
<svg width="800" height="800" viewBox="0 0 200 200">
  <!-- <path d="M10,10 h100  m10,10 h100" fill="none" stroke="#1600FC" stroke-width="10" /> -->
  <path :d=path fill="none" stroke="#1600FC" stroke-width="10"  v-for="(path, idx) in getGuntArryWait" :key="idx"/>
  <!-- <path :d=path fill="none" stroke="#1600FC" stroke-width="10"  v-for="(path, idx) in paths" :key="idx"/>
  <path :d=path fill="none" stroke="pink" stroke-width="10"  v-for="(path, idx) in paths2" :key="idx"/> -->
  <!-- <path :d=paths[1] fill="none" stroke="pink" stroke-width="20" /> -->


  <!-- <path d="M 10 10 H 120 V 30 H 10 L 10 10"/> -->
  <!-- <path d="M50,0 L100,100 0,100" fill="#cccccc" /> -->
   <!-- <line  stroke="pink" stroke-width="20" :x1=Lines2[0][0] :y1=Lines2[0][1] :x2=Lines2[0][2] :y2=Lines2[0][3] /> -->
</svg>
<svg width="800" height="200" viewBox="0 0 100 100">
    <!-- <text x="0" y="20" font-family="serif" font-weight="bold" font-size="20" font-style="italic" text-decoration="underline" fill="#e74c3c">
    テキスト
    <tspan font-size="10" fill="#333">
      テキスト
    </tspan>
    テキスト
  </text> -->


  <line  x1="0"          y1="20" :x2=TimeValue[0][0] y2="20" :stroke=StatusValue[0][0] stroke-width="20"/>
  <line :x1=TimeValue[0][0] y1="20" :x2=TimeValue[0][1] y2="20" :stroke=StatusValue[0][1] stroke-width="20"/>
  <line :x1=TimeValue[0][1] y1="20" :x2=TimeValue[0][2] y2="20" :stroke=StatusValue[0][2] stroke-width="20"/>
  <line :x1=TimeValue[0][2] y1="20" :x2=TimeValue[0][3] y2="20" :stroke=StatusValue[0][3] stroke-width="20"/>
  <line :x1=TimeValue[0][3] y1="20" :x2=TimeValue[0][4] y2="20" :stroke=StatusValue[0][4] stroke-width="20"/>

  <text x="40" y="27" class="my-text">
      8:00〜
  
  </text>

  <line x1="0" y1="42" :x2=TimeValue[1][0] y2="42" :stroke=StatusValue[1][0] stroke-width="20"/>
  <line :x1=TimeValue[1][0] y1="42" :x2=TimeValue[1][1] y2="42" :stroke=StatusValue[1][1] stroke-width="20"/>
  <line :x1=TimeValue[1][1] y1="42" :x2=TimeValue[1][2] y2="42" :stroke=StatusValue[1][2] stroke-width="20"/>
  <line :x1=TimeValue[1][2] y1="42" :x2=TimeValue[1][3] y2="42" :stroke=StatusValue[1][3] stroke-width="20"/>
  <line :x1=TimeValue[1][3] y1="42" :x2=TimeValue[1][4] y2="42" :stroke=StatusValue[1][4] stroke-width="20"/>
  <line :x1=TimeValue[1][4] y1="42" :x2=TimeValue[1][5] y2="42" :stroke=StatusValue[1][5] stroke-width="20"/>
  <text x="40" y="49" class="my-text">
      9:00〜
  </text>
</svg>

<svg viewBox="0 0 63.6619772368 63.6619772368" class="sda-anime">
    <circle　cx="31.8309886184" cy="31.8309886184"
    r="15.9154943092" fill="rgba(0,0,0,0)"
    stroke="#c09"
    stroke-width="31.8309886184"
    :stroke-dashoffset=dashA
    :stroke-dasharray=dash
    />
    <circle　cx="31.8309886184" cy="31.8309886184"
    r="5.9154943092" 
    fill="rgba(100,100,100,0)"
    stroke="blue"
    stroke-width="3"
    :stroke-dashoffset=dashA
    :stroke-dasharray=dash
    />
</svg>

  </v-row>
  </div>
</template>



<style>

  .line {
    stroke-width: 4px;
    stroke-dasharray: 700px;
    stroke-dashoffset: 700px;
    animation: draw 2s linear infinite;
  }

  .my-text {
    font-size: 20px;
    font-weight: bold;
    font-family: Arial;
    /*fill: #fff;*/
    fill: none;
    /* stroke: #fff; */
    stroke: red;
    text-anchor: middle;
  }
</style>
<script>
import firebase from '@/plugins/firebase'

export default {
 data () {

   return {
     TimeValue:[[20,70,120,200,220],[10,90,100,120,300]],
     StatusValue:[["lightgreen","gray","pink","lightgreen","gray","pink"],["yellow","red","gray","blue","green"]],
     user: {
       name: "",
       email: ""
     },
     dash:[80,20],
    dashA:25,
    Lines:["x1='0' y1='0' x2='400' y2='200'","x1='15' y1='30' x2='220' y2='200'"],
    Lines2:[[0,20,70,90],[30,10,50,70]],
    paths:["M20,20 h80","M200,20 h10","M100,55 h25"],
    paths2:["M100,30 h100","M210,30 h20","M150,55 h45"]
   }
 },
 computed: {
    getGuntArryWait() {
      return this.$store.getters["timeBank/getGuntArryWait"];
    },
 },
 methods: {
   submit () {
     const db = firebase.firestore()
     let dbUsers = db.collection('users')
     dbUsers
       .add({
         name: this.user.name,
         email: this.user.email,
       })
       .then(ref => {
         console.log('Add ID: ', ref.id)
       })
   },
   test(){
     let round1=Math.round(Math.random()*1000);
     let round2=Math.round(Math.random()*1000);
     let round3=Math.round(Math.random()*100);

     this.$store.commit('timeBank/GuntArryWaitPush',{GuntStart:round1,GuntHorizon:round2,y:round3});
    //  console.log(this.getStatusData());
   }

  },
}
</script>