<script>
  import Product from "./Product.svelte";

  function addToCart(event) {
    console.log(event);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }
</script>

<Product
  productTitle="A Book"
  on:add-to-cart={addToCart}
  on:delete={deleteProduct} />
