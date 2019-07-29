<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <div class="container mt-5">
      <div class="row">
        <div class="col-sm">
          <label for="addValue">Add Item</label>
          <input type="text" class="form-control" id="addValue" v-model="newItem"/>
          <button type="button" class="btn btn-primary" @click="addValue">Add Value</button>
        </div>
      </div>
      <div class="row">
        <div class="col-sm">
          <Multiselect 
            label="Please Select Your Fruits..."
            placeholder="Search Fruits..."
            :items="items"
            v-model="selectedItems"/>
        </div>
        <div class="col-sm">
          Current Selected Items:
          <ul>
            <li v-for="item in selectedItems" :key="item">
              {{ item }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import Multiselect from '@/components/Multiselect.vue';
import { SelectItem } from '@/models/SelectItem';

@Component({
  components: {
    HelloWorld,
    Multiselect,
  },
})
export default class App extends Vue {
  public items: string[] = ['Apple', 'Banana', 'Orange', 'Lemon', 'Lime', 'Mango', 'Pear', 'Peach'];
  public selectedItems: string[] = ['Apple', 'Orange'];
  public preselectedItems: string[] = [];
  public newItem: string = '';

  public addValue(): void {
    if (this.newItem.length > 0) {
      this.items.push(this.newItem);
      this.newItem = '';
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
