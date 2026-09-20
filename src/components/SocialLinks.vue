<template>
  <div class="social-links">
    <span>Follow our journey</span>
    <div class="social-list">
      <a href="#" aria-label="Instagram">ig</a><a href="#" aria-label="Pinterest">p</a><a href="#" aria-label="LinkedIn">in</a>
    </div>
  </div>
</template>
<style scoped>
.social-links { display: flex; flex-direction: column; gap: 14px; color: var(--muted); font-size: 12px; }
.social-list { display: flex; gap: 9px; }
.social-list a { display: grid; place-items: center; width: 29px; height: 29px; color: var(--ink); border: 1px solid var(--line); border-radius: 50%; font-size: 11px; transition: background .2s, color .2s; }
.social-list a:hover { background: var(--ink); color: white; }
</style>
