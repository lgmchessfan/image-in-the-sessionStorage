<template>
  <div id="app">
    <input type="file" accept="image/*;capture=camera" @input="signalChange" />
    <br />
    <button @click="muestralo">Presiona para mostrar imagen!!!</button>
    <button @click="borraSESS">Borrar session</button>
    <button @click="borraIMG">Borrar Imagen</button>
    <hr />
    <img id="output" width="250px" />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {};
  },

  methods: {
    muestralo: function() {
      if (sessionStorage.imagen) {
        var output = document.getElementById("output");
        var file = JSON.parse(sessionStorage.imagen);
        output.src = file.dataURL;
      } else {
        alert("No hay imagen cargada!");
      }
    },
    borraSESS() {
      sessionStorage.clear();
    },
    borraIMG() {
      var output = document.getElementById("output");
      output.src = null;
    },
    signalChange: function(evt) {
      var element = evt.srcElement;
      var file = element.files[0],
        reader = new FileReader();

      reader.onload = (function() {
        return function(e) {
          file.dataURL = e.target.result;
          //console.log(JSON.stringify(file));

          // var output = document.getElementById("output");
          if (typeof Storage !== "undefined") {
            sessionStorage.imagen = JSON.stringify(file);
          }
          // output.src = file.dataURL;
        };
      })(file);
      reader.readAsDataURL(file);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
