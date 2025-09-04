<template>
  <div class="terminal">
    <!-- Past commands and their outputs -->
    <div v-for="(entry, index) in history" :key="index">
      <div class="line">
        <span class="prompt">user@portfolio:~$</span>
        <span class="text">{{ entry.command }}</span>
      </div>
      <div v-if="entry.output" class="output" v-for="(line, idx) in entry.output" :key="idx">
        {{ line }}
      </div>
    </div>

    <!-- Active input line -->
    <div class="line">
      <span class="prompt">user@portfolio:~$</span>
      <input class="input" type="text" v-model="currentInput" @keyup.enter="handleEnter" autofocus />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      history: [], // stores command + outputs
      currentInput: "", // active line
    };
  },
  methods: {
    handleEnter() {
      const command = this.currentInput.trim();
      let output = [];

      if (command) {
        // Basic command handling
        switch (command) {
          case "ls":
            output = ["skills.txt    about.txt    projects.txt"];
            break;
          case "whoami":
            output = ["Asad Ali Khan"]
            break;
          case "help":
            output = [
              "Available commands:",
              "ls - list files",
              "cat <file> - view file contents",
              "clear - clear the screen",
              "help - show this message",
              "whoami - shows my name"
            ];
            break;
          case "clear":
            this.history = [];
            this.currentInput = "";
            return; // don’t add "clear" itself to history
          default:
            output = [`bash: ${command}: command not found`];
        }

        // Push command and output to history
        this.history.push({ command, output });
      }

      this.currentInput = "";
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
  overflow-y: auto;
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

.output {
  white-space: pre-wrap;
  text-align: left;
  width: 100%;
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

/* Chrome, Edge, Safari */
.terminal::-webkit-scrollbar {
  width: 8px;
  /* scrollbar width */
  height: 8px;
  /* for horizontal scroll if needed */
}

.terminal::-webkit-scrollbar-track {
  background: black;
  /* track color */
}

.terminal::-webkit-scrollbar-thumb {
  background-color: #33ff33;
  /* the draggable part */
  border-radius: 4px;
  border: 1px solid black;
}

.terminal::-webkit-scrollbar-thumb:hover {
  background-color: #66ff66;
}

/* Firefox */
.terminal {
  scrollbar-width: thin;
  /* "auto" | "thin" | "none" */
  scrollbar-color: #33ff33 black;
  /* thumb color | track color */
}
</style>
