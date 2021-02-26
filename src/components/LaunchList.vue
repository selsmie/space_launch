<template>
<div>
  <h2 v-if='launches.length > 0' id='number'>Number of Launches: {{launches.length}}</h2>
  <ul>
    <launch-list-item v-for='(launch, index) in launches' :key='index' :launch='launch'></launch-list-item>
  </ul>
</div>
 
</template>

<script>
import LaunchListItem from './LaunchListItem'

export default {
    name: 'launch-list',
    props: ['launches'],
    components: {'launch-list-item': LaunchListItem}
}
</script>

<style>

ul {
  height: 80vh;
  overflow: auto;
  margin: 0;
}

ul::-webkit-scrollbar {
  display: none;
}

#number {
  padding-left: 40px;
}

</style>