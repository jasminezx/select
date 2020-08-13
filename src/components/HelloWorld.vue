<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <br/>
    <h2>父组件的model值:{{selected.name}}</h2>
    <br/>
    <fd-select :list="selectList" v-model="selected"></fd-select>
  </div>
</template>

<script>
import fdSelect from '@/components/select';

export default {
  name: 'HelloWorld',
  components: { fdSelect },
  data() {
    return {
      msg: 'This is an example of a Vue hand-written drop-down box',
      selectList: [
        {
          name: '选项一',
          code: 1,
        }, {
          name: '选项二',
          code: 2,
        }, {
          name: '选项三',
          code: 3,
        }, {
          name: '选项四',
          code: 4,
        },
      ],
      selected: {},
    };
  },
};
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
  color: #41b883;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
  .fd-ml20 {
    margin-left: 20px;
  }
  .fd-tac {
    text-align: center;
  }
</style>
