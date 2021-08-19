<template>
  <div>
    <ChildComponent :some-value="value"></ChildComponent>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import ChildComponent from './ChildComponent.vue';

@Component({
  components: {ChildComponent}
})
export default class App extends Vue {
  value = 'XXXXXXX'
}
</script>
