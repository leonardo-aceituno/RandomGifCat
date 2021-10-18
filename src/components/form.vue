<template>
  <div class="row d-flex justify-content-evenly ">
    <div class="col-5 border p-5 bg-white">
      <h2 class="mb-4">Random Gif-Cat</h2>

      <div class="alert alert-danger" v-show="muestraError" role="alert">
        tienes campos sin completar...
      </div>
      <form>
        <div class="row mb-3">
          <label for="titulo" class="col-sm-2 col-form-label">Titulo</label>
          <div class="col-sm-10">
            <input
              type="text"
              class="form-control"
              id="titulo"
              v-model="titulo"
            />
          </div>
        </div>

        <div class="row mb-3">
          <label for="filtro" class="col-sm-2 col-form-label">Filtro</label>
          <div class="col-sm-10">
            <select
              class="form-select"
              id="filtro"
              v-model="filtroSeleccionado"
            >
              <option selected>Seleccione...</option>
              <option
                v-for="(filtro, index) in filtros"
                :key="index"
                :value="filtro.nombre"
                >{{ filtro.nombre }}</option
              >
            </select>
          </div>
        </div>

        <div class="row mb-3 d-flex justify-content-between">
          <label for="color" class="col-sm-2 col-form-label">Color</label>
          <div class="col-sm-8">
            <select
              class="form-select"
              id="color"
              @change="colorSeleccionado($event)"
              v-model="miColor"
            >
              <!-- v-model="colorSeleccionado"  -->
              <option selected>Seleccione...</option>
              <option
                v-for="(color, index) of colores"
                :key="index"
                :value="color.valor"
                >{{ color.nombre }}</option
              >
            </select>
          </div>
          <div class="col-sm-2 d-flex justify-content-end">
            <div
              class="border circulo"
              :style="{ 'background-color': miColor }"
            ></div>
          </div>
        </div>

        <div class="row mb-3">
          <label for="tamano" class="col-sm-2 col-form-label">Tamaño</label>
          <div class="col-sm-10">
            <input
              type="number"
              class="form-control"
              id="tamano"
              v-model.number="tamano"
            />
          </div>
        </div>

        <div class="row mb-3">
          <div class="col d-flex justify-content-end">
            <button type="button" class="btn btn-warning" @click="gatito">
              Obtener mi Cat
            </button>
          </div>
        </div>
      </form>
    </div>
    <div
      class="col-5 border p-5"
      v-show="mostrar"
      :style="{ 'background-color': miColor }"
    >
      <img class="w-100" :src="imagenGato" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: "formulario",

  data() {
    return {
      filtros: [
        { id: 0, nombre: "blur" },
        { id: 1, nombre: "mono" },
        { id: 2, nombre: "sepia" },
        { id: 3, nombre: "negative" },
        { id: 4, nombre: "paint" },
        { id: 5, nombre: "pixel" },
      ],
      colores: [
        { id: 0, nombre: "Amarillo", valor: "yellow" },
        { id: 1, nombre: "Naranjo", valor: "orange" },
        { id: 2, nombre: "Azul", valor: "blue" },
        { id: 3, nombre: "Rosado", valor: "pink" },
        { id: 4, nombre: "Verde", valor: "green" },
      ],
      imagenGato: "",
      titulo: "",
      mostrar: false,
      miColor: "",
      filtroSeleccionado: "",
      tamano: "",
      muestraError: false,
    };
  },

  methods: {
    gatito() {
      if (
        !this.titulo ||
        !this.filtroSeleccionado ||
        !this.miColor ||
        !this.tamano
      ) {
        return (this.muestraError = true);
      } else {
        this.imagenGato = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtroSeleccionado}&color=${this.miColor}&size=${this.tamano}`;
        console.log(this.imagenGato);
        this.mostrar = true;
        this.muestraError = false;
      }
    },
    colorSeleccionado(event) {
      console.log(event.target.value);
      this.miColor = event.target.value;
    },
    validar() {
      if (this.titulo == "") {
        alert("Completar campos obligatorios");
      }
    },
  },
};
</script>

<style>
img {
  width: 440px;
  height: 320px;
}

.circulo {
  width: 40px;
  height: 100%;
  border-radius: 50%;
  /* background: #5cb85c; */
}
</style>
