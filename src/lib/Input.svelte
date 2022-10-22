<script>
import { onMount } from "svelte";
import Output from "./Output.svelte";   

let value = 'london';
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
        }, 1000)
    }
}
</script>

<div>
    <form on:submit|preventDefault={handleSubmit}>
        <input class="bg-white p-0.5 rounded-sm border-b-2 focus:border-pink-500 transition-colors focus:outline-none" placeholder="city or country" bind:value>
        <button class="{spin? 'animate-spin':''}"><i class="fa-solid fa-magnifying-glass"></i></button>
    </form>
</div>
<Output city={value} eventInput={check}/>