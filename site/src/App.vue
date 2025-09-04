<script>
export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {},

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event handlers in templates.
  methods: {},

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {},
};
</script>

<template>
  <div class="terminal-prompt">
    <label class="terminal-prompt__label">user@portfolio:~$</label>
    <input
      class="terminal-prompt__input"
      type="text"
      autofocus
      spellcheck="false"
      autocomplete="off"
    />
  </div>
</template>

<style scoped>
.terminal-prompt {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  padding: 0.5rem;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
  z-index: 1000;
}

.terminal-prompt__label {
  margin-right: 0.5rem;
}

.terminal-prompt__input {
  flex: 1;
  background: transparent;
  border: none;
  color: #00ff00;
  columns: inherit;
  font-family: inherit;
  font-size: inherit;
  outline: none;
}
</style>
