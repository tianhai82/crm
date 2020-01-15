<script>
import { createEventDispatcher } from 'svelte';
import Input from './Input.svelte';

const dispatch = createEventDispatcher();

export let label = '';
export let items = [];
export let value = '';
export let minCharactersToSearch = 1;
export let noResultsText = 'No results found';
export let maxLen = undefined;

export let borderColor = 'border-blue-700';
export let labelColor = 'text-blue-700';
export let helperText = '';
export let helperTextColor = '';
export let outlined = false;

export let labelFieldName = undefined;
export let keywordsFieldName = labelFieldName;
export let keywordsFunction = function (item) {
  if (item === undefined || item === null) {
    return '';
  }
  return keywordsFieldName ? item[keywordsFieldName] : item;
};

let filteredListItems = [];
let text = '';
let listVisible = false;
let itemClicked = false;
let icon;

$: icon = listVisible ? 'arrow_drop_up' : 'arrow_drop_down';
$: {
  if (text.length >= minCharactersToSearch) {
    const tempFiltered = items.filter(it => keywordsFunction(it)
      .includes(text.toLowerCase()));
    filteredListItems = maxLen ? tempFiltered.slice(0, maxLen) : tempFiltered;
  }
}

function setVal(item) {
  itemClicked = false;
  listVisible = false;
  value = item;
  dispatch('change', item);
  if (typeof item === 'string') {
    text = item;
  } else {
    text = item[labelFieldName];
  }

}

function handleKeydown(e) {
  listVisible = e.key !== 'Escape';
}

function onFocus(e) {
  listVisible = true;
  if (text) {
    e.target.selectionStart = 0;
    e.target.selectionEnd = text.length;
  }
}

function onBlur() {
  if (itemClicked) return;
  listVisible = false;
  if (typeof value === 'string') {
    text = value || '';
  } else {
    text = value[labelFieldName] || '';
  }
}
</script>

<div class="relative">
  <Input {outlined} icon="{icon}"
         bind:value={text}
         {label} {labelColor} {borderColor} {helperText} {helperTextColor}
         on:keydown={handleKeydown}
         on:blur={onBlur}
         on:focus="{onFocus}"/>
  <div
    class="absolute -mt-4 bg-white w-full shadow-md z-10 {listVisible && text.length>=minCharactersToSearch ? '' : 'hidden'}">
    {#if filteredListItems.length>0}
      <ul class="my-2">
        {#each filteredListItems as item}
          <li class="p-3 cursor-pointer hover:bg-gray-200"
              on:mousedown={()=> itemClicked = true}
              on:click|stopPropagation|preventDefault={setVal(item)}>{labelFieldName? item[labelFieldName]: item}</li>
        {/each}
      </ul>
    {:else}
      <div class="m-3" on:mousedown|stopPropagation|preventDefault>{noResultsText}</div>
    {/if}
  </div>
</div>
