# vue-player360

Vue sound player component

## How to install

`npm install  @serh/vue-player360 --save`

## Example

```html
<template>
    <VuePlayer360 url="https://file-examples-com.github.io/uploads/2017/11/file_example_MP3_1MG.mp3"></VuePlayer360>
</template>
<script>
import VuePlayer360 from "@serh/vue-player360";
export default {
  components: {
    VuePlayer360,
  },
};
</script>
```

### Props

| name              | type           | default | | description |
| --- | --- | --- | --- | --- | 
| url | String |  | true | The url of the sound to play.| The url of the sound to play. |