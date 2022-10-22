<script>


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
</script>

<div>
  <!--{#if data[0] !== null}
    {data[0].lat} {data[0].lon}
  {/if}-->
  {#if data.length !== 0}
    {getFormatted(data[0].lon, data[0].lat)}
  {:else}
    <p>Could not find city</p>
  {/if}
</div>