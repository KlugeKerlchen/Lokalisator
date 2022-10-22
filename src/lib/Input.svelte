<script>

import Output from "./Output.svelte";   

let value = '';

let check = false;
function handleSubmit(e){
    check = true;
    setTimeout(() => {
        check = false
    })
}
</script>

<div>
    <form on:submit|preventDefault={handleSubmit}>
        <input class="bg-neutral-300 p-0.5 rounded-sm placeholder:text-black" placeholder="city" bind:value>
    </form>
</div>
<Output city={value} eventInput={check}/>