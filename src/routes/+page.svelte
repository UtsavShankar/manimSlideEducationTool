<script lang="ts">
  import { getCurrentWindow } from '@tauri-apps/api/window';
  const appWindow = getCurrentWindow();
  import { onMount } from 'svelte'
  import loader from '@monaco-editor/loader'

  let editorContainer: HTMLDivElement
  let editor: any

  onMount(async () => {
    const monaco = await loader.init()
    
    editor = monaco.editor.create(editorContainer, {
      value: `from manim import *\n\nclass Slide01(Scene):\n    def construct(self):\n        pass`,
      language: 'python',
      theme: 'vs-dark',
      fontSize: 14,
      minimap: { enabled: false },
      automaticLayout: true,
    })
  })

  export function getCode() {
    return editor?.getValue()
  } 
</script>

<main>
  <div data-tauri-drag-region class="titlebar">
    <div class="controls">
      <button onclick={() => appWindow.minimize()}>−</button>
      <button onclick={() => appWindow.toggleMaximize()}>□</button>
      <button onclick={() => appWindow.close()}>✕</button>
    </div>
  </div>
  <div class="content">
    <div bind:this={editorContainer} class="editor"></div>
  </div>
</main>



<style>
.content {
  flex: 1;
  display: flex;
  min-height: 0;
}

.editor {
  width: 50%;
  height: 100%;
}
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
