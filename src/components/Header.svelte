<script>

import { isLoggedInStore } from '../utils/auth.js';
import { logOut } from '../utils/auth.js';
import { goto } from '$app/navigation';
// import Themes from './Themes.svelte';

function postLogOut() {
  logOut();
  goto('/');
}
</script>

<header class = "flex flex-col sm:flex-row justify-between m-5">

  <a href = "/" class = "btn btn-outline">Next Jobs</a>

  <div class = "flex justify-evenly">
    <ul class = "menu menu-horizontal px-1">
      <!-- <li><Themes/></li> -->
    </ul>
    <ul class = "menu horizontal px-1">
      <li><a href = "/jobs/new" class = "btn btn-outline">Post Job</a></li>
    </ul>
   
    {#if !$isLoggedInStore} 
    <ul class="menu horizontal px-1">
      <li><a href="/users/new" class="btn btn-outline">Sign Up</a></li>
    </ul>
    {/if}
  
    {#if $isLoggedInStore}
      <ul class = "menu menu-horizontal px-1">
        <li><button class = "btn btn-outline" on:click = {postLogOut}>Log Out</button></li>
      </ul>
    {:else}
      <ul class = "menu horizontal px-1">
        <li><a href = "/login" class = "btn btn-outline">Log In</a></li>
      </ul>
    {/if}
  </div>
</header>



