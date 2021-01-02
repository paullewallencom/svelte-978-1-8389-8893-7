<script>
  import Product from "./Product.svelte";
  import CartItem from "./CartItem.svelte";

  let renderedComponent = { cmp: Product, title: "Test Product", id: "p1" };

  function toggle() {
    if (renderedComponent.cmp === Product) {
      renderedComponent = { cmp: CartItem, title: "Another Product", id: "p2" };
    } else {
      renderedComponent = { cmp: Product, title: "Test Product", id: "p1" };
    }
  }
</script>

<button on:click={toggle}>Toggle Display</button>

<svelte:component 
    this={renderedComponent.cmp} 
    title={renderedComponent.title} 
    id={renderedComponent.id} />
