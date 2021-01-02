<script context="module">
  export function preload({ params, query }) {
	  console.log('Preloading...');
    return this.fetch(`blog.json`)
      .then(r => r.json())
      .then(posts => {
        return { posts: posts };
      });
  }
</script>

<script>
  import { onMount } from "svelte";
  export let posts;

  console.log('Executing!');

//   fetch();

  onMount(() => {
	  console.log('Mounted!');
	//   fetch();
  });
</script>

<style>
  ul {
    margin: 0 0 1em 0;
    line-height: 1.5;
  }
</style>

<svelte:head>
  <title>Blog</title>
</svelte:head>

<h1>Recent posts</h1>

<ul>
  {#each posts as post}
    <!-- we're using the non-standard `rel=prefetch` attribute to
				tell Sapper to load the data for the page as soon as
				the user hovers over the link or taps it, instead of
				waiting for the 'click' event -->
    <li>
      <a rel="prefetch" href="blog/{post.slug}">{post.title}</a>
    </li>
  {/each}
</ul>
