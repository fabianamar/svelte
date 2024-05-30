<script>
    import { Inertia } from '@inertiajs/inertia';
    import { writable } from 'svelte/store';
    
    let name = '';
    let email = '';
    let password = '';
    let password_confirmation = '';
    let errors = writable({});
    
    function submit() {
      errors.set({});  // Limpiar errores antes de enviar el formulario
      Inertia.post('/register', { name, email, password, password_confirmation }, {
        onError: (err) => {
          errors.set(err);
        }
      });
    }
    </script>
    
    <form on:submit|preventDefault={submit}>
      <div>
        <label for="name">Name</label>
        <input id="name" bind:value={name} required />
        {#if $errors.name}
          <div>{$errors.name}</div>
        {/if}
      </div>
    
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
        <label for="password_confirmation">Confirm Password</label>
        <input id="password_confirmation" type="password" bind:value={password_confirmation} required />
        {#if $errors.password_confirmation}
          <div>{$errors.password_confirmation}</div>
        {/if}
      </div>
    
      <button type="submit">Register</button>
    </form>
    