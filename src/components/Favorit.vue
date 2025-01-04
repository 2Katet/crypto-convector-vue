
<template>
  <h2>Варианты в избранном</h2>
  <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<script>
export default {
  props: {
    favs: {
      type: Array,
      required: true
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
    favourite: {
      type: Function,
      required: true,
    }
  }
}
</script>

<style scoped>
h2 {
  color: #fff;
  font-size: 20px;
  font-weight: 500;
  letter-spacing: 3px;
}

div {
  display: flex;
  justify-content: space-between;
  width: 500px;
  margin: 0 auto;
  transition: all 500ms ease;
}
div:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}

span {
  padding: 10px 15px;
  background: #8c00ff;
  color: #fff;
  width: 100px;
  box-shadow: 0px 10px 3px -8px rgba(0,0,0,0.54);
  margin-bottom: 5px;
}


</style>