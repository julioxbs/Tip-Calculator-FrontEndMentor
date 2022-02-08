<template>
  <div id="app">
    <div class="container">
      <Calculator />
    </div>
  </div>
</template>

<script>
  import Calculator from "./components/Calculator.vue";

  export default {
    name: "App",
    components: {
      Calculator,
    }
}
</script>

<style>
  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :root {
    --clr-strong-cyan: hsl(172, 67%, 45%);
    --clr-very-dark-cyan: hsl(183, 100%, 15%);
    --clr-dark-grayish-cyan: hsl(186, 14%, 43%);
    --clr-light-grayish-cyan: hsl(184, 14%, 56%);
    --clr-lighter-grayish-cyan: hsl(185, 41%, 84%);
    --clr-white-grayish-cyan: hsl(189, 41%, 97%);
    --clr-white: hsl(0, 0%, 100%);
    --clr-font: 'Space Mono', monospace;
  }

  body {
    height: 100vh;
    width: 100vw;
    background-color: var(--clr-lighter-grayish-cyan);

    display: flex;
    align-items: center;
    justify-content: center;

    font-family: var(--clr-font);
  }
</style>
