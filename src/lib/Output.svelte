<script>
  import { fade } from "svelte/transition";




export let eventInput;

$: eventInput? getKoordinaten() : '';

export let city = 'london';

const url = 'https://nominatim.openstreetmap.org/search?format=json&'
let data = [{lat: null, lon: null}];
async function getKoordinaten(){
    let myUrl = url + `city="${city}"`
    const response = await fetch(myUrl);
    data = await response.json();
    console.log(data)
}

function getFormatted(lat, lon){
  let latAfterThing = '';
  let lonAfterThing = '';
  if(lat >= 0){
    latAfterThing = 'ÖL'
  } else if(lat < 0){
    latAfterThing = 'WL'
    lat *= -1;
  }
  if(lon >= 0){
    lonAfterThing = 'NB'
  } else if(lon < 0){
    lonAfterThing = 'SB'
    lon *= -1;
  }
  return `ca. ${Math.round(lon)}°${lonAfterThing}, ca. ${Math.round(lat)}°${latAfterThing}`
}

$: data.length === 0? '' : '';
</script>

<div class="">
  <!--{#if data[0] !== null}
    {data[0].lat} {data[0].lon}
  {/if}-->
  {#if data.length !== 0}
    {#key data[0].lon}
      <p in:fade class="text-3xl font-semibold">{getFormatted(data[0].lon, data[0].lat)}</p>
    {/key}
  {:else}
    <p class="text-red-500 text-4xl">Could not find city</p>
  {/if}
  <a href={data.length !== 0?`https://www.google.com/maps/@${data[0].lat},${data[0].lon},12z`: ''} target="_blank" rel="noreferrer" class="absolute left-0 bottom-0 m-6 group">
    <svg width=75 height=75 xmlns="http://www.w3.org/2000/svg" viewBox="0 0 92.3 132.3"><path fill="#1a73e8" d="M60.2 2.2C55.8.8 51 0 46.1 0 32 0 19.3 6.4 10.8 16.5l21.8 18.3L60.2 2.2z"/><path fill="#ea4335" d="M10.8 16.5C4.1 24.5 0 34.9 0 46.1c0 8.7 1.7 15.7 4.6 22l28-33.3-21.8-18.3z"/><path fill="#4285f4" d="M46.2 28.5c9.8 0 17.7 7.9 17.7 17.7 0 4.3-1.6 8.3-4.2 11.4 0 0 13.9-16.6 27.5-32.7-5.6-10.8-15.3-19-27-22.7L32.6 34.8c3.3-3.8 8.1-6.3 13.6-6.3"/><path fill="#fbbc04" d="M46.2 63.8c-9.8 0-17.7-7.9-17.7-17.7 0-4.3 1.5-8.3 4.1-11.3l-28 33.3c4.8 10.6 12.8 19.2 21 29.9l34.1-40.5c-3.3 3.9-8.1 6.3-13.5 6.3"/><path fill="#34a853" d="M59.1 109.2c15.4-24.1 33.3-35 33.3-63 0-7.7-1.9-14.9-5.2-21.3L25.6 98c2.6 3.4 5.3 7.3 7.9 11.3 9.4 14.5 6.8 23.1 12.8 23.1s3.4-8.7 12.8-23.2"/></svg>
    <div class="absolute hidden group-hover:flex justify-center items-center w-32 h-6 bg-red-500 rounded p-2 text-sm text-white font-semibold -bottom-4 left-[-22px] text-center z-10">Google Maps</div>
  </a>
</div>