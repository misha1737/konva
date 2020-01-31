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
            points: [0,60*line,width,60*line],
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
          <v-line v-if="points.length>0"
          :config="{    
            x: 0,
            y: 200,
            points: points,
            tension: 0.5,
            closed: false,
            stroke: 'black',
            draggable: false,
            fillLinearGradientStartPoint: { x: -50, y: -50 },
            fillLinearGradientEndPoint: { x: 50, y: 50 },
            fillLinearGradientColorStops: [0, 'red', 1, 'yellow']
            }"
          >
          </v-line>
      </v-layer>
        <v-layer>
          
          <v-circle 
          v-for="item in list"
          :key="item.id"
          :config='{
            x:item.x,
            y:height-item.y,
            draggable: true,
            id:item.id,
            dragBoundFunc: function(pos) {
              return {
                x: this.absolutePosition().x,
                y: pos.y
              };
            },
            radius: 5,
            fill: "red",
            stroke: "black",
            strokeWidth: 1
          }'
          ></v-circle>
          
        </v-layer>
      </v-stage>
    </div>
    <button @click="renderLine">DrawGrafic</button>
    <div class="statusInfo">
    <p>configCircle - <span>{{configCircle}}</span></p>
    <p>configCircle x-y -<span>{{configCircle.x}} - {{configCircle.y}}</span></p>
    <p>points - <span>{{points}}</span></p>
    <p>list - <span>{{list}}</span></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
 
  data() {
    
    return {
      width: 600,
      height: 400,
      list:[{x:50,y:40,id:1},{x:100,y:200},{x:150,y:160,id:3},{x:200,y:240,id:4},{x:250,y:80,id:5},{x:300,y:120,id:6},{x:350,y:140,id:7},{x:400,y:120,id:8}],
      points:[],
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
  props: {
    msg: String
  },
  methods:{
      renderLine(){
        if(this.points.length>1){
        this.points=[];
        }
        for(let i in this.list){
        console.log(this.list[i]);
          this.points.push(this.list[i].x);
          this.points.push(this.height-this.list[i].y-200);
        }
      },
      handleDragstart(){
      },
      handleDragend(){

      },
      handleDragmove(e){
          console.log(e.target.index)
          this.list[e.target.index].y=this.height-e.target.attrs.y;
          this.renderLine()
      }
  },
  mounted(){
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
