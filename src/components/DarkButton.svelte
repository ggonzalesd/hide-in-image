<script lang="ts">
import darkSvg from '@/assets/dark.svg?raw';
import lightSvg from '@/assets/light.svg?raw';

let theme = $state('light');

$effect(() => {
  const localTheme = localStorage.getItem('theme');

  if (localTheme) {
    theme = localTheme;
    return;
  }

  if (document.documentElement.matches('(prefers-color-scheme: dark)')) {
    theme = 'dark';
  } else {
    theme = 'light';
  }
});

function onclick() {
  if (theme === 'dark') {
    localStorage.setItem('theme', 'light');
    document.documentElement.classList.toggle('dark', false);
  } else {
    localStorage.setItem('theme', 'dark');
    document.documentElement.classList.toggle('dark', true);
  }
  theme = theme === 'dark' ? 'light' : 'dark';
}
</script>

<button
  class="relative flex aspect-square h-full items-center justify-center bg-gray-100 hover:cursor-pointer hover:bg-gray-200 dark:bg-gray-700 dark:hover:bg-gray-600"
  onclick={onclick}
>
  <span class="sr-only"> Toggle dark mode </span>
  <div class="contents" class:onhide={theme === 'light'}>
    {@html darkSvg}
  </div>
  <div class="contents" class:onhide={theme === 'dark'}>
    {@html lightSvg}
  </div>
</button>

<style lang="scss">
button {
  div.contents :global {
    svg {
      display: block;
      position: absolute;
      scale: 1;

      transition: all 0.5s allow-discrete;

      margin: auto;
      padding: 4px;
      width: 36px;
      height: 36px;

      @starting-style {
        rotate: 90deg;
        scale: 0.25;
        opacity: 10%;
      }
    }

    &.onhide {
      svg {
        display: none;
        scale: 0.25;
        opacity: 0%;
      }
    }
  }

  &:active div.contents :global {
    svg {
      scale: 1.25;
      opacity: 100%;
    }
  }
}
</style>
