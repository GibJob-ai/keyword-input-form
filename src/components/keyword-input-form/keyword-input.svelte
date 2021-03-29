<script>
  /* import createForm from '@spaceavocado/svelte-form'; */
  import TextInput from '../input/text.svelte';

  class KeywordInput {
    constructor(name, aliases, related, category){
      this.name = name;
      this.aliases = aliases;
      this.related = related;
      this.category = category;
    }
  }

  class InputElement {
    constructor(name, input_type, hover_text, value, readonly) {
      this.name = name;
      this.input_type = input_type;
      this.hover_text = hover_text;
      this.value = value;
      this.readonly
    }
  }

  export let data = new KeywordInput(
    name=new InputElement(name="name",hover_text=hover_text, value="", readonly=false),
    aliases=[],
    related={}
  );
  export let show_details = false;
  export let editing = false;
</script>

<style lang="scss">

  .keyword-main{
    display: flex;
    flex-flow: row nowrap;
    .name {
      flex: 20vw 0 0;
      margin: 0;
      padding: 15px;
    }
    .section{
      display: flex;
      flex-flow: column nowrap;
      .mini-title {
        font: {
          size: 8px;
        }
        margin: 0;
        padding: 0;
        flex: 12px 0 0;
      }
      .content-summary{
      }
      .content-full{
        display: flex;
        flex-flow: column nowrap;
        .item.related.show_details{
          display: flex;
          flex-flow: row nowrap;
          .item-name{
            
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

<div class='main'>
  <div class='name'>
    <input type="text" bind:value={data.name.value}/>
  </div>
  <div class='section related'>
    <h1 class='mini-title'>related</h1>
    {#each Object.keys(data.related) as k}
      <div class="item related" class:show_details>{data.related[k]}{show_details?",":""}
        <div class="item-name">{k}</div>
        {#if show_details}
          <input type=number bind:value={data.related}>
        {/if}
      </div>
    {/each}
  </div>
</div>

