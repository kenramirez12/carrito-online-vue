<template>
  <div class="py-4">
    <section id="thankyou-page" class="d-none">
      <div class="container py-5 text-center">
        <h1 class="fs-1 fw-bold mb-3">🛒</h1>
        <h1 class="fs-3 fw-bold mb-3">¡Gracias por tu compra!</h1>
        <p>En breve recibirás tu pedido en la puerta de tu casa.</p>
        <a href="index.html" class="btn btn-lg btn-primary">
          Volver al carrito
        </a>
      </div>
    </section>
    <section id="checkout" class="d-none">
      <div class="container pb-3">
        <div class="w-100 pt-2 pb-4 px-3 bg-white rounded border">
          <div class="d-flex align-items-center justify-content-between">
            <h1 class="fs-5 mb-0">¿Listo para comprar?</h1>
            <button
              id="volver-carrito-boton"
              type="button"
              class="btn btn-link"
            >
              Volver al carrito
            </button>
          </div>
          <hr class="mt-1 mb-5" />
          <form action="#">
            <div class="row">
              <div class="col-8 border-end">
                <div class="row gy-3">
                  <div class="col-12">
                    <h5 class="fw-semibold">Información del cliente</h5>
                  </div>
                  <div class="col-6">
                    <label for="">Nombres completos</label>
                    <input id="nombres" type="text" class="form-control" />
                  </div>
                  <div class="col-6">
                    <label for="">Dirección</label>
                    <input id="direccion" type="text" class="form-control" />
                  </div>
                  <div class="col-6">
                    <label for="">Correo electrónico</label>
                    <input id="correo" type="text" class="form-control" />
                  </div>
                  <div class="col-6">
                    <label for="">Número de teléfono</label>
                    <input id="telefono" type="tel" class="form-control" />
                  </div>
                </div>
              </div>
              <div class="col-4">
                <h5 class="fw-semibold mb-3">Resumen de la compra</h5>
                <div
                  class="
                    mb-3
                    text-center
                    d-flex
                    align-items-center
                    justify-content-between
                  "
                >
                  <span class="fw-bold">Total:</span>
                  <span id="total-checkout" class="fw-bold fs-5">S/0.00</span>
                </div>
                <hr />
                <h5 class="fw-semibold mb-3">Métodos de pago</h5>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="flexRadioDisabled"
                    id="flexRadioDisabled"
                  />
                  <label class="form-check-label" for="flexRadioDisabled">
                    Tarjeta de crédito/débito
                  </label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="flexRadioDisabled"
                    id="flexRadioCheckedDisabled"
                  />
                  <label
                    class="form-check-label"
                    for="flexRadioCheckedDisabled"
                  >
                    Transferencia bancaria
                  </label>
                </div>
                <button
                  id="realizar-pedido-boton"
                  type="submit"
                  class="btn btn-lg btn-primary w-100 mt-3"
                >
                  Realizar pedido
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </section>
    <SectionCarrito
      :carrito="carrito"
      @eliminarItemCarrito="eliminarItemCarrito"
    />
    <section id="productos">
      <div class="container mt-5">
        <ul class="row gy-4">
          <div v-for="producto in productos" :key="producto.id" class="col-3">
            <TarjetaProducto
              :producto="producto"
              @agregarAlCarrito="agregarAlCarrito"
            />
          </div>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
import SectionCarrito from "./components/SectionCarrito.vue";
import TarjetaProducto from "./components/TarjetaProducto.vue";

const PRODUCTOS = [
  {
    id: 1,
    nombre: "Producto #1",
    precio: "10.00",
    imagen: "/imagenes/producto.png",
  },
  {
    id: 2,
    nombre: "Producto #2",
    precio: "4.50",
    imagen: "/imagenes/producto.png",
  },
  {
    id: 3,
    nombre: "Producto #3",
    precio: "4.50",
    imagen: "/imagenes/producto.png",
  },
  {
    id: 4,
    nombre: "Producto #4",
    precio: "43.00",
    imagen: "/imagenes/producto.png",
  },
  {
    id: 5,
    nombre: "Producto #5",
    precio: "43.00",
    imagen: "/imagenes/producto.png",
  },
];

export default {
  name: "App",
  components: {
    SectionCarrito,
    TarjetaProducto,
  },
  data() {
    return {
      productos: PRODUCTOS,
      carrito: [],
    };
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
    agregarAlCarrito(producto) {
      const itemCarrito = this.carrito.findIndex(
        (itemCarrito) => itemCarrito.id === producto.id
      );
      if (itemCarrito === -1) {
        this.carrito.push({ ...producto, cantidad: 1 });
      } else {
        this.carrito[itemCarrito].cantidad += 1;
      }
    },
    eliminarItemCarrito(productoId) {
      this.carrito = this.carrito.filter((item) => item.id !== productoId);
    },
  },
};
</script>

<style>
ul {
  padding-left: 0;
}

.img-cart-item {
  width: 38px;
  margin-right: 0.5rem;
}
</style>
