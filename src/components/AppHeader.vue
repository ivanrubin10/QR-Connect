<template>
    <header>
    <nav>
      <div class="title">
        <slot name="title"></slot>
      </div>
    </nav>
  </header>
</template>

<style scoped>
header {
  background-image: linear-gradient(to right, #0f0c29, #302b63, #24243e);;
  color: white;
  height: 4em;
  display: flex;
  align-items: center;
  padding: 0em 2em;
}

</style>
