<template>
  <div :class="protalCss.silderBox">
        <div :class="protalCss.menuItem" v-for="(order, one) in datamenu">
              <div v-if="one.subMenus" :class="protalCss.menuTitle" @click="changeSubBox(one)">
                <icon :iconname="one.icon" :class='protalCss.menuicon'></icon> {{one.name}}  <icon  :class="protalCss.directicon"  iconname="icon-right3"></icon>
              </div>
              <div  :class="protalCss.menuSubAction" v-else>
                <a v-link="one.url"><icon :class='protalCss.menuicon' :iconname="one.icon"></icon> {{one.name}} <icon :class="protalCss.directicon"  iconname="icon-right3"></icon> </a>
              </div>
              <div :class="protalCss.subMenus" v-show="one.show">
                <a v-link="subone.url"  v-for="subone in one.subMenus">{{subone.name}}</a>
              </div>
        </div>
  </div>
</template>

<script>
import protalCss from './portal.css';
import icon from "component/sprite/icon";
export default {
    data(){
      return {
        protalCss,
        datamenu:[
          {name:"首页", url:"/index", icon:"icon-home"},
          {name:"账户管理", url:"/accountmgr", icon:"icon-tip"},
          {name:"员工管理", url:"/employee", icon:"icon-tip"},
          {name:"用户管理", url:"/user", icon:"icon-tip"},
          {name:"客户管理", url:"/custom", icon:"icon-tip"},
          {name:"销售订单管理", url:"/sale", icon:"icon-tip"},
          {name:"采购管理", icon:"icon-tip",show: false,subMenus:[{
                  url:"/purchase",name:"采购订单管理"
              },//{
                  // url:"/prestoremgr",name:"备货管理"
              // },{
                  // url:"/prestorevalidate",name:"备货审核"}
              ]
          },
          {name:"订制品设计申请", url:"/specapplydesignmgr", icon:"icon-tip"},
          {name:"订制品设计管理", url:"/specdesignmgr", icon:"icon-tip"},
          {name:"加急卡管理", url:"/urgent", icon:"icon-tip"}
        ]
      }
    },

    ready: function(){
      let path = this.$route.path;
      for (let i = 0; i < this.datamenu.length; i++) {
            let one = this.datamenu[i];
            if(!one.subMenus || one.subMenus.length == 0) continue;
            let subStr = JSON.stringify(one.subMenus);
            if(subStr.indexOf(path) != -1) {
              console.log(one);
              one.show = true;
              break;
            }
      }
    },

    route:{
      data: function(){
        alert(1)
      }
    },
    created: function(){

      // var demoinfo = {name:"开发文档", icon:"icon-tip", subMenus:[{url:"/demo/datepicker",name:"日历"},
      //                                           {url:"/demo/dialog",name:"对话框"},{url:"/demo/paginate",name:"分页"},{url:"/demo/tab",name:"tab"},
      //                                           {url:"/demo/datatable",name:"表格"}, {url:"/demo/combobox",name:"下拉"},  {url:"/demo/filetest",name:"文件上传"},
      //                                           {url:"/demo/search",name:"查询"},{url:"/demo/form",name:"表单"},{url:"/demo/tablesp", name:"手风琴表格"}], show: false}
      // this.datamenu.push(demoinfo);
    },
    methods:{
      changeSubBox: function(one) {
          one.show = !one.show;
      }
    },
    components:{
      icon
    }

}
</script>
