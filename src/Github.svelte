<script>
import {onMount} from 'svelte';
let users = [];
let loading = true;
onMount(async ()=>{
  let userData = await fetch('https://api.github.com/users');
  let githubUsers = await userData.json();
  console.log(githubUsers);
  users = githubUsers;
  loading = false;
})
</script>

<style>
  h2 {
    text-align: center;
  }
</style>

{#if loading}
  <h2>Loading I think</h2>
{:else}
  <section>
    {#each users as user}
      <article class='user'>
        <img src={user.avatar_url} alt={user.login}>
      </article>
      <div class="user-info">
      <h3>User: {user.login}</h3>
      <a href={user.html_url} class="btn-primary" target="_blank">github url</a>
      </div>
    {/each}
  </section>
{/if}
