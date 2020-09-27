
<template>
 <DateTimer :dateTime="value1" @onTime="onChangeTime"/>
</template>

<script>
import DateTimer from './DateTimer'

import { liveStatusList } from "./constance";
export default {
  methods: {
  
    onChangeTime(val){
       this.value1 = val
    },
    
  },
 
  data() {
    return {
      value1: new Date().getTime(),
    };
  },
};
</script>
<style  lang="scss">

</style>