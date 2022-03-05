<template>
    <!-- <img alt="pic" width =100px  src="public\src_pic.jpg"> -->
    <!--<img id = "pic" alt="pic" src="src_pic.jpg">-->
    <div id="my_dataviz"></div>

</template>


<script>
import * as d3 from 'd3'
export default ({
    name : 'graph',
    data(){
        return{
        }
    },
    mounted() {
        const margin = {top: 10, right: 10, bottom: 10, left: 10},
        width = 460 - margin.left - margin.right,
        height = 460 - margin.top - margin.bottom,
        innerRadius = 80,
        outerRadius = Math.min(width, height) / 2;   
        const svg = d3.select("#my_dataviz")
            .append("svg")
              .attr("width", width + margin.left + margin.right)
              .attr("height", height + margin.top + margin.bottom)
            .append("g")
              .attr("transform", `translate(${width/2},${height/2+100})`); 
        var data = []
        var max = 0
        data.push(0)
        for(let i in this.data_time){
            if(max<this.data_time[i]){
                max = this.data_time[i]
            }
            data.push(this.data_time[i])
        }
        data.push(0)
        data.push(0)
        for(let i in this.data_dif){
            if(max<this.data_dif[i]){
                max = this.data_dif[i]
            }
            data.push(this.data_dif[i])
        }
        data.push(0)
        var list = []
        for(var i in data){
          list.push({num:i,Value:String(data[i])})
        }
        const x = d3.scaleBand()
            .range([1.5*Math.PI, 3.5*Math.PI])    
            .align(1)                 
            .domain( list.map(d => d.num)); 
        const y = d3.scaleRadial()
            .range([innerRadius, outerRadius])   
            .domain([0, 1]); 
        const color = d3.color()
        svg.append("g")
            .selectAll("path")
            .data(list)
            .join("path")
            .attr("d", d3.arc()   
                .innerRadius(innerRadius)
                .outerRadius(d => y(d['Value']))
                .startAngle(d => x(d.num))                    
                .endAngle(d => x(d.num) + 0.9*x.bandwidth())
                .padAngle(0.01)
                .padRadius(innerRadius))
            .attr("fill", "#69b3a2")
            .style("opacity",function(d){ return d['Value']/max})

    },
    props:{
        data_time: [],
        data_dif:[]
    }
})
</script>


<style scoped>

#pic{
    position:absolute;
    left:212px;
    right:200px;
    top:238px;
    bottom:200px;
    width:160px;
    height:160px;
    border-radius:100%;
    border-style:solid;
    opacity: 70%;
    
}
#my_dataviz{
    position:absolute;
    left:75px;
    right:200px;
    top:0px;
    bottom:200px;
    width:200px;
    height:200px;
    background: white;
}


</style>