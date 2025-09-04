<template>
  <div class="terminal">
    <div v-for="(line, index) in lines" :key="index" class="line">
      <span class="prompt">user@portfolio:~$</span>
      <span class="text">{{ line }}</span>
    </div>

    <!-- Active input line -->
    <div class="line">
      <span class="prompt">user@portfolio:~$</span>
      <input
        class="input"
        type="text"
        v-model="currentInput"
        @keyup.enter="handleEnter"
        autofocus
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lines: [],         // stores submitted commands
      currentInput: "",  // what user is typing
    };
  },
  methods: {
    handleEnter() {
      if (this.currentInput.trim() !== "") {
        this.lines.push(this.currentInput); // save typed command
        this.currentInput = "";             // reset input
      }
    },
  },
};
</script>

<style scoped>
.terminal {
  width: 100%;
  height: 100vh;
  background: #000;
  color: #33ff33;
  font-family: "Fira Code", "Courier New", Courier, monospace;
  padding: 1rem;
  box-sizing: border-box;
  overflow-y: auto; /* scroll if too many lines */
}

.line {
  display: flex;
  align-items: center;
}

.prompt {
  margin-right: 0.5rem;
}

.text {
  white-space: pre-wrap;
}

.input {
  background: transparent;
  border: none;
  outline: none;
  color: #33ff33;
  font-family: inherit;
  font-size: inherit;
  flex: 1;
}
</style>
