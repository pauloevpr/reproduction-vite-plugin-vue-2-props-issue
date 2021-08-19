<template>
  <div>
    <span>{{ someValue}}</span>
  </div>
</template>
<script lang="ts">
import {Component, Prop, Vue} from 'vue-property-decorator';

class TestClass {
  constructor(value: string) {
    console.log(`value when initialing data: ${value}`)
  }
}

@Component
class ChildComponent extends Vue {
  @Prop({required: true, type: String}) someValue!: string;
  dataField = new TestClass(this.someValue);

  beforeMount() {
    console.log(`value beforeMount: ${this.someValue}`)
  }
}
export default ChildComponent;
</script>
