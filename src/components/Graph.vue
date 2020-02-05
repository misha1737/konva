<template>
  <div class="graficPage">
    <div class="grafic">
      <v-stage 
      :config="configKonva"
    
      >
      
        <v-layer
          :config="{
            x:40,
            y:10
          }"
          >
          <v-text 
          v-for="(textInfo,index) in horisontalPoints"
          :key="index.id"
           :config="{
             x:  textInfo*disVerLine-disVerLine-10,
             y: height+10,
             text: textInfo-1,
            fontSize: 10
            }"
           >
           </v-text>

           <v-text 
          v-for="textInfo in 10"
          :key="textInfo.id"
           :config="{
             x: -55,
             y: ((textInfo-1)*height/10)-5,
             width:50,
             text: maxRange-Math.trunc(maxRange/10)*(textInfo-1),
            fontSize: 10,
            align:'right'
            }"
           >
           </v-text>

          <v-line 
          v-for="(line, index) in horisontalPoints"
          :key="index"
          :config="{    
            x: 0,
            y: 0,
            points: [disVerLine*(line-1),0,disVerLine*(line-1),height],
            tension: 0.5,
            closed: false,
            stroke: '#888',
            draggable: false,
            strokeWidth: 1,
            ZIndex:500
            }"
          >
          </v-line>
            </v-layer>
       <v-layer
        :config="{
            x:40,
            y:10
          }">
          
          <v-line 
          v-for="line in 11"
          :key="line"
          :config="{    
            x: 0,
            y: 0,
            points: [0,(height/10)*(line-1),width,(height/10)*(line-1)],
            tension: 0.5,
            closed: false,
            stroke: '#888',
            draggable: false,
            strokeWidth: 1
            }"
          >
          </v-line>
         
       </v-layer>
         <GraphLine 
          v-for="graph in list"
          :key="graph.id"
          :list="graph"
          :width="width"
          :height="height"
          :disVerLine="disVerLine"
          :onePixel="onePixel"
          ></GraphLine>
      </v-stage>
    </div>
    <div class="statusInfo">
    <p>list:<span>{{list}}</span></p>
    <p>horisontalPoints:<span>{{horisontalPoints}}</span></p>
    <p>disVerLine:<span>{{disVerLine}}</span></p>
    <p>onePixel:<span>{{onePixel}}</span></p>
    
    
    </div>
  </div>
</template>

<script>
import GraphLine from './GraphLine.vue'
export default {
  name: 'Graph',
 
  data() {

    return {
      width: 800,
      height: 400,
      maxRange:800,
      onePixel:1,
      list:[],
      horisontalPoints:Number,
      distanceVerticalLine:Number,
      disVerLine:0,
       configKonva: {
         width: 850,
         height: 450
       },
      configCircle: {
        x: 100,
        y: 100,
        draggable: true,
        radius: 5,
        fill: "red",
        stroke: "black",
        strokeWidth: 1
      },
      configLine:{
   
      }
    };
  },
   components: {
    GraphLine
  },
  props: {
    msg: String,
    graphics: {}
  },
  methods:{
     

  },
  mounted(){
    this.list=this.graphics;
    this.horisontalPoints=this.list[0].length;
    this.disVerLine=this.width/(this.horisontalPoints-1);
    this.onePixel=this.height/this.maxRange;
    
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.graficPage{
  .grafic{
   
    
    //width:300px;
   // height:300px;
    background:#eee;
    display:inline-block;
  }
  .statusInfo{
    background-color: black;
    padding:40px;
    text-align: left;
    p{
      color:white;
      span{
        color:greenyellow;
      }
    }
  }
}
</style>
