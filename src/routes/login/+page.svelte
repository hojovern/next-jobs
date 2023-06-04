<script>
    import { goto } from '$app/navigation';
    import { authenticateUser } from './../../utils/auth.js';
    let formErrors = {};
  
    async function logIn(evt) {
      evt.preventDefault();
    
      const userData = {
        username: evt.target['username'].value,
        password: evt.target['password'].value,
      };
  
    const res = await authenticateUser(userData.username, userData.password);
      if (res.success) {
        goto('/')
      }
    }
    
  </script>
  
  <h1 class="text-center text-xl">Log In</h1>
  <div class="text-center">
  </div>

  <div class="flex justify-center items-center mt-8">
      <form on:submit={logIn} class="w-1/3">
          <div class="form-control w-full">
              <label class="label" for="username">
                  <span class="label-text">Username</span>
              </label>
              <input type="text" name="username" placeholder="johndoe" class="input input-bordered w-full" />
              {#if 'username' in formErrors}
              <label class="label" for="username">
                  <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
              </label>
              {/if}
          </div>
  
          <div class="form-control w-full">
              <label class="label" for="password">
                  <span class="label-text">Password</span>
              </label>
              <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
              {#if 'password' in formErrors}
              <label class="label" for="password">
                  <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
              </label>
              {/if}
          </div>
  
          <div class="form-control w-full mt-4">
              <button class="btn btn-md">Log In</button>
          </div>
      </form>
  </div>
    