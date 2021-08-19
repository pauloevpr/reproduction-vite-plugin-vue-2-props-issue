<template>
  <div>
    <span>{{ someValue}}</span>
  </div>
</template>
<script lang="ts">
import {Component, Prop} from 'vue-property-decorator';
import Vue from 'vue';

class TestClass {
  constructor(value: string) {
    console.log(`value when initialing data: ${value}`)
  }
}

@Component({
  props: {
    someValue: { type: String, required: true }
  }
})
class ChildComponent extends Vue {
  @Prop({required: true, type: String}) someValue!: string;
  _ = new TestClass(this.someValue);

  beforeMount() {
    console.log(`value beforeMount: ${this.someValue}`)
  }
}
export default ChildComponent;
</script>
