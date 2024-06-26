<!-- Main.svelte -->
<script>
  import Productos from "../src/lib/Productos.svelte";
  import Pedidos from "../src/lib/Pedidos.svelte";
  import menu from "./data/menu.json";

  let productos= [];
  let pedidos = [];
  let selectedProducto = null;
  let contadorIdProducto = 1;
  let contadorIdPedido = 1;
  let totalPedido = 0;

  function agregarProducto() {
    if (selectedProducto) {
      const producto = menu.find((item) => item.id === selectedProducto);
      productos = [
        ...productos,
        {
          id: contadorIdProducto,
          nombre: producto.nombre,
          precio: producto.precio,
        },
      ];
      contadorIdProducto++;
      totalPedido += producto.precio;
    }
  }

  function agregarPedido() {
    // Copiar productos actuales para este pedido
    const productosPedidoActual = [...productos];

    // Agregar el pedido con su ID y lista de productos
    pedidos = [
      ...pedidos,
      {
        id: contadorIdPedido,
        precio: totalPedido,
        productosPedidos: productosPedidoActual,
      },
    ];

    contadorIdPedido++;
    totalPedido = 0;
    productos = [];
  }

  function eliminarProducto(id) {
    const producto = productos.find((producto) => producto.id === id);
    totalPedido -= producto.precio;
    productos = productos.filter((producto) => producto.id !== id);
  }

</script>

<div class="p-4">
  <h1 class="text-2xl font-bold m-10">Control de Pedidos</h1>

  <div class="flex gap-10 m-10 flex-col md:flex-row">
    <div class="flex justify-between w-full">
      <select bind:value={selectedProducto} class="border p-2 mr-2 w-full">
        <option value="" disabled selected>Seleccione un producto</option>
        {#each menu as item}
          <option value={item.id}
            >{item.nombre} - ${item.precio.toFixed(2)}</option
          >
        {/each}
      </select>

      <button
        on:click={agregarProducto}
        class="bg-blue-500 text-white p-2 px-10 rounded-lg w-auto"
      >
        Añadir
      </button>
    </div>

    <div class="flex justify-around w-full">
      <h2 class="text-xl font-bold">
        Total: ${totalPedido.toFixed(2)}
      </h2>

      <button
        on:click={agregarPedido}
        class="bg-blue-500 text-white p-2 px-5 rounded-lg"
      >
        Guardar Pedido
      </button>
    </div>
  </div>
<!-- lex gap-10 m-10 flex-col md:flex-row -->
<div class="flex flex-col gap-10 mb-10 mt-10 md:flex-row">
  <div class="w-full flex-grow">
    <div class="mb-10 h-96 md:mb-0 overflow-auto">
      <Productos {productos} {eliminarProducto} />
    </div>
  </div>
  <div class="w-full flex-grow">
    <Pedidos {pedidos} />
  </div>
</div>


  
</div>
