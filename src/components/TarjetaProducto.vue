<template>
  <div class="card">
    <img class="card-img-top" :src="producto.imagen" />
    <div class="card-body">
      <h5 class="card-title">{{ producto.nombre }}</h5>
      <span>{{ formatearPrecio(producto.precio) }}</span>
      <button @click="agregarAlCarrito(producto)" class="d-block btn btn-outline-primary mt-3">
        Agregar al carrito
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["producto"],
  methods: {
    formatearPrecio(monto) {
      return "S/" + parseFloat(monto).toFixed(2);
    },
    agregarAlCarrito() {
      this.$emit("agregarAlCarrito", this.producto)
    }
  }
}
</script>

<style>

</style>