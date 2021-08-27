<template>
 <dir>

   <v-row>
     <v-col   cols="12" sm="1" md="1" lg="1" xl="1">
      <h2>{{message}}</h2>
      <h2>{{getTest}}</h2>
      <h2>{{getKeikaJikan}}</h2>
      <h2>{{getGenzaiJikan}}</h2>
      <v-btn @click="KyouseiReset">リセット</v-btn>
     </v-col>
    <v-col  cols="12" sm="1" md="1" lg="1" xl="1">
        <v-checkbox
          v-model="Nishio"
          label="西尾"
        ></v-checkbox>
     </v-col>
     <v-col  cols="12" sm="1" md="1" lg="1" xl="1">
        <v-checkbox
          v-model="NishioHP"
          label="HP"
        ></v-checkbox>
     </v-col>
     <!-- <v-col>
        <div  width="50px" height="50px" v-if="Nishio == true">
          <img src="~/assets/factory/Nishio.png" width="100%" height="100%">
        </div>
     </v-col> -->
     <v-col  cols="12" sm="1" md="1" lg="1" xl="1">
        <v-checkbox
          v-model="Fukushima"
          label="福島"
        ></v-checkbox>
     </v-col>
   </v-row>
<v-row>
    
    <!-- <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="NishioHP == true"> -->

    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="Nishio == true">
      <compMachineHP name="MC024"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="Nishio == true">
      <compMachineHP name="MC026"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="Nishio == true">
      <compMachineHP name="MC027"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="Nishio == true">
      <compMachineHP name="MC028"/>
    </v-col>
    
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="Nishio == true">
      <compMachineHP name="LNB035"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"  v-show="NishioHP == true">
      <compMachineHP name="MC031"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="NishioHP == true">
      <compMachineHP name="EX124"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="NishioHP == true">
      <compMachineHP name="MC037"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2"   v-show="NishioHP == true">
      <compMachineHP name="LN034"/>
    </v-col>

     <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="Fukushima == true">
      <compMachineHP name="MC009"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="Fukushima == true">
      <compMachineHP name="MC010"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="Fukushima == true">
      <compMachineHP name="MC011"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="Fukushima == true">
      <compMachineHP name="MC013"/>
    </v-col>
    <!-- <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="Fukushima == true">
      <compMachineHP name="GT999"/>
    </v-col> -->
</v-row>
 </dir>
</template>


<script src="./main.js">

</script>