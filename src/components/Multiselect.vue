<template>
<div>
    <label>{{ label }}</label>

    <div class="search-box">
        <input type="search"
            class="form-control"
            :placeholder="placeholder" 
            :aria-placeholder="placeholder"
            v-model="searchValue">
    </div>
    <div class="selected" :class="{open: hasSelectedItems}">
        <div v-for="item in value" :key="item" class="choice">
            {{ item }}<i class="fa fa-times unselect" @click="clickedItem(item)"></i>
        </div>
    </div>
    <div class="list-group list-group-flush">
        <a v-for="(item, index) in filteredItems" 
            :key="index" 
            href="#" 
            @click="clickedItem(item)" 
            class="list-group-item list-group-item-action"
            :class="{active: isSelected(item)}">

            <input type="checkbox" hidden />
            <i class="far fa-square"></i>
            <span>{{ item }}</span>
        </a>
    </div>
</div>

</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator';
import { SelectItem } from '@/models/SelectItem';

@Component
export default class Multiselect extends Vue {
    public searchValue: string = '';
    @Prop() private label!: string;
    @Prop({default: 'Search...'}) private placeholder!: string;
    @Prop() private items!: string[];
    @Prop() private value!: string[];

    private get hasSelectedItems(): boolean {
        return this.value.length > 0;
    }

    private get filteredItems(): string[] {
        if (!this.isSearching) {
            return this.items;
        }

        const searchLower = this.searchValue.toLowerCase();
        return this.items.filter((item) => item.toLowerCase().indexOf(searchLower) > -1);
    }

    private get isSearching(): boolean {
        return this.searchValue.length >  0;
    }

    private clickedItem(selectedItem: string): void {
        const isItemSelected = this.isSelected(selectedItem);
        if (isItemSelected) {
            const indexToDelete = this.value.indexOf(selectedItem);
            this.$delete(this.value, indexToDelete);
        } else {
            this.value.push(selectedItem);
        }

        this.onInputChange();
    }

    @Emit('input')
    private onInputChange() {
        return this.value;
    }

    private isSelected(selectedItem: string): boolean {
        return this.value.includes(selectedItem);
    }
}
</script>

<style scoped>
.search-box {
  position: relative;
}
.search-box .form-control {
  background-color: transparent;
  border-radius: 0.25rem 0.25rem 0 0;
  margin-bottom: -1px;
  padding-left: 2.75rem;
  position: relative;
  z-index: 10;
}
.search-box:before {
  content: "\f002";
  color: #999;
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  padding: 0.5rem 1rem;
  position: absolute;
}

.selected {
  border-right: 1px solid #ced4da;
  border-left: 1px solid #ced4da;
  display: flex;
  max-height: 0;
  overflow-x: auto;
  overflow-y: hidden;
  transition: 0.15s all ease-in-out;
}
.selected.open {
  max-height: 3rem;
}
.selected .choice {
  background: #f5f6f8;
  border-right: 1px solid #ced4da;
  display: flex;
  align-items: center;
  font-size: 0.75rem;
  height: 2rem;
  padding-left: 0.5rem;
}
.selected .choice i {
  color: #999;
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: 0.7rem;
  height: 100%;
  padding: 0 0.75rem;
  transition: 0.15s color ease-in-out;
}
.selected .choice i:hover {
  color: #000;
}

.list-group {
  border: 1px solid #ced4da;
  border-radius: 0 0 0.25rem 0.25rem;
  height: 205px;
  overflow-y: auto;
}
.list-group .list-group-item {
  border-top: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  margin: 0;
  outline: none;
  padding: 0.5rem 1rem;
  transition: 0.15s background-color ease-in-out;
}
.list-group .list-group-item i {
  margin-right: 1rem;
  transform: rotate(270deg);
  transition: 0.15s transform ease-in-out;
}
.list-group .list-group-item i:before {
  transition: 0.15s transform ease-in-out;
}
.list-group .list-group-item.active i {
  transform: rotate(360deg);
}
.list-group .list-group-item.active i:before {
  content: "\f00c";
  font-weight: 900;
}

</style>
