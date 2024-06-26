<!-- Pedidos.svelte -->
<script>
  export let pedidos = [];
</script>

<div class="w-full">
  <table class="min-w-full border-collapse">
    <thead>
      <tr>
        <th class="border p-2">ID</th>
        <th class="border p-2">Precio Total</th>
        <th class="border p-2">Productos Pedidos</th> <!-- Nueva columna -->
      </tr>
    </thead>
    <tbody>
      {#each pedidos as pedido}
        <tr>
          <td class="border p-2">{pedido.id}</td>
          <td class="border p-2">${pedido.precio.toFixed(2)}</td>
          <td class="border p-2">
            <ul>
              {#each pedido.productosPedidos as producto}
                <li>{producto.nombre} - ${producto.precio.toFixed(2)}</li>
              {/each}
            </ul>
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

