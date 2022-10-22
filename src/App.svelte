<script lang="ts">
  import { onMount } from "svelte";
  import Input from "./lib/Input.svelte";
  import Output from "./lib/Output.svelte";

let yes = false;
onMount(() => {
  setTimeout(() => {
    yes = true;
  })
})

/* random color */
function getRndInteger(min, max) { //  returns a random number between min and max (both included)
    return Math.floor(Math.random() * (max - min + 1) ) + min;
}

function getRndColor_hsl(){
    let random_h = getRndInteger(0,355);
    let random_color = 'hsl(' + random_h + ',100%, 50%)'
    return random_color;
}

const color = getRndColor_hsl();
</script>

<main class="flex flex-col justify-center items-center h-screen w-screen /bg-gradient-to-tr /from-purple-500 /to-pink-500 transition-colors" style="background:{color};">
  <div class="md:w-1/2 md:h-1/3 w-5/6 h-1/2 bg-white rounded flex flex-col items-center p-4 relative shadow-lg">
    <h1 class="font-semibold text-4xl mb-8 relative z-0">Kluge Kerlchen Lokalisator
      <div class="absolute -bottom-2 left-0 w-full h-2 rounded -z-10 transition-transform duration-500 ease-out origin-left {yes? 'scale-x-100':'scale-x-0'}"
      style="background:{color};"></div>
    </h1>
    <div class="flex justify-center items-center flex-col gap-8">
      <Input color={color}/>
    </div>
  </div>
</main>

