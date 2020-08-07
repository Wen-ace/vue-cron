### vue-cron

### demo

```
<template>
  <vue-cron
   :value.sync="cron"
   @close="newTaskForm.showCronDialog = false"
  ></vue-cron>
</template>

<script>
import vueCron from '@/compnents/vue-cron';
epxort default {
  conpmnents: {
    'vue-cron': vueCron
  },
  data(){
    return {
      cron: ''
    }
  }
}
</script>
```
