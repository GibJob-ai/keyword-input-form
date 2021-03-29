<script>
import createForm from '@spaceavocado/svelte-form';
import TextInput from './input/text.svelte';

let presets = [];
let dummyInvisibleFileInput; // for hacky json file download

const attachFile = () => {
  dummyInvisibleFileInput.click();
}
const import_append_mappings_json = async () => {
  const mappings_text = await dummyInvisibleFileInput.files[fileInput.files.length - 1].text();
  let parsed_keywords = JSON.parse(mappings_text);
  keywords.push(parsed_keywords);
}

const clear_all = () => {
  keywords = [];
}

// An example of a form without validation
const form = createForm({});

</script>

<h1>keyword mappings create/edit</h1>

<button on:click={import_append_mappings_json}>import and append mappings json</button>
<button on:click={clear_all}>clear all mappings</button>
<button>export mappings json</button>

<TextInput {form} name='username' />
<TextInput {form} name='password' />

{#each Object.values(keywords).sort((a,b) => a.name < b.name) as keyword}
  {#each keywordInputFields as inputField}
  {/each}
  <svelte:component this={i.component} bind:this={i.inst} bind:contentSettings={i.contentSettings}/>
{/each}
