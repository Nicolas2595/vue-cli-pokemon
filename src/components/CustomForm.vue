<template>
  <form>
      <input 
        type="text"
        :placeHolder="inputPlaceholder" 
        v-model.trim="searchtext"
      >

      <input 
      type="submit" 
      value="CERCA"
      @click.prevent="$emit('sendForm', searchtext)"
      >
  </form>
</template>

<script>
export default {
    name: "CustomForm",
    data: function() {
        return {
            searchtext: ''
        }
    },
    props: ["inputPlaceholder"],
    methods: {
        
    }
}
</script>

<style lang="scss" scoped>

form {
    margin: 20px 0;
    text-align: center;

    input {
    padding: 5px;
    margin-right: 10px;
    cursor: pointer;

        &[type="text"] {
            width: 300px;
        }
    }
}



</style>