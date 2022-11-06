<script>
  import { onMount } from "svelte";

  // Data fetching
  let advice;
  let adviceid;

  async function fetchdata() {
    await fetch("https://api.adviceslip.com/advice")
      .then((response) => response.json())
      .then((data) => {
        advice = data.slip.advice;
        adviceid = data.slip.id;
        console.log(data);
      });
  }

  let promise = fetchdata();
  function handleClick() {
    promise = fetchdata();
  }

  onMount(fetchdata);
</script>

<svelte:head>
  <style>
    @import url("https://fonts.googleapis.com/css2?family=Manrope:wght@800&display=swap");
  </style>
</svelte:head>

<main>
  <container>
    <div class="flexbox-col">
      {#await promise}
        <!-- Terminal spinner by Zeno Rocha -->
        <!-- https://codepen.io/zenorocha/pen/LLBVmo -->
        <div class="spinner" />
      {:then}
        <h2 class="adviceid">Advice #{adviceid}</h2>
        <h1 class="advice">"{advice}"</h1>
      {/await}
      <div class="divider">
        <img
          src="pattern-divider-desktop.svg"
          class="divider-desktop"
          alt="Desktop divider"
        />
        <img
          src="pattern-divider-mobile.svg"
          class="divider-mobile"
          alt="Mobile divider"
        />
      </div>
      <button class="dice" on:click={handleClick}>
        <img src="icon-dice.svg" alt="Dice" />
      </button>
    </div>
  </container>

  <div class="attribution">
    Challenge by <a
      href="https://www.frontendmentor.io?ref=challenge"
      target="_blank"
      rel="noreferrer">Frontend Mentor</a
    >. Coded by
    <a href="https://github.com/GermanHeim" target="_blank" rel="noreferrer"
      >Germán Heim</a
    >.
  </div>
</main>

<style>
  .attribution {
    font-size: 12px;
    text-align: center;
    position: absolute;
    bottom: 0;
    width: 100%;
    margin-bottom: 20px;
    color: hsl(193, 38%, 86%);
  }
  .attribution a {
    color: hsl(228, 59%, 60%);
    text-decoration: none;
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: hsl(218, 23%, 16%);
  }

  container {
    background-color: hsl(217, 19%, 24%);
    width: 650px;
    border-radius: 10px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
  }

  .adviceid {
    text-transform: uppercase;
    color: hsl(150, 100%, 66%);
    text-size-adjust: 100%;
    letter-spacing: 4px;
    font-size: 12px;
    padding-top: 25px;
  }

  .flexbox-col {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    text-align: center;
  }

  .divider {
    position: relative;
    bottom: -40px;
  }

  .advice {
    font-size: 28px;
    color: hsl(194, 49%, 92%);
  }

  .dice {
    background-color: hsl(150, 100%, 66%);
    border: none;
    border-radius: 50%;
    height: 65px;
    width: 65px;
    margin-top: 2rem;
    cursor: pointer;
    position: relative;
    bottom: -3.5rem;
  }

  .dice img {
    width: 30px;
    vertical-align: middle;
  }

  .dice:hover {
    -webkit-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    -ms-transform: rotate(360deg);
    transform: rotate(360deg);

    -webkit-transition: all 800ms ease;
    -moz-transition: all 800ms ease;
    -ms-transition: all 800ms ease;
    -o-transition: all 800ms ease;
    transition: all 800ms ease;
    box-shadow: 0px 0px 65px 10px hsla(150, 100%, 66%, 0.367);
  }

  h1 {
    padding: 25px 10px 0px 10px;
  }

  @media (max-width: 701px) {
    container {
      width: 90%;
    }
    .divider-desktop {
      display: none;
    }
  }

  @media (min-width: 700px) {
    .divider-mobile {
      display: none;
    }
  }

  .spinner {
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .spinner:after {
    animation: changeContent 0.8s linear infinite;
    display: block;
    content: "⠋";
    font-size: 80px;
  }

  @keyframes changeContent {
    10% {
      content: "⠙";
    }
    20% {
      content: "⠹";
    }
    30% {
      content: "⠸";
    }
    40% {
      content: "⠼";
    }
    50% {
      content: "⠴";
    }
    60% {
      content: "⠦";
    }
    70% {
      content: "⠧";
    }
    80% {
      content: "⠇";
    }
    90% {
      content: "⠏";
    }
  }
</style>
