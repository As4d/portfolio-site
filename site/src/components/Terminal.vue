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
  flex: 1;                /* take all remaining space below Boot */
  padding: 1rem;
  display: flex;
  flex-direction: column;
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
  color: #33ff33;
  flex: 1;
}
</style>
