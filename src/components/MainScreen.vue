<script>
    export default {
        methods : {
            onSelectModeGame(numberOfBlocks) {
                this.$emit('onStartGame', {numberOfBlocks : numberOfBlocks,startTime : new Date().getTime()});
                console.log('start time : ' , new Date().getTime(), typeof new Date().getTime());
            }
        }
    }
</script>

<template>
  <div class="container">
      <h1>POKE MEMORIES</h1>
      <h3>Select mode to start game</h3>
      <div class="selection">
          <button class="mode-game" @click="onSelectModeGame(16)">
              <span>4x4</span>
              <span>Easy</span>
          </button>
          <button class="mode-game" @click="onSelectModeGame(36)">
              <span>6x6</span>
              <span>Normal</span>
          </button>
          <button class="mode-game" @click="onSelectModeGame(64)">
              <span>8x8</span>
              <span>Hard</span>
          </button>
          <button class="mode-game" @click="onSelectModeGame(100)">
              <span>10x10</span>
              <span>Super hard</span>
          </button>
      </div>
  </div>
</template>

<style scoped>
.container {
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: var(--dark);
    color: var(--light);
}
.selection {
    display: flex;
    margin-top: 2rem;
}
.mode-game {
    font: var(--font);
    width: 150px;
    height: 150px;
    background: transparent;
    box-shadow: none;
    border: 1px solid var(--light);
    color: var(--light);
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    margin: 0 1rem;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background .3s ease-in-out;
}
.mode-game:hover {
    background-color: var(--light);
    color: var(--dark);
}
</style>