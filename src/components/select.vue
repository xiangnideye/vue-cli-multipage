<template>
  <div class="select_bg">
    <div class="select">
      <div class="select_head">
        <span class="text_add">Add</span>
        <span class="icon_close" @click="clickCancel">X</span>
      </div>
      <div class="select_body clear">
        <div class="select_left">
          <input type="text" class="input_select" placeholder="Search" v-on:input="getSelectValue" v-model="selectValue">
          <ul class="left_data">
            <li class="item_data" v-for="(item, index) in dataArr" :class="{isActive:item.isActive}" @click="selectData(item, index)" :key="index">{{item.name}}</li>
          </ul>
        </div>
        <div class="select_right">
          <span class="text_select">Select</span>
          <ul class="left_data">
            <li class="item_data select_data" v-for="(item, index) in selectArr" @click="delect_itme(item, index)" :key="index">{{item.name}}</li>
          </ul>
        </div>
      </div>
      <div class="button_box clear">
        <button class="button_cancel" @click="clickCancel">cancel</button>
        <button class="button_confirm" @click="clickConfirm">confirm</button>
      </div>
    </div>
  </div>
</template>

<script>
import '../common/css/reset.min.css'
export default {
  data () {
    return {
      dataArr: [
        {
          id: 0,
          name: '选择name 1',
          isActive: false
        },
         {
          id: 1,
          name: '选择name 2',
          isActive: false
        },
         {
          id: 2,
          name: '选择name 3',
          isActive: false
        },
         {
          id: 3,
          name: '选择name 4',
          isActive: false
        },
      ],
      newSelectArr: [],
      selectArr :[],
      selectValue: '',
    }
  },
  mounted () {
    this.newSelectArr = this.dataArr.slice(0);
  },
  methods: {
    //
    clickConfirm () {
      this.$emit('confirm', this.selectArr);
    },
    //
    clickCancel () {
      this.$emit('cancel', true);
    },
    //过滤查询
    filterFunction (query) {
      if(query){
        setTimeout(() => {
					this.$nextTick(() => {
						this.dataArr = this.newSelectArr.filter(item => {
							return item.name.toLowerCase().indexOf(query.toLowerCase()) > -1;
            });
					});
				}, 200);
      }
    },
    getSelectValue () {
      if(this.selectValue != '') {
        this.filterFunction(this.selectValue)
      }else{
	      this.dataArr = this.newSelectArr;
      }
      
    },
    selectData (el, index) {
      el.isActive = true;
      if(this.selectArr.indexOf(el) == -1)this.selectArr.push(el);
    },
    delect_itme (el, index) {
      this.dataArr.map(x => {
        if(x.id == el.id) x.isActive = false;
      });
      this.selectArr.splice(index, 1);
    }
  }
}
</script>

<style>
  .select_bg{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .5);
  }
  .select{
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -235px 0 0 -310px;
    width: 620px;
    height: 470px;
    background: #FFFFFF;
    border-radius: 4px;
  }
  .select_head{
    position: relative;
    background: #F9FAFC;
    border-radius: 4px 4px 0 0;
  }
  .text_add{
    display: block;
    width: 100%;
    height: 60px;
    line-height: 60px;
    text-align: center;
    font-size: 16px;
    color: #283644;
  }
  .icon_close{
    position: absolute;
    top: 23px;
    right: 25px;
    font-size: 14px;
    color:  #CCCCCE;
    cursor: pointer;
  }
  .select_body {
    padding: 40px 50px;
  }
  .select_left, .select_right{
    float: left;
    width: 250px;
    height: 260px;
    border: 1px solid #E6ECF2;
  }
  .select_right{
    float: right;
  }
  .input_select{
    padding-left: 15px;
    width: 235px;
    height: 34px;
    border: none;
    border-bottom: 1px solid #E6ECF2;
  }
  .left_data{
    padding-left: 15px;
    padding-top: 10px;
    width: 235px;
    height: 225px;
    overflow-y: auto;
  }
  .item_data{
    margin-bottom: 8px;
    font-size: 14px;
    color: #283644;
    cursor: pointer;
  }
  .isActive {
    color: #4C9DFF;
  }
  .item_data:hover{
    color: #4C9DFF;
  }
  .select_data:hover{
    text-decoration: line-through;
  }
  .text_select{
    display: block;
    padding-left: 16px;
    height: 35px;
    line-height: 35px;
    background: #F9FAFC;
    font-size: 14px;
    color: #283644;
  }
  .button_box{
    margin: 0 auto;
    width: 260px;
    height: 44px;
  }
  .button_cancel, .button_confirm{
    float: left;
    width: 120px;
    height: 44px;
    text-align: center;
    line-height: 44px;
    background: #FFFFFF;
    border: 1px solid #E6ECF2;
    border-radius: 2px;
    cursor: pointer;
  }
  .button_confirm {
    margin-left: 16px;
    background: #4C9DFF;
    color: #FFFFFF;
  }
</style>