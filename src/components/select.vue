<template>
    <div class="fd-select-box" @click="changeShow"  v-click-outside="closeDialog">
        <p v-text="scoped.selected&&scoped.selected.name?scoped.selected.name:'请选择'"></p>
        <span :class="['fd-arrow icon iconfont',{'fd-down':scoped.showFlag}]">&#xe6a4;</span>
        <ul class="fd-select-list" v-show="scoped.showFlag">
            <li v-for="(item,index) in list"
                :key="index+'select'"
                @click.stop="changeValue(item)"
                :class="{'active':scoped.selected&&item.code===scoped.selected.code}">
                {{item.name}}</li>
        </ul>
    </div>
</template>

<script>
import derections from '@/assets/js/directions';

export default {
  name: 'fdSselect',
  model: {
    prop: 'selected',
    event: 'changeValue',
  },
  props: {
    list: {
      type: Array,
      required: true,
    },
    selected: Object,
  },
  data() {
    return {
      scoped: {
        // 是否展示下面的列表
        showFlag: false,
        // 当前选中的
        selected: this.selected,
      },
    };
  },
  directives: { clickOutside: derections.clickOutside },
  methods: {
    // 值改变后传给父组件，因为组件定义了model，所以父组件相当于执行了绑定的model值=emit出去的值
    changeValue(item) {
      this.scoped.selected = item;
      this.scoped.showFlag = false;
      this.$emit('changeValue', this.scoped.selected);
    },
    // 改变下拉选项的显隐
    changeShow() {
      this.scoped.showFlag = !this.scoped.showFlag;
    },
    closeDialog() {
      this.scoped.showFlag = false;
    },
  },
};
</script>

<style scoped lang="less">
    @import "../assets/css/iconFont/iconfont.css";
    .fd-select-box {
        position: relative;
        width: 200px;
        padding-right: 40px;
        padding-left: 10px;
        height: 36px;
        margin: 30px auto;
        line-height: 36px;
        border: 1px solid #41b883;
        border-radius: 4px;
        color: #000;
        font-size: 14px;
        text-align: left;
        cursor: pointer;
        box-sizing: border-box;

        .fd-arrow {
            position: absolute;
            top: 0;
            right: 0;
            font-size: 30px;
            transition: all 200ms;

            &.fd-down {
                transform: rotate(180deg);
            }
        }

        .fd-select-list {
            position: absolute;
            width: 100%;
            max-height: 200px;
            overflow: auto;
            list-style: none;
            top: 36px;
            left: 0;
            background: #fff;
            box-shadow: 0 0 5px rgba(0,0,0,0.2);
            z-index: 9;

            li {
                padding-left: 12px;
                line-height: 30px;
                cursor: pointer;

                &:hover {
                    background: rgba(65, 191, 138, 0.2);
                }

                &.active {
                    background: rgba(65, 191, 138, 0.9);
                    color: #fff;
                }
            }
        }
    }

</style>
