<script context="module" lang="ts">
  export const prerender = true;
</script>

<script lang="ts">
  import Word from "$lib/word.svelte";
  let library_words: string[] = [
    "친구",
    "가족",
    "나",
    "사람",
    "너",
    "우리",
    "저희",
    "언제",
    "오리온 초코파이"
  ];

  let target_words: string[] = [];

  function onDragover(event: DragEvent) {
    event.preventDefault();
    event.dataTransfer.dropEffect = "move";
  }

  function onDrop(event: DragEvent) {
    event.preventDefault();
    let data = event.dataTransfer.getData("text");
    moveword(data);
    render();
  }

  function moveword(word: string) {
    target_words.push(word);
    library_words = library_words.filter((w) => w != word);
  }
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>

<div id="notepad">
  <div id="word-list">
    {#each library_words as word}
      <Word {word} />
    {/each}
  </div>
</div>

<div on:dragover={onDragover} on:drop={onDrop} id="target-placeholder">
  <div id="target-word-list">
    {#each target_words as word}
      <Word {word} />
    {/each}
  </div>
</div>

<style>
  #notepad {
    background-color: #f7f3ac;
    width: 80vw;
    height: 60vh;

    border: 2px solid #ccc;
    border-radius: 30px;

    padding: 25px;

    display: flex;
    flex-wrap: wrap;

    align-items: flex-start;
    justify-content: flex-start;
  }

  #word-list {
    display: flex;
    flex-wrap: wrap;
  }

  #target-placeholder {
    position: absolute;
    bottom: 0;

    width: 60vw;
    height: 30vh;

    border: 2px solid #ccc;
    border-radius: 30px 30px 0 0;

    margin-top: 5vh;
  }
</style>
