<script lang="ts">
import type { ChangeEventHandler } from 'svelte/elements';

let iFileTag: HTMLInputElement | null = null;
const iFile = $state<{ file: File | null }>({ file: null });

const onchange: ChangeEventHandler<HTMLInputElement> = (e) => {
  const target = e.target as HTMLInputElement;

  if (target.files == null) return;
  if (target.files.length === 0) return;

  iFile.file = target.files[0];
};

const onkeydown = (e: KeyboardEvent) => {
  if (e.key !== 'Enter' && e.key !== ' ') return;
  if (iFileTag == null) return;

  iFileTag.click();
};
</script>

<!-- svelte-ignore a11y_no_noninteractive_tabindex -->
<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
<label
  tabindex="0"
  onkeydown={onkeydown}
  class="flex cursor-pointer items-center gap-2 rounded-md p-2 hover:bg-gray-100 dark:hover:bg-gray-800"
>
  <div class="border border-dashed p-4">
    {#if iFile.file}
      <span class="text-sm text-gray-500 dark:text-gray-400">
        {iFile.file.name}
      </span>
    {:else}
      <span class="text-sm text-gray-500 dark:text-gray-400">
        No file selected
      </span>
    {/if}
  </div>
  <input
    bind:this={iFileTag}
    class="hidden"
    type="file"
    accept="image/*"
    onchange={onchange}
  />
</label>
