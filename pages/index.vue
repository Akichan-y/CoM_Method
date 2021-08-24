<template>
 <dir>
   <v-row>

    <h1>{{message}}</h1>
    <h2>{{getTest}}</h2>
    <h2>{{getGenzaiJikan}}</h2>
    <h2>{{getKeikaJikan}}</h2>

   </v-row>
<v-row>
    
    <!-- <v-col cols="12" sm="6" md="4" lg="3" xl="2" v-show="NishioHP == true"> -->

    <v-col cols="12" sm="6" md="4" lg="3" xl="2">
      <compMachineHP name="MC031"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2">
      <compMachineHP name="EX124"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2">
      <compMachineHP name="MC037"/>
    </v-col>
    <v-col cols="12" sm="6" md="4" lg="3" xl="2">
      <compMachineHP name="LN034"/>
    </v-col>
</v-row>
 </dir>
</template>


<script src="./main.js">

</script>