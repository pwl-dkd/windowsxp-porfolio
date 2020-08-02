<template>
  <div id="desktop">
    <div class="column" v-for="columnIndex in columns">
      <div class="row" v-for="rowIndex in rows" :class="{'filled' : applications.filter(a => a.x === rowIndex && a.y === columnIndex).length}">
        <template v-for="(app,index) in applications">
          <Icon v-if="app.y === columnIndex && app.x === rowIndex" :key="app.name" :appName="app.name" :iconName="app.icon"/>
        </template>
      </div>
    </div>
  </div>
</template>

<script>

import Icon from '../components/Icon'


export default {
  name: 'Desktop',
   components: {
    Icon,
  },
  methods: {
    moveApp(name,x,y){
      let places = document.querySelectorAll('#desktop .column .row');
      let myPosition = {x,y}
      let destinations = [];
      for( let i = 0; i < places.length; i++){
        destinations.push({
          open: !places[i].classList.contains('filled'),
          x: places[i].offsetLeft + places[i].offsetWidth/2,
          y: places[i].offsetTop + places[i].offsetHeight/2,
        })
      }
      console.log(destinations);

      function DistSquared(pt1, pt2) {
        var diffX = pt1.x - pt2.x;
        var diffY = pt1.y - pt2.y;
        return (diffX*diffX+diffY*diffY);
      }

      let closest = destinations[Math.floor(Math.random()*this.columns*this.rows)];
      let index = -1;
      let shortestDistance = DistSquared(myPosition, destinations[0]);
      for (let i = 0; i < destinations.length; i++) {
        var d = DistSquared(myPosition, destinations[i]);
        if (d < shortestDistance && destinations[i].open) {
          closest = destinations[i];
          index = i;
          shortestDistance = d;
        }
      }
      
      let column = index%this.rows;
      let row = (index-column) / this.rows;
      let newSpot = {
          row,
          column
        };

      let app = this.applications.find(app => app.name === name);
      app.x = newSpot.column + 1;
      app.y = newSpot.row + 1;
    },
  },
  data() {
    return {
      rows: 24,
      columns: 7,
      applications: [
        {
          name: "Chrome",
          icon: "Chrome",
          x: 1,
          y: 1
        },
        {
          name: "Pornhub",
          icon: "Chrome",
          x: 8,
          y: 2
        },
        {
          name: "Firefox",
          icon: "Firefox",
          x: 5,
          y: 2
        }
      ],
    }
  }

}
</script>

<style lang="scss">
#desktop{
  height:96vh;
  width:100vw;
  background-image: url(~@/assets/images/backgrounds/desktop_wallpaper.jpg);
  background-size: cover ;
  display: flex;
  flex-direction: column;
  .column{
    flex: 1;
    display: flex;
  }
  .row{
    box-shadow: inset black 0 0 1px;
    flex: 1;
  }
}
</style>
