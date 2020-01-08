<script>
import Tailwindcss from './Tailwindcss.svelte';
import Button from './widgets/Button.svelte';
import Input from './widgets/Input.svelte';
import Autocomplete from './widgets/Autocomplete.svelte';

export let name = '';
let error = '';
$: if (name.trim().length === 0) {
  error = 'Please enter a name';
} else {
  error = '';
}
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<Tailwindcss/>
<div class="py-5 px-32 bg-yellow-100">
  <h1>Hello {name}!</h1>
  <Button textColor="text-white" bgColor="bg-orange-500">Normal Button</Button>
  <Button textColor="text-orange-500" outlineColor="border-orange-500" outlined rounded>
    Normal Button
  </Button>
  <Button textColor="text-orange-500" text>Normal Button</Button>

  {#each Array(20) as i}
    <Input borderColor="border-green-600" labelColor="text-red-700" label="Name"
           icon="search"
           helperText={error} helperTextColor="text-red-500" bind:value={name}/>
    <Button textColor="text-white" bgColor="bg-orange-500" rounded>Normal Button</Button>
    {name} {error}
    <Input outlined borderColor="border-green-600" labelColor="text-red-700" label="Name"
           icon="search"
           helperText={error} helperTextColor="text-red-500" bind:value={name}/>
    <!--  <Autocomplete borderColor="border-green-600" labelColor="text-red-700" label="Name"-->
    <!--         helperText={error} helperTextColor="text-red-500"/>-->
    <!--    <Input borderColor="border-green-600" labelColor="text-red-700" label="Name"-->
    <!--           helperText={error} helperTextColor="text-red-500" bind:value={name}/>-->
  {/each}}
  <Button textColor="text-white" bgColor="bg-orange-500" rounded>Normal Button</Button>
  {name} {error}
</div>
