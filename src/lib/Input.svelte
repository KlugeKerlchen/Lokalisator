<script>
import { onMount } from "svelte";
import Output from "./Output.svelte";   

export let color;

let value = 'London';
onMount(() => {
    handleSubmit();
})

let check = false;
let spin = false;
function handleSubmit(){
    check = true;
    setTimeout(() => {
        check = false
    })
    if(spin === false){
        spin = true;
        setTimeout(() => {
            spin = false
        }, 300)
    }
}
</script>

<div>
    <form on:submit|preventDefault={handleSubmit} class="relative mt-4">
        <input id="input" class=" peer bg-white p-0.5 rounded-sm text-2xl border-b-2 focus:border-black transition-colors focus:outline-none placeholder-transparent" placeholder="City" bind:value>
        <label for="input" class=" transition-all absolute left-1 -top-4 text-gray-600 text-base peer-placeholder-shown:text-2xl peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-1 peer-focus:-top-4 peer-focus:text-base hover:cursor-text">
            City</label>
        <button class="{spin? 'animate-[spin_300ms_ease-in-out]':''} focus:outline-offset-2"><i class="fa-solid fa-magnifying-glass"></i></button>
    </form>
</div>
<Output city={value} eventInput={check}/>