This repo describes an issue that happens when using `vite-plugin-vue2` with `vue-property-decorator`.

When defining props using the `@Prop` decorator from `vue-property-decorator`, the props are undefined during the component's initilization when running in production.

If you take for instance the following class component:

```vue
<template>
  <div>
    <span>{{ someValue }}</span>
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
``` 

When the component is rendered, the following output will appear on the console:

```
value when initialing data: undefined
value beforeMount: XXXXXXX
```

The expected output should be:

```
value when initialing data: XXXXXXX
value beforeMount: XXXXXXX
```

The issue only happens:
- During production when the application is built using `vite build`;
- When using @Prop decorator to define props. It seems to work fine when props are defined inside the @Component decorator's parameter;
