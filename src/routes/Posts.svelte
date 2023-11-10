<script>
  import { onMount } from 'svelte';

  let posts = [];
  let postName = '';
  const url = 'https://jsonplaceholder.typicode.com/posts/1/comments';

  onMount(async () => {
    const response = await fetch(url);
    const jsonResponse = await response.json();
    const postNames = jsonResponse.map((post) => post.name);

    posts = postNames;
  });

  const sendPost = () => {
    posts = [...posts, postName];
    postName = '';
  };

  const deletePost = (index) => {
    posts = posts.filter((post, idx) => idx != index);
  };
</script>

<div class="posts">
  {#each posts as post, i (i)}
    <div class={i}>
      <p>{post}&nbsp;<button on:click={() => deletePost(i)}>Supprimer</button></p>
    </div>
  {:else}
    <p>Pas de posts à montrer</p>
  {/each}
</div>
<div class="create-post">
  <input bind:value={postName} placeholder="Votre post" /><button on:click={sendPost}
    >Envoyer</button
  >
</div>

<style>
</style>
