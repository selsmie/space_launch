<template>
  <ul>
      <h2 v-if='launches.length > 0'>Number of Launches: {{launches.length}}</h2>
      <h5 v-if='launches.length === 0'>Selected filter parameters</h5>
      <launch-list-item v-for='(launch, index) in launches' :key='index' :launch='launch'></launch-list-item>
  </ul>
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

</style>