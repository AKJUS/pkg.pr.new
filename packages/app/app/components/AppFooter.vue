<template>
  <footer
    class="text-center p-12 opacity-50 hover:opacity-100 focus-within:opacity-100 flex flex-col items-center gap-3 text-xs"
  >
    <a href="https://stackblitz.com/" target="_blank">
      <img
        src="/stackblitz.svg"
        alt="StackBlitz"
        width="117"
        height="24"
        class="not-dark:hidden"
      />
      <img
        src="/stackblitz-black.svg"
        alt="StackBlitz"
        width="117"
        height="24"
        class="dark:hidden"
      />
    </a>
    <div class="flex gap-3 items-center">
      <div>
        Built in
        <a
          href="https://github.com/stackblitz-labs"
          target="_blank"
          class="text-primary"
          >StackBlitz Labs</a
        >
      </div>
      <UIcon name="ph-dot" />
      <div>
        UI by
        <a href="https://github.com/Akryum" target="_blank" class="text-primary"
          >Akryum</a
        >
      </div>
    </div>
  </footer>
</template>
