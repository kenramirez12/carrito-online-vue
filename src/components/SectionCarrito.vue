<template>
  <section class="container">
    <div class="card">
      <div class="card-header fw-bold">🛒 Carrito de compras</div>
      <p v-if="carrito.length === 0" class="pt-3 px-3">
        Aún no has agregado productos al carrito.
      </p>
      <ul v-else class="list-group list-group-flush">
        <li
          v-for="itemCarrito in itemsCarrito"
          :key="itemCarrito.id"
          class="list-group-item"
        >
          <ItemCarrito
            :itemCarrito="itemCarrito"
            @eliminarItemCarrito="eliminarItemCarrito"
          />
        </li>
      </ul>
    </div>
    <div class="row mt-3">
      <div class="col-12 text-end">
        <span class="fw-bold fs-5">
          Total {{ formatearPrecio(totalCarrito) }}
        </span>
        <button class="btn btn-lg btn-primary ms-2">
          Comprar
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import ItemCarrito from "./ItemCarrito.vue";

export default {
  props: ["carrito"],
  components: {
    ItemCarrito
  },
  computed: {
    itemsCarrito() {
      if (this.carrito.length === 0) return [];
      return this.carrito.map((itemCarrito) => ({
        ...itemCarrito,
        totalCarrito: itemCarrito.precio * itemCarrito.cantidad,
      }));
    },
    totalCarrito() {
      if (this.itemsCarrito.length === 0) return 0;
      let total = 0;
      this.itemsCarrito.forEach((item) => {
        total += item.totalCarrito;
      });
      return total;
    },
  },
  methods: {
    formatearPrecio(monto) {
      return "S/" + parseFloat(monto).toFixed(2);
    },
    eliminarItemCarrito(itemCarritoId) {
      this.$emit("eliminarItemCarrito", itemCarritoId);
    }
  }
}
</script>

<style>

</style>