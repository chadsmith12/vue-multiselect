# multiselect-vue
This is a basic multiselect component written in TypeScript. It was modified from [this](https://codepen.io/SkyHyzer/pen/xvOVZq).

The component shows a simple way to provide multiselect with searching ability. 
The component is not tested and isn't mean to be used in a production environment, but an example of a multiselect component.

## Example Use
Example Usage of the comnponent:
```
<Multiselect 
    label="Please Select Your Fruits..."
    placeholder="Search Fruits..."
    :items="items"
    v-model="selectedItems"/>
```

### v-model Support
This component supports `v-model` with a `string[]`. 

### Props
Component supports the following props:
* label: `string` - The label to show for the multiselect.
* placeholder:  `string` - The placeholder in the search box.
* items: `string[]` - The items that appear in the search box.
* value: `string[]` - The input value of the component.

