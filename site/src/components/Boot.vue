<template>
  <div class="boot-banner">
    <pre>
██████╗  ██████╗ ██████╗ ████████╗███████╗ ██████╗ ██╗     ██╗ ██████╗ 
██╔══██╗██╔═══██╗██╔══██╗╚══██╔══╝██╔════╝██╔═══██╗██║     ██║██╔═══██╗
██████╔╝██║   ██║██████╔╝   ██║   █████╗  ██║   ██║██║     ██║██║   ██║
██╔═══╝ ██║   ██║██╔══██╗   ██║   ██╔══╝  ██║   ██║██║     ██║██║   ██║
██║     ╚██████╔╝██║  ██║   ██║   ██║     ╚██████╔╝███████╗██║╚██████╔╝
╚═╝      ╚═════╝ ╚═╝  ╚═╝   ╚═╝   ╚═╝      ╚═════╝ ╚══════╝╚═╝ ╚═════╝
👋 Welcome to my linux terminal style portfolio :) - Asad Ali Khan. 👋
🏗️ History search, more files, tabbing files and mobile compatibility in the works! 🏗️

⁉️ Non-technical? No problem! Try typing "help" to get you started.
Still stuck? Try out  "whoami", "cat about.txt" and "cat projects.txt". ⁉️
</pre>
  </div>
</template>

<style scoped>
/* Boot banner styles */
.boot-banner {
  flex-shrink: 0;
  /* never shrink */
  white-space: pre;
  /* preserve ASCII art formatting */
  font-size: 12px;
  line-height: 1.2;
  padding: 1rem;
  overflow-x: auto;
  /* prevent ASCII art from overflowing on mobile */
}
</style>
