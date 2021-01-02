<script>
  import { onMount } from "svelte";
  import hobbyStore from "./hobby-store.js";

  let hobbies = [];
  let hobbyInput;
  let isLoading = false;

  isLoading = true;
  let getHobbies = fetch("https://svelte-course.firebaseio.com/hobbies.json")
    .then(res => {
      if (!res.ok) {
        throw new Error("Failed!");
      }
      return res.json();
    })
    .then(data => {
      isLoading = false;
      //   hobbies = Object.values(data);
      hobbyStore.setHobbies(Object.values(data));
      let keys = Object.keys(data);
      console.log(keys);

      for (const key in data) {
        console.log(key, data[key]);
      }
      return hobbies;
    })
    .catch(err => {
      isLoading = false;
      console.log(err);
    });

  function addHobby() {
    // hobbies = [...hobbies, hobbyInput.value];
    hobbyStore.addHobby(hobbyInput.value);

    isLoading = true;
    fetch("https://svelte-course.firebaseio.com/hobbies.json", {
      method: "POST",
      body: JSON.stringify(hobbyInput.value),
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(res => {
        isLoading = false;
        if (!res.ok) {
          throw new Error("Failed!");
        }
        // ...
		alert("Saved Data!");
		// res.json() => Promise with a object that contains the id
      })
      .catch(err => {
        isLoading = false;
        console.log(err);
      });
  }
</script>

<label for="hobby">Hobby</label>
<input type="text" id="hobby" bind:this={hobbyInput} />
<button on:click={addHobby}>Add Hobby</button>

{#if isLoading}
  <p>Loading...</p>
{:else}
  <ul>
    {#each $hobbyStore as hobby}
      <li>{hobby}</li>
    {/each}
  </ul>
{/if}

<!-- {#await getHobbies}
  <p>Loading...</p>
{:then hobbyData}
  <ul>
    {#each hobbyData as hobby}
      <li>{hobby}</li>
    {/each}
  </ul>
{:catch error}
  <p>{error.message}</p>
{/await} -->
