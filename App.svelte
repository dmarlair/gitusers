<script>
  import { onMount } from "svelte";
  import User from "./User.svelte";
  import UserSearch from "./UserSearch.svelte";
  // run this when the app starts
  onMount(() => {
    getGitHubUsers();
  });

  // create a variable to store our users
  let users;

  /*
     _ Grab users from GitHub
     */
  function getGitHubUsers() {
    fetch("https://api.github.com/users")
      .then(resp => resp.json())
      .then(data => {
        users = data;
      });
  }
</script>

<style>
  .user-list {
    display: flex;
    flex-flow: wrap;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .user-list li {
    width: 20%;
    padding: 10px;
  }
</style>


<main>
  <UserSearch></UserSearch>
  {#if users}
    <ul class="user-list">
      {#each users as user}
        <li>
           <User username={user.login} avatar={user.avatar_url} />
        </li>
      {/each}
    </ul>
  {/if}
</main>