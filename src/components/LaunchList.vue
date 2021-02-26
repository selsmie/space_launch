<template>
  <ul>
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