<script>
    import { Inertia } from '@inertiajs/inertia';
    import { writable } from 'svelte/store';
    
    let email = '';
    let password = '';
    let remember = false;
    let errors = writable({});
    
    function submit() {
      errors.set({});  // Limpiar errores antes de enviar el formulario
      Inertia.post('/login', { email, password, remember }, {
        onError: (err) => {
          errors.set(err);
        }
      });
    }
    </script>
    
    <form on:submit|preventDefault={submit}>
      <div>
        <label for="email">Email</label>
        <input id="email" type="email" bind:value={email} required />
        {#if $errors.email}
          <div>{$errors.email}</div>
        {/if}
      </div>
    
      <div>
        <label for="password">Password</label>
        <input id="password" type="password" bind:value={password} required />
        {#if $errors.password}
          <div>{$errors.password}</div>
        {/if}
      </div>
    
      <div>
        <label for="remember">Remember Me</label>
        <input id="remember" type="checkbox" bind:checked={remember} />
      </div>
    
      <button type="submit">Login</button>
    </form>
    