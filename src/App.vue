<script>
import inputTag from "./components/InputTag.vue"

export default {
  components: {
    inputTag
  },
  methods: {
    //Cada vez que haya un cambio en el estado del array se va a reflejar
    handleOnTagsChange(tags){
      console.log(tags)
    }
  }
}
</script>

<template>
  <inputTag :onTagsChange="handleOnTagsChange" />
</template>

<style>
body {
  font-family: 'Courier New', Courier, monospace;
  padding: 0;
  margin: 0;
}
</style>
