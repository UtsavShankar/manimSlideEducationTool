<script lang="ts">
  import { getCurrentWindow } from '@tauri-apps/api/window';
  const appWindow = getCurrentWindow();
</script>

<main>
  <div data-tauri-drag-region class="titlebar">
    <div class="controls">
      <button onclick={() => appWindow.minimize()}>−</button>
      <button onclick={() => appWindow.toggleMaximize()}>□</button>
      <button onclick={() => appWindow.close()}>✕</button>
    </div>
  </div>
</main>

<style>
  :global(*, *::before, *::after) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(html, body) {
    width: 100%;
    height: 100%;
    overflow: hidden;
    background: #1F1F1F;
  }

  main {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }

  .titlebar {
    height: 32px;
    background: #1F1F1F;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 0 8px;
    user-select: none;
  }

  .controls button {
    all: unset;
    color: #cdd6f4;
    cursor: pointer;
    padding: 4px 10px;
    font-size: 14px;
    border-radius: 4px;
  }

  .controls button:hover {
    background: rgba(255,255,255,0.1);
  }
</style>
