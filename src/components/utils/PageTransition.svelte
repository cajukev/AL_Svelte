<script>
  import { fly } from 'svelte/transition';
  export let refresh = '';
</script>

{#key refresh}
  <div
    in:fly="{{ y: -50, duration: 500, delay: 25 }}"
    >
    <slot/>
  </div>
{/key}