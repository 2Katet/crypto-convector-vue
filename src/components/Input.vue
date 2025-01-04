<template>
  <input min="0" type="number" @input="changeAmount($event.target.value)"><br>
  <button @click="convert()">Конвертировать</button>
  <button @click="favourite()" className='fuv-button'>В избранное</button>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true
    },
    convert: {
      type: Function,
      required: true
    },
    favourite: {
      type: Function,
      required: true
    }
  }
}
</script>

<style scoped>
input {
  /* text-align: center; */
  border-radius: 3px;
  border: 0;
  padding: 12px;
  background: #fafafa;
  color: #333;
  outline: none;
  width: 500px;
  position: relative;
  top: -50px;
  font-size: 1.2em;
}

button {
  position: relative;
  top: -20px;
  padding: 15px 20px;
  color: #fff;
  text-transform: uppercase;
  cursor: pointer;
  background: #1a032d;
  border: 0;
  border-radius: 3px
}

.fuv-button {
  margin-left: 20px;
}
</style>