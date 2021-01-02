<script>
  import Product from "./Product.svelte";
  import Modal from "./Modal.svelte";

  let products = [
    {
      id: "p1",
      title: "A book",
      price: 9.99
    }
  ];

  let showModal = false;
  let closeable = false;

  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }
</script>

{#each products as product}
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<button on:click={() => (showModal = true)}>Show Modal</button>

{#if showModal}
  <Modal
    on:cancel={() => (showModal = false)}
    on:close={() => (showModal = false)}
	let:didAgree={closeable}>
    <h1 slot="header">Hello!</h1>
    <p>This works!</p>
    <button slot="footer" on:click={() => (showModal = false)} disabled={!closeable}>Confirm</button>
  </Modal>
{/if}
