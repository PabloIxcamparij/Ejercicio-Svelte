<!-- Productos.svelte -->
<script>
  export let productos = [];
  export let eliminarProducto;
</script>

<div class="w-full h-4">
  <table class="min-w-full border-collapse">
    <thead>
      <tr>
        <th class="border p-2">ID</th>
        <th class="border p-2">Nombre</th>
        <th class="border p-2">Precio</th>
        <th class="border p-2">Accion</th>
      </tr>
    </thead>
    <tbody>
      {#each productos as producto}
        <tr>
          <td class="border p-2">{producto.id}</td>
          <td class="border p-2">{producto.nombre}</td>
          <td class="border p-2">${producto.precio.toFixed(2)}</td>
          <td class="border p-2">
            <button
              class="bg-red-500 text-white p-2 rounded-lg"
              on:click={() => eliminarProducto(producto.id)}
            >
              Eliminar
            </button>
          </td>
        </tr>
      {/each}
    </tbody>
  </table>


</div>
