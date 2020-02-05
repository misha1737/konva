<template>
  <div class="GraphLine" >
      <v-layer
       :config="{
            x:40,
            y:10
          }">
          <v-line v-if="points.length>0"
          :config="{    
            x: 0,
            y: 0,
            points: points,
            tension: 0,
            closed: true,
            stroke: 'black',
            draggable: false,
            fill: '#33cc3388',
            strokeWidth: 1
            //opacity: 0.3
            }"
          >
          </v-line>
      </v-layer>
        <v-layer
         :config="{
            x:40,
            y:10
          }"
        @dragstart="handleDragstart"
        @dragend="handleDragend"
        @dragmove="handleDragmove"
          >
          
          <v-circle 
          v-for="(item, state) in list"
          :key="state"
          :config='{
            x:state*disVerLine,
            y:height-(item*onePixel),
            draggable: true,
            id:item.id,
            dragBoundFunc: function(pos) {
              
              if(pos.y<10 || pos.y>height+10){
                return{
                  x: this.absolutePosition().x,
                  y: this.absolutePosition().y,
                }
              }
              return {
                x: this.absolutePosition().x,
                y: pos.y
              };
            },
            radius: 5,
            fill: "green",
            stroke: "black",
            strokeWidth: 1
          }'
          ></v-circle>
         
        </v-layer>


    </div>

</template>

<script>
export default {
  
  name: 'HelloWorld',
 
  data() {
    
    return {
     points:[]
    };
  },
  props: {

    list:{},
    height:Number,
    width:Number,
    disVerLine:Number,
    onePixel:Number
  },
  methods:{
     renderLine(){
        if(this.points.length>1){
        this.points=[];
        }
        for(let i in this.list){
          this.points.push(i*this.disVerLine);
          this.points.push(this.height-this.list[i]*this.onePixel);
        }
        this.points.push(this.width);
        this.points.push(this.height);
        this.points.push(0);
        this.points.push(this.height);
        //this.$emit('update:points', this.points)

      },
        handleDragstart(){
         
      },
      handleDragend(e){
           this.list[e.target.index]=(this.height-e.target.attrs.y)/this.onePixel;
          this.renderLine();
         
      },
      handleDragmove(){
         
          
      }
  },
  mounted(){

 


  },
  created(){
    setTimeout(()=>{
      this.renderLine();
    },0)
     
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
