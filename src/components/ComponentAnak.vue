<template>
  <div class="component-anak">
    <h1>Ini Component Anak</h1>
    <h3>Hasil lempar data : {{ dataAnak }}</h3>
    <button type="button" class="btn btn-info" v-on:click="$emit('data-dari-anak',dataDariAnak)">Mau lempar Klik Aku</button>
    <br />
  </div>
</template>

<script>
export default {
  name: "ComponentAnak",
  props: {
    dataAnak: String
  },
  data() {
    return {
      dataDariAnak: "Ini data dari anak ke ortu"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
