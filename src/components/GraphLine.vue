<template>
  <div class="GraphLine">
      <v-layer>
          <v-line v-if="points.length>0"
          :config="{    
            x: 0,
            y: 0,
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
          v-for="(item, state) in list"
          :key="item.id"
          :config='{
            x:state*40,
            y:height-item.y,
            draggable: true,
            id:item.id,
            dragBoundFunc: function(pos) {
              if(pos.y<0 || pos.y>height){
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
            fill: "red",
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
    points:[],
    list:[],
    height:Number,
    width:Number
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
