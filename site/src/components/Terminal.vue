<template>
  <div class="terminal">
    <div class="line">
      <span class="prompt">user@portfolio:~$</span>
      <input class="input" type="text" />
    </div>
  </div>
</template>

<style scoped>
.terminal {
  flex: 1;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  color: #33ff33;
  font-family: "Fira Code", "Courier New", Courier, monospace;
  font-size: 16px;
}

.line {
  display: flex;
  align-items: center;
}

.prompt {
  margin-right: 0.5rem;
}

.input {
  background: transparent;
  border: none;
  outline: none;
  color: inherit; /* match terminal text */
  font-family: inherit; /* inherit from terminal */
  font-size: inherit; /* inherit from terminal */
  flex: 1;
}
</style>
