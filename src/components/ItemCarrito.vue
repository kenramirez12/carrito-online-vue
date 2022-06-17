<template>
  <div class="row align-items-center">
    <div class="col-6">
      <img
        class="img-thumbnail img-cart-item"
        :src="itemCarrito.imagen"
      />
      <span>{{ itemCarrito.nombre }}</span>
    </div>
    <div class="col-6 text-end">
      <span class="precio fw-bold">
        {{ formatearPrecio(itemCarrito.totalCarrito) }}
      </span>
      <span class="cantidad fst-italic">
        ({{ itemCarrito.cantidad }} und)
      </span>
      <button
        @click="eliminarItemCarrito"
        class="btn btn-outline-danger btn-sm ms-2"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["itemCarrito"],
  methods: {
    formatearPrecio(monto) {
      return "S/" + parseFloat(monto).toFixed(2);
    },
    eliminarItemCarrito() {
      this.$emit("eliminarItemCarrito", this.itemCarrito.id);
    }
  }
}
</script>

<style>

</style>