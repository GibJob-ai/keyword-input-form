<script>
  /* import createForm from '@spaceavocado/svelte-form'; */
  /* import TextInput from '../input/text.svelte'; */
  import KeywordInputData from './keyword_input_data.js';

  /* class Name { */
    /* constructor(name, input_type, hover_text, value, readonly) { */
      /* this.name = name; */
      /* this.input_type = input_type; */
      /* this.hover_text = hover_text; */
      /* this.value = value; */
      /* this.readonly */
    /* } */
  /* } */

  export let data;
  export let all_keywords;

  $: related_text = data.related.map((i, n) => {
      return `${i.name}:${i.value}`;
    }).join(', ');

  let errMessage = '';

  const save = () => {
    if (data.show_details){
      const valid = data.valid(all_keywords);
      if (valid.valid){
        data.show_details = false;
        errMessage = '';
      }
      else{
        errMessage = valid.message;
      }
    }
    else{
      data.show_details = true;
      errMessage = '';
    }
  }
</script>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
  }
  .keyword-main{
    display: flex;
    flex-flow: row nowrap;
    justify-content: flex-start;
    .name {
      flex: 20vw 0 0;
      margin: 0;
      padding: 15px;
      input{
        width: 100%;
        font-size: 23px;
      }
    }
    .section{
      display: flex;
      flex-flow: column nowrap;
      margin: 5px 10px;
      .mini-title {
        font: {
          size: 14px;
        }
        margin: 0;
        padding: 0;
        flex: 12px 0 0;
      }
      .content{
        display: flex;
        flex-flow: row nowrap;
      }
      .content.show_details{
        flex-flow: column nowrap;
        .item.related.show_details{
          display: flex;
          flex-flow: row nowrap;
          .item-name{
            width: 100%;
          }
          input.number_input{
            max-width: 40px;
          }
          .item-relevance{

          }
        }
      }
    }
    .related-section {

    }
    .alias-section {

    }
  }

  
</style>

<div class='keyword-main'>
  <div class='name'>
    <input type="text" bind:value={data.name}/>
  </div>
  <div class='section related-section'>
    <h1 class='mini-title'>related</h1>
    <div class='content' class:show_details={data.show_details}>
      {#if data.show_details}
        {#each data.related as related}
          <div class="item related" class:show_details={data.show_details}>
            <input type="text" bind:value={related.name} readonly={!data.show_details}>
            <input type=number class='number_input' bind:value={related.value}>
          </div>
        {/each}
      {:else}
        <div>{related_text}</div>
      {/if}
      {#if data.show_details}
        <button on:click={() => {data.related = [...data.related, {'name': '', 'value': null}]}}>add related keyword</button>
      {/if}
    </div>
  </div>
  <div class='section alias-section'>
    <h1 class='mini-title'>aliases</h1>
    <div class='content' class:show_details={data.show_details}>
      {#each data.aliases as alias, i}
        <div class='item alias' class:show_details={data.show_details}>
          <input type="text" bind:value={alias} readonly={!data.show_details}>
        </div>
      {/each}
      {#if data.show_details}
        <button on:click={() => {data.aliases = [...data.aliases, ""]}}>add alias</button>
      {/if}
    </div>
  </div>
  <button on:click={save}>{data.show_details?"save":"show/edit details"}</button>
</div>
{#if errMessage}
  <h2 style="color: red">{errMessage}</h2>
{/if}

