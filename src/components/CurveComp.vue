<template>
    <div class="wrap-svg"></div>
</template>

<script>
import * as d3 from "d3"
export default {
  data() {
    return {
      rotate: -9,
      valX: null,
      rect: null
    }
  },
  props: ['valCurve', 'activeDot'],
  computed:{
    getRotate() {
      return this.rotate
    }
  },
  watch: {
    valCurve: function(val) {
      this.rect
        .attr("x", 440)
        .attr("transform", `rotate(9.1, 50, 6)`)
        .attr('y', -44)
    },
    activeDot:function(val) {
      let vm = this
      function setValThumb(x, y, transform) {
        return vm.rect
                .attr("x", x)
                .attr("y", y)
                .attr("transform", transform)
      }
      switch (val) {
        case 1: return setValThumb(10, 24, `rotate(-9, 66, 66)`)
          break;
        case 2: return setValThumb(175-50, 20.20, `rotate(-4.8, 50, 6)`)
          break;
        case 3: return setValThumb(310, -12.72, `rotate(4.14, 50, 6)`)
          break;
        case 4: return setValThumb(440, -44, `rotate(9.1, 50, 6)`)
          break;
      }
    }
  },
  mounted() {
    let vm = this

    let points = []

    let size = 0

    for(let x = 10; x <= 540; x++) {
      size++;
      points.push({
        x: x,
        y: 40 - 28*Math.sin((Math.PI/540)*x),
        angleInRadians: ''
      })
    }
    
    let angle = 0
    
    for(let k = 0; k < size-1; k++) {
      if((points[k+1].x-points[k].x) != 0) {
        angle = Math.atan( (points[k+1].y-points[k].y) / (points[k+1].x-points[k].x) )
      }

      points[k].angleInRadians = angle
    }
    
    let width = 550, height = 60
    
    let svg = d3.select('.wrap-svg').append('svg')
      .attr('width', width).attr('height', height)
      .style('background', '#ffffff')
    
    let line = d3.line()
      .x(function(d) {return d.x})
      .y(function(d) {return d.y})
      .curve(d3.curveCardinal);
    
    let path = svg.append('path')
      .attr('d', line(points))
      .style('fill', 'none')
      .style('stroke', '#b1b1b1')
      .style('stroke-width', 1);

    let rect = vm.rect = svg.append('rect')
      .attr('width', 100)
      .attr('height', 11)
      .attr('rx', 5)
      .attr('ry', 5)
      .attr('x', 1)
      .attr('y', 25.8)
      .attr("transform", `rotate(${vm.getRotate}, 50, 6)`)
      .style('fill', '#4350ce');

    svg.select('rect')
      .call(d3.drag()
        .on("start", dragstarted)
        .on("drag", dragged)
        .on("end", dragended));
    
    let deltaX

    function dragstarted() {
      var current = d3.select(this);
        deltaX = current.attr("x") - d3.event.x;
    }

    function dragged() {
        vm.valX = d3.event.x + deltaX + 50
        let valX = vm.valX
        vm.$emit('valx', valX)

        let currentValues

        points.forEach(el => {
            el.x == valX ? currentValues = el : ''
        });
        d3.select(this)
          .attr("x", function() {
            if(currentValues) {
              if(currentValues.x < 60) {
                return 5
              } else if(currentValues.x >= 60 && currentValues.x < 492) {
                return currentValues.x - 50
              } else {
                  return 442
              }
            } else {
              if(valX < 100) {
                return -1
              } else {
                return 442
              }
            }
          })
          .attr("y", function() {
            if(currentValues) {
              return currentValues.y - 6
            } else {
              if(valX < 100) {
                return 25.5
              } else {
                return 33.5
              }
            }
          })
          .attr('transform', function() {
            if(currentValues) {
              let angleInDegrees = currentValues.angleInRadians*180/Math.PI
              if(currentValues.angleInRadians) {
                return `rotate(${angleInDegrees}, ${currentValues.x}, ${currentValues.y})`
              } else {
                return `rotate(9.21, 538, 39)`
              }
            }
             else {
              if(valX < 100) {
                return `rotate(-9, 50, -6)`
              } else {
                return `rotate(9.21, 538, 39)`
              }
            }
          })
    }
    function dragended() {

    }
  }
}
</script>

<style>
  
</style>