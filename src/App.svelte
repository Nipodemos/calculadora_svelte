<script lang="ts">
  let validKeys = [
    "0",
    "1",
    "2",
    "3",
    "4",
    "5",
    "6",
    "7",
    "8",
    "9",
    "-",
    "+",
    "*",
    "÷",
    "/",
    "%",
    "=",
    ",",
    "←",
    "Backspace",
    "Delete",
    "Enter",
    "Escape",
  ];
  let displayContent = "1234";

  function calculate() {
    let formattedValue = displayContent.replace(",", ".").replace("÷", "/");

    const result = eval(formattedValue);
    displayContent = result;
  }

  function handleAction(action: string) {
    const isValidKey = validKeys.includes(action);

    // console.log("isValidKey :>> ", isValidKey);

    if (isValidKey) {
      switch (action) {
        case "Backspace":
        case "Delete":
        case "←":
          return (displayContent = displayContent.slice(0, -1));
        case "Escape":
          return (displayContent = "");
        case "Enter":
        case "=":
          return calculate();
        default:
          return (displayContent += action);
      }
    }
  }

  function handleKeyDown(event: KeyboardEvent) {
    handleAction(event.key);
  }

  function handleClick(event: MouseEvent) {
    const { innerHTML } = event.target as Element;
    handleAction(innerHTML);
  }

  function cleanDisplay() {
    displayContent = "";
  }

  function invertNumberSign() {
    console.log(
      "invertNumberSign:  parseInt(displayContent) :>> ",
      parseInt(displayContent)
    );
    if (isNaN(parseInt(displayContent))) {
      return;
    }
    const number = parseInt(displayContent);
    displayContent = (-number).toString();
  }
</script>

<svelte:body on:keydown={handleKeyDown} />
<main>
  <div class="calculadora">
    <p class="display">{displayContent}</p>

    <div class="buttons">
      <div class="row c-row">
        <button class="green" on:click={cleanDisplay}>AC</button>
        <button class="green" on:click={invertNumberSign}>±</button>
        <button class="green" on:click={handleClick}>%</button>
        <button class="red" on:click={handleClick}>÷</button>
      </div>
      <div class="row">
        <button on:click={handleClick}>7</button>
        <button on:click={handleClick}>8</button>
        <button on:click={handleClick}>9</button>
        <button class="red">x</button>
      </div>
      <div class="row">
        <button on:click={handleClick}>4</button>
        <button on:click={handleClick}>5</button>
        <button on:click={handleClick}>6</button>
        <button class="red">-</button>
      </div>

      <div class="row">
        <button on:click={handleClick}>1</button>
        <button on:click={handleClick}>2</button>
        <button on:click={handleClick}>3</button>
        <button class="red" on:click={handleClick}>+</button>
      </div>

      <div class="row">
        <button on:click={handleClick}>←</button>
        <button on:click={handleClick}>0</button>
        <button on:click={handleClick}>,</button>
        <button class="red" on:click={handleClick}>=</button>
      </div>
    </div>
  </div>
</main>

<style lang="scss">
  main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
  }

  .calculadora {
    background-color: #22252d;
    border-radius: 20px;
    margin: 20px;
    overflow-y: auto;
  }

  .display {
    /* border: 1px solid red; */
    margin-top: 40px;
    margin-right: 16px;
    margin-left: 16px;
    flex: 1;
    display: flex;
    align-items: center;
    flex-direction: row-reverse;
    font-size: 32px;
    font-weight: bold;
    color: white;
    height: 30px;
  }

  .buttons {
    border-radius: 20px;
    background-color: #292d36;

    .row {
      display: flex;
      justify-content: space-evenly;

      button {
        background-color: #272b33;
        border-radius: 10px;
        color: white;
        margin: 8px;
        padding: 8px;
        font-size: 20px;
        font-weight: bold;
        min-width: 40px;
        min-height: 40px;
        border: none;
        outline: none;
        font-family: "Merriweather", serif;
        cursor: pointer;

        &.green {
          color: #26a290;
        }

        &.red {
          color: #a25053;
        }
      }
    }
  }
</style>
