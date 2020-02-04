<template>
  <div class="graficPage">
    <div class="grafic">
      <v-stage 
      :config="configKonva"
       @dragstart="handleDragstart"
        @dragend="handleDragend"
        @dragmove="handleDragmove"
      >
      
        <v-layer>
          <v-line 
          v-for="line in 10"
          :key="line"
          :config="{    
            x: 0,
            y: 0,
            points: [(width/horisontalPoints)*line,0,(width/horisontalPoints)*line,height],
            tension: 0.5,
            closed: false,
            stroke: '#888',
            draggable: false,
            strokeWidth: 1
            }"
          >
          </v-line>
            </v-layer>
       <v-layer>
          <v-line 
          v-for="line in 10"
          :key="line"
          :config="{    
            x: 0,
            y: 0,
            points: [0,(height/10)*line,width,(height/10)*line],
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
          :points="points"
          :list="list"
          :width="width"
          :height="height"
          :disVerLine="disVerLine"
          
          ></GraphLine>
      </v-stage>
    </div>
    <button @click="renderLine">DrawGrafic</button>
    <div class="statusInfo">
    <p>configCircle:<span>{{configCircle}}</span></p>
    <p>configCircle x-y:<span>{{configCircle.x}} - {{configCircle.y}}</span></p>
    <p>points:<span>{{points}}</span></p>
    <p>list:<span>{{list}}</span></p>
    <p>horisontalPoints:<span>{{horisontalPoints}}</span></p>
    <p>disVerLine:<span>{{disVerLine}}</span></p>
    
    </div>
  </div>
</template>

<script>
import GraphLine from './GraphLine.vue'
export default {
  name: 'Graph',
 
  data() {
    
    return {
      width: 600,
      height: 400,
      list:[],
      points:[],
      horisontalPoints:Number,
      distanceVerticalLine:Number,
       configKonva: {
         width: 600,
         height: 400
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
      renderLine(){
        if(this.points.length>1){
        this.points=[];
        }
        for(let i in this.list){
          this.points.push(i*this.disVerLine);
          this.points.push(this.height-this.list[i]);
        }
      },
      handleDragstart(){
      },
      handleDragend(){

      },
      handleDragmove(e){
         
          this.list[e.target.index]=this.height-e.target.attrs.y;
          this.renderLine()
      }
  },
  mounted(){
    this.list=this.graphics;
    this.horisontalPoints=this.list.length-1;
    this.disVerLine=this.configKonva.width/this.horisontalPoints;
    this.renderLine()
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
