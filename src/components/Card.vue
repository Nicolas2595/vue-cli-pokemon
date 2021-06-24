<template>
  <li>
      <a
      target="_blank" 
      :href="element.url"
      >
      <img 
      v-if="element.img"
      :src="element.img" 
      :alt="element.name">
      <h2>{{ element.name }}</h2>
      </a>
  </li>
</template>

<script>
export default {
    name: "Card",
    props: {
        element: {
            type: Object
        }
        // name: {
        //     type: String,
        // },
        // url: {
        //     type: String,
        // }
    }
}
</script>

<style lang="scss" scoped>

li {
    list-style: none;
    width: calc(25% - 10px);
    margin: 5px;
    background-color: #ffcc01;
    padding: 5px;
    text-align: center;
    border-radius: 30px;

        a {
            text-decoration: none;
            color: #3d5ea5;
        }

        img {
            width: 60%;
            margin-bottom: 20px;
        }
}

</style>