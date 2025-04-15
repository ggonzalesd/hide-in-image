<script lang="ts">
function onclick() {
  const theme = localStorage.getItem('theme');
  if (theme === 'dark') {
    localStorage.setItem('theme', 'light');
    document.documentElement.classList.toggle('dark', false);
  } else {
    localStorage.setItem('theme', 'dark');
    document.documentElement.classList.toggle('dark', true);
  }
}
</script>

<button onclick={onclick}> Click </button>

<style>
button {
  cursor: pointer;
  border: none;
  border-radius: 5px;
  background-color: #333;
  padding: 10px 20px;
  height: 100%;
  color: white;
  font-size: 16px;
}

button:hover {
  background-color: #555;
}
</style>
