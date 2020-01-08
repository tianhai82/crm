<script>
import Input from './Input.svelte';

export let label = '';
export let items = [];
export let value = '';
export let minCharactersToSearch = 1;
export let noResultsText = 'No results found';

export let borderColor = 'border-blue-700';
export let labelColor = 'text-blue-700';
export let helperText = '';
export let helperTextColor = '';
export let outlined = false;

let hasFocus = false;
let opened = false;
let list;
let filteredListItems;
let text;

$: icon = hasFocus ? 'arrow_drop_up' : 'arrow_drop_down';

function onDocumentClick(e) {
  console.log('onDocumentClick: ' + JSON.stringify(e.target));
  if (!e.target.closest('.autocomplete')) {
    console.log('onDocumentClick outside');
    close();
  } else {
    console.log('onDocumentClick inside');
    highlight();
  }
}
function close() {
  opened = false;
  if (!text) {
    highlightFilter = 0;
    selectItem();
  }
}
</script>

<Input {outlined} icon="{icon}"
       {label} {labelColor} {borderColor} {helperText} {helperTextColor}
       on:focus="{() => hasFocus=true}"
       on:blur="{() => hasFocus=false}"/>
<div
  class="autocomplete-list {opened ? '' : 'hidden'} is-fullwidth"
  bind:this={list}>
  {#if filteredListItems && filteredListItems.length > 0}
    {#each filteredListItems as listItem, i}
      {#if maxItemsToShowInList <= 0 || i < maxItemsToShowInList}
        <div
          class="autocomplete-list-item {i === highlightIndex ? 'selected' : ''}"
          on:click={() => onListItemClick(listItem)}>
          {#if listItem.highlighted}
            {@html listItem.highlighted.label}
          {:else}
            {@html listItem.label}
          {/if}
        </div>
      {/if}
    {/each}

    {#if maxItemsToShowInList > 0 && filteredListItems.length > maxItemsToShowInList}
      <div class="autocomplete-list-item-no-results">
        ...{filteredListItems.length - maxItemsToShowInList} results not shown
      </div>
    {/if}
  {:else if noResultsText}
    <div class="autocomplete-list-item-no-results">{noResultsText}</div>
  {/if}
</div>
<svelte:window on:click={onDocumentClick}/>
