<template>
  <div id="addClassify">
    <div class="main-container">
      <div class="padding-md">
        <div class="main">
          <div class="design smart-widget widget-dark-blue">
            <div class="smart-widget-header"><span class="text m-left-sm"><i class="icon iconfont icon-document"></i>添加分类</span></div>
            <div class="form-group has-success clearfix">
              <label class="control-label" for="inputSuccess1">分类标题：</label>
              <input type="text" class="form-control" id="inputSuccess1" aria-describedby="helpBlock2" v-model="initclasifyData.title">
            </div>
            <div class="form-group has-success clearfix">
              <label class="control-label" for="inputSuccess2">关键字标题</label>
              <input type="text" class="form-control" id="inputSuccess2" aria-describedby="helpBlock2" v-model="initclasifyData.keytitle">
            </div>
            <div class="form-group has-success clearfix">
              <label class="control-label" for="inputSuccess3">关键字描述：</label>
              <textarea class="form-control" rows="5" id="inputSuccess3" v-model="initclasifyData.keydesc"></textarea>
            </div>
            <div class="form-group has-success clearfix">
              <label class="control-label" for="inputSuccess11">排序：</label>
              <input type="text" class="form-control" id="inputSuccess11" aria-describedby="helpBlock2" v-model="initclasifyData.sort">
            </div>
            <button class="btn btn-success btn-sm no-shadow" id="classify-submit" @click="submit">提交</button>
            <button class="btn btn-success btn-sm no-shadow" id="classify-cancel" @click="cancel">取消</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "addClassify",
  mounted() {
      localStorage.setItem('classifyData',JSON.stringify(this.classifyData))
      this.classifyData = JSON.parse(localStorage.getItem('classifyData'));
  },
  data(){
    return{
      initclasifyData:{
        title:'',
        keytitle:'',
        keydesc:'',
        sort:'',
      },
      classifyData:[
        {
          id:1,
          title:'箱包',
          keytitle:'双肩包',
          keydesc:'各种款式箱包',
          sort:10
        },
        {
          id:2,
          title:'单鞋',
          keytitle:'初秋单鞋',
          keydesc:'各种款式单鞋',
          sort:11
        },
        {
          id:3,
          title:'家居',
          keytitle:'沙发',
          keydesc:'各种款式沙发',
          sort:6
        },
        {
          id:4,
          title:'食品零售',
          keytitle:'牛肉、猪肉、鸡肉',
          keydesc:'各种肉',
          sort:10
        },
        {
          id:5,
          title:'个人护理',
          keytitle:'护肤套装',
          keydesc:'各种护肤产品',
          sort:2
        },
      ]
    }
  },
  methods: {
    submit() {
      console.log(this.classifyData);
      let max = maxId(this.classifyData)
      this.classifyData.unshift({
        id:++max,
        title:this.initclasifyData.title,
        keytitle:this.initclasifyData.keytitle,
        keydesc:this.initclasifyData.keydesc,
        sort:this.initclasifyData.sort,
      })
      localStorage.setItem('classifyData',JSON.stringify(this.classifyData))
      this.initclasifyData.title=this.initclasifyData.keytitle=this.initclasifyData.keydesc=this.initclasifyData.sort='';
    },
    cancel(){
      this.initclasifyData.title=this.initclasifyData.keytitle=this.initclasifyData.keydesc=this.initclasifyData.sort='';
    }
  }
}


function maxId(data){
    let max = 0;
    data.forEach(e=>{
      if(max<e.id){
        max = e.id
      }
    })
    return max;
}

function getItem(data){
  return JSON.parse(localStorage.getItem('data')) || [];
}
</script>
<style  scoped>
.control-label{
  color:#2baab1;
}
.tiptitle{
  display:inline-block;
  vertical-align: middle;
  padding:8px;
}
#inputSuccess11,#inputSuccess1{
  width:50%;
}
.classify1{
  margin-bottom: 15px;
}
#classify-submit,#classify-cancel{
  width:100px;
  margin-left:100px;
}
#classify-cancel{
  margin-left:30px;
}
</style>
