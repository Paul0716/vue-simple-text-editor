<template>
  <div class="about">
    <h1>This is an about page</h1>
    <simple-text-editor />
  </div>
</template>

<script lang='ts'>
import SimpleTextEditor from '@/components/SimpleTextEditor.vue';
import { Component, Vue } from 'vue-property-decorator';

@Component({
  components: {
    SimpleTextEditor,
  },
})
export default class Abount extends Vue {

}
</script>
