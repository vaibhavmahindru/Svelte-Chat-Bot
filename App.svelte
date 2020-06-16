<script>
  import Buttons from "./Buttons.svelte";
  import Container from "./Container.svelte";
  import story from "./story.js";

  let happyScore = 0;
  let storyIndex = 0;

  $: smileySays = story[storyIndex].end
    ? finalMessage()
    : story[storyIndex].smileySays;
  $: buttons = tory[storyIndex].buttons;

  function finalMessage() {
    if (happyScore > 0) return story[storyIndex].end.nice;
    else if (happyScore < 0) return story[storyIndex].end.mean;
    else return story[storyIndex].end.neutral;
  }

  function clickHandler() {
    if (e.detail.value === "reset") {
      happyScore = 0;
      storyIndex = 0;
    } else {
      storyIndex += 1;
      happyScore = e.detail.value;
    }
  }

  let name = "";
</script>

<style type="stylesheet">
  h1 {
    text-align: center;
    background: #ff3e00;
    font-size: 2em;
    padding: 0.3em 0.6em;
    color: white;
    border-radius: 50px;
  }
  input {
    margin: 1em;
    width: 250px;
    font-family: "Nunito", sans-serif;
    border: 0;
    outline: 0;
    background: transparent;
    border-bottom: 1px solid black;
    text-align: center;
    font-size: 2em;
  }
  :global(*) {
    box-sizing: border-box;
  }
  :global(body, html) {
    margin: 0;
    height: 100vh;
    overflow: hidden;
  }
</style>

<Container>
  <input type="text" placeholder="Enter Your Name" bind:value={name} />
  <h1>{name}, {smileySays}</h1>
  <Buttons {buttons} onclick={clickHandler} />
</Container>
