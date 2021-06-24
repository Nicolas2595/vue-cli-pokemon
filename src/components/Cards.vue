<template>
  <ul>
      <!-- <li v-for="item in items"
      :key="item.url"
      >
      {{ item.name }}
      </li> -->

      <Card 
      v-for="item in items"
      :key="item.url"
      :element="item"
      />
  </ul>
</template>

<script>

import Card from '../components/Card'

export default {
    name: "Cards",
    props: {
        items: {
            type: Array,
        }
    },
    components: {
        Card
    }
}
</script>

<style lang="scss" scoped>

ul {
    display: flex;
    flex-wrap: wrap;    
}

</style>