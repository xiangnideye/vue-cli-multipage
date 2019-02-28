<template>
  <div class="vue_select">
    <div class="button_add" @click="addSelect">add +</div>
    <ul class="select_list">
      <li class="select_item" v-for="(item, index) in selectArr" :key="index">
        <span class="name">{{item.name}}</span>
        <span class="close" @click="deleteSelect(index)">X</span>
      </li>
    </ul>
    <v-select @cancel="closeSelect" @confirm="confirmSelect" v-show="selectHide"></v-select>
  </div>
</template>

<script>
  import select from '../../components/select';

  export default {
    components:  {
      'v-select': select
    },
    data () {
      return {
        selectHide: false,
        selectArr: [],
      }
    },
    methods: {
      //
      deleteSelect (index) {
        this.selectArr.splice(index, 1)
      },
      //新增
      addSelect () {
        this.selectHide = true;
      },
      //取消
      closeSelect () {
        this.selectHide = false;
      },
      //保存获取数据
      confirmSelect (data) {
        console.log(data)
        this.selectArr = data;
        this.selectHide = false;
      }
    }
  }
</script>

<style>
  .vue_select{
    width: 100%;
  }
  .button_add{
    margin: 100px auto 20px;
    width: 360px;
    height: 44px;
    line-height: 44px;
    text-align: center;
    background: #FFFFFF;
    border: 1px dashed #4C9DFF;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    color: #4C9DFF;
  }
  .select_list{
    margin: 0 auto;
    width: 360px;
  }
  .select_item{
    padding-left: 16px;
    margin-bottom: 10px;
    height: 40px;
    line-height: 40px;
    background: #FFFFFF;
    border: 1px dashed #E6ECF2;
    border-radius: 4px;
  }
  .name{
    font-size: 14px;
    color: #283644;   
  }
  .close{
    float: right;
    margin-right: 20px;
    cursor: pointer;
  }
</style>
