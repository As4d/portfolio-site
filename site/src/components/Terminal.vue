<template>
  <div class="terminal" ref="terminal">
    <!-- History -->
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
      <input class="input" type="text" v-model="currentInput" @keyup.enter="handleEnter" ref="input" autofocus />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      history: [],        // [{ command: string, output: string[] }]
      currentInput: "",   // active input line
      defaultFiles: ["about.txt", "certs.txt"], // fallback for ls
    };
  },
  mounted() {
    // focus input on mount
    this.$nextTick(() => this.$refs.input && this.$refs.input.focus());
  },
  methods: {
    async handleEnter() {
      const raw = this.currentInput;
      const commandLine = raw.trim();
      if (!commandLine) return;

      const [cmd, ...args] = commandLine.split(/\s+/);

      // clear behaves specially (no history entry)
      if (cmd === "clear") {
        this.history = [];
        this.currentInput = "";
        this.$nextTick(this.scrollToBottom);
        return;
      }

      // route commands
      let output = [];
      switch (cmd) {
        case "help":
          output = [
            "Available commands:",
            "  ls              - list files",
            "  cat <file>      - view file contents",
            "  whoami          - shows my name",
            "  pwd             - current directory",
            "  clear           - clear the screen",
            "  help            - this message"
          ];
          break;

        case "whoami":
          output = ["Asad Ali Khan"];
          break;

        case "pwd":
          output = ["/home/user"];
          break;

        case "ls":
          output = await this.cmdLs();
          break;

        case "cat":
          output = await this.cmdCat(args[0]);
          break;

        default:
          output = [`bash: ${cmd}: command not found`];
      }

      // add entry to history & reset input
      this.history.push({ command: commandLine, output });
      this.currentInput = "";

      // keep input focused & scroll to bottom
      this.$nextTick(() => {
        this.$refs.input && this.$refs.input.focus();
        this.scrollToBottom();
      });
    },

    async cmdLs() {
      // Try to fetch a manifest of files; fallback to defaults if not present
      try {
        const res = await fetch("/files/index.json", { cache: "no-cache" });
        if (res.ok) {
          const files = await res.json(); // expects ["about.txt","certs.txt",...]
          return [files.join("    ")];
        }
      } catch (_) { }
      return [this.defaultFiles.join("    ")];
    },

    async cmdCat(filename) {
      if (!filename) {
        return ["cat: missing file operand", "Try 'cat <filename>'"];
      }

      try {
        const res = await fetch(`/files/${encodeURIComponent(filename)}`, {
          cache: "no-cache",
        });

        // If fetch fails or returns index.html instead of file
        if (!res.ok) {
          return [`cat: ${filename}: No such file or directory`];
        }

        const text = await res.text();

        // Detect if we accidentally got back index.html
        if (text.includes("<!DOCTYPE html>") || text.includes("<html")) {
          return [`cat: ${filename}: No such file or directory`];
        }

        return text.replace(/\r\n/g, "\n").split("\n");
      } catch (err) {
        return [`cat: ${filename}: Failed to read file`];
      }
    },

    scrollToBottom() {
      const el = this.$refs.terminal;
      if (el) el.scrollTop = el.scrollHeight;
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
  font-size: 16px;
  /* set baseline so input + prompt match */
  line-height: 1.5;
  padding: 1rem;
  box-sizing: border-box;
  overflow-y: auto;
}

.line {
  display: flex;
  align-items: baseline;
  /* keep text baselines aligned */
}

.prompt {
  margin-right: 0.5rem;
  white-space: pre;
  /* keep the exact spacing of the prompt */
}

.text {
  white-space: pre-wrap;
}

.output {
  white-space: pre-wrap;
  /* preserve newlines */
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

/* Custom scrollbars */
/* Chrome, Edge, Safari */
.terminal::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

.terminal::-webkit-scrollbar-track {
  background: #000;
}

.terminal::-webkit-scrollbar-thumb {
  background-color: #33ff33;
  border-radius: 4px;
  border: 1px solid #000;
}

.terminal::-webkit-scrollbar-thumb:hover {
  background-color: #66ff66;
}

/* Firefox */
.terminal {
  scrollbar-width: thin;
  scrollbar-color: #33ff33 #000;
}
</style>
