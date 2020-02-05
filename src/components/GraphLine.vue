<template>
  <div class="GraphLine">
    
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
            fill: '#33cc3355',
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
          }">
          
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
  
    };
  },
  props: {
    points:{},
    list:{},
    height:Number,
    width:Number,
    disVerLine:Number,
    onePixel:Number
  },
  methods:{
      
  },
  mounted(){
   
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
