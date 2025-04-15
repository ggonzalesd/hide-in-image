<script lang="ts">
let name = $state('Hello World');
</script>

<div>
  <span>{name}</span>
  <button onclick={() => name = 'Hello SvelteKit'}>Change</button>
</div>
