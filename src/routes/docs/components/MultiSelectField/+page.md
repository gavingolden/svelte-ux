---
name: $name
sourceUrl: $sourceUrl
docUrl: $docUrl
---

<script>
  import { mdiMagnify, mdiPlus, mdiPencil } from '@mdi/js';

  import api from '$lib/components/MultiSelectField.svelte?raw&sveld';
  import ApiDocs from '$lib/components/ApiDocs.svelte';

  import Button from '$lib/components/Button.svelte';
  import Drawer from '$lib/components/Drawer.svelte';
  import Preview from '$lib/components/Preview.svelte';
  import MenuItem from '$lib/components/MenuItem.svelte';
  import MultiSelectField from '$lib/components/MultiSelectField.svelte';
  import ToggleButton from '$lib/components/ToggleButton.svelte';

  import { delay } from '$lib/utils/promise';
  import { cls } from '$lib/utils/styles';

  const options = [
    { name: 'One', value: 1 },
    { name: 'Two', value: 2 },
    { name: 'Three', value: 3 },
    { name: 'Four', value: 4 },
  ];

  const manyOptions = Array.from({ length: 100 }).map((_, i) => ({ name: `${i + 1}`, value: i + 1 }))

  let value = [3];
</script>

# Examples

## basic

<Preview>
  <MultiSelectField
    {options}
    {value}
    on:change={(e) => value = e.detail.selection.selected}
  />
</Preview>

## disabled

<Preview>
  <MultiSelectField
    {options}
    {value}
    on:change={(e) => value = e.detail.selection.selected}
    disabled
  />
</Preview>

## many options

<Preview>
  <MultiSelectField
    options={manyOptions}
    {value}
    on:change={(e) => value = e.detail.selection.selected}
    classes={{ menu: 'max-h-[360px]' }}
    menuProps={{ autoPlacement: true }}
  />
</Preview>

## formatSelected

<Preview>
  <MultiSelectField
    {options}
    {value}
    formatSelected={({ options }) => options.map(o => o.name).join(', ') || 'None'}
    on:change={(e) => value = e.detail.selection.selected}
  />
</Preview>

## actions slot

<Preview>
  <MultiSelectField
    {options}
    {value}
    on:change={(e) => value = e.detail.selection.selected}
  >
    <div slot="actions">
      <Button color="accent" icon={mdiPlus}>Add item</Button>
    </div>
  </MultiSelectField>
</Preview>

## within Drawer

<Preview>
  <ToggleButton let:on={open} let:toggle let:toggleOff>
    Open Drawer
    <Drawer slot="toggle" {open} on:close={toggleOff} right class="w-[400px]">
      <div class="p-4">
        <MultiSelectField
          {options}
          {value}
          on:change={(e) => value = e.detail.selection.selected}
        /> 
      </div>
      <div
        class="fixed bottom-0 w-full flex justify-center bg-gray-500/25
      p-1 border-t border-gray-400"
      >
        <Button on:click={toggleOff}>Close</Button>
      </div>
    </Drawer>
  </ToggleButton>
</Preview>

# API

<ApiDocs {api} />