<script>
import Tailwindcss from './Tailwindcss.svelte';
import Button from './widgets/Button.svelte';
import Input from './widgets/Input.svelte';
import Autocomplete from './widgets/Autocomplete.svelte';
import { countries } from './countries';

export let name = '';
let countrySelected = {};
let error = '';
$: if (name.trim().length === 0) {
  error = 'Please enter a name';
} else {
  error = '';
}

const fruits = ['apple', 'orange', 'pear', 'strawberry'];
let fruit = '';

function countryChanged(item) {
  console.log(item);
}
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<Tailwindcss/>
<div class="py-5 px-32 bg-yellow-400">
  <h1>Hello {countrySelected.name?countrySelected.name:'No country selected'}!</h1>
  <Button textColor="text-white" bgColor="bg-orange-500">Normal Button</Button>
  <Button textColor="text-orange-500" outlineColor="border-orange-500" outlined rounded>
    Normal Button
  </Button>
  <Button textColor="text-orange-500" text>Normal Button</Button>
  <div>fruit: {fruit}</div>
  <Autocomplete borderColor="border-green-600" labelColor="text-red-700" label="Nameol"
                bind:value="{fruit}"
                items="{fruits}"/>

  <Input borderColor="border-green-600" labelColor="text-red-700" label="Namewertyu uiou"
         icon="search"
         helperText={error} helperTextColor="text-red-500" bind:value={name}/>
  <Button textColor="text-white" bgColor="bg-orange-500" rounded>Normal Button</Button>
  {name} {error}
  <Input outlined borderColor="border-green-600" labelColor="text-red-700"
         label="Namewert"
         icon="search"
         helperText={error} helperTextColor="text-red-500" bind:value={name}/>
  <Input outlined borderColor="border-green-600" labelColor="text-red-700"
         label="Namewert Country here is very long"
         icon="search"
         helperText={error} helperTextColor="text-red-500" bind:value={name}/>
  <Autocomplete borderColor="border-green-600" labelColor="text-red-700" label="Nameol"
                bind:value="{countrySelected}"
                items="{countries}"
                keywordsFunction="{it=>`${it.name.toLowerCase()}|^|${it.code.toLowerCase()}`}"
                labelFieldName="name" minCharactersToSearch={2} maxLen={12}
                on:change={countryChanged}
                outlined/>

  <!--    <Input borderColor="border-green-600" labelColor="text-red-700" label="Name"-->
  <!--           helperText={error} helperTextColor="text-red-500" bind:value={name}/>-->

  <Button textColor="text-white" bgColor="bg-orange-500" rounded>Normal Button</Button>
  {name} {error}
  <Input outlined borderColor="border-green-600" labelColor="text-red-700" label="b"
         icon="search"
         helperText={error} helperTextColor="text-red-500" bind:value={name}/>
  <Input outlined borderColor="border-green-600" labelColor="text-red-700" label="Name"
         icon="search"
         helperText={error} helperTextColor="text-red-500" bind:value={name}/>
</div>
