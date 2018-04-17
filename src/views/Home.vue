<template>
  <div class="hello" v-show="!loading">
  <section class="middle_mode has_action" data-hot-time="" data-group-id="" data-item-id="" data-format="0" v-for="(item,index) in articles" :key="index">
    <a href="javascript: void(0)" class="article_link clearfix " data-action-label="" data-tag="">
      
      
      <div class="item_detail desc">
        <h3 class="dotdot line2 image-margin-right">
          {{item.title}}
        </h3>
        <div class="item_info">
          <div>
            <span class="hot_label space">热</span>
            <span class="src space">生活就是娱乐</span>
            <span class="cmt space">评论 30</span>
            <span class="time" title="2018-04-12 09:34">{{item.time | formatDate}}</span>
          </div>
        </div>
      </div>
      <div class="list_img_holder">
        <img :src="item.coverUrl">
      </div>
    </a>
  </section>	
  
  <!--<section class="has_action" data-hot-time="" data-group-id="" data-item-id="" data-format="">
    <a href="javascript: void(0)" data-action-label="click_headline" data-tag="news_politics" class="article_link clearfix ">
      <div class="item_detail">
        <h3 class="dotdot line2">
          {{msg}}
        </h3>
        <div class="item_info">
          <div>
            <span class="stick_label space">置顶</span>
            <span class="src space">生活就是娱乐</span>
            <span class="cmt space">评论 30</span>
            <span class="time" title="2018-04-12 09:15">15分钟前</span>
          </div>
        </div>
      </div>
    </a>
  </section>
  <section class="middle_mode has_action" data-hot-time="" data-group-id="" data-item-id="" data-format="">
    <a href="javascript: void(0)" data-action-label="" data-tag="" class="article_link clearfix ">
      <div class="item_detail desc">
        <h3 class="dotdot line2 image-margin-right">
          {{msg}}
        </h3>
        <div class="item_info">
          <div>
            <span class="hot_label space">热</span>
            <span class="src space">生活就是娱乐</span>
            <span class="cmt space">评论 30</span>
          </div>
        </div>
      </div>
      <div class="list_img_holder">
        <img src="../assets/images/new_picture.png">
        <span class="video-btn"></span>
      </div>
    </a>
  </section>
  <section class="has_action" data-hot-time="" data-group-id="" data-item-id="" data-format="">
    <a href="javascript: void(0)" data-action-label="" data-tag="" class="article_link clearfix">
      <div class="item_detail">
        <h3 class="dotdot line2">
          {{msg}}
        </h3>
        <div class="list_image">
          <ul class="clearfix">
            <li class="list_img_holder">
              <img src="../assets/images/QQ20180409-0.png">
            </li>
            <li class="list_img_holder">
              <img src="../assets/images/QQ20180409-1.png">
            </li>
            <li class="list_img_holder">
              <img src="../assets/images/QQ20180409-2.png">
            </li>
          </ul>
        </div>
        <div class="item_info">
          <div>
            <span class="src space">生活就是娱乐</span>
            <span class="cmt space">评论30</span>
            <span class="time" title="2018-04-12 09:34">1天前</span>
          </div>
        </div>
      </div>
    </a>
  </section>
  <section class="has_action" data-hot-time="" data-group-id="" data-item-id="" data-format="0">
    <a href="javascript: void(0)" class="article_link clearfix " data-action-label="">
      <h3 class="dotdot line2">
        {{msg}}
      </h3>
      <div class="list_img_holder_large">
          <img src="../assets/images/big_img-1.png">
      </div>
      <div class="item_info">
        <span class="hot_label space">热</span>
        <span class="cmt space">评论 30</span>
        <span class="time" title="2018-04-11 14:09">1天前</span>
      </div>
    </a>
  </section>-->
  </div>
</template>

<script>
import axios from 'axios'
//自己封装的函数方法
import {getScrollTop,getScrollHeight,getWindowHeight,ajaxJSON} from '../store/MobileFun.js'
import {formatDate} from '../store/Date.js'

export default {
  name: 'Home',
  filters:{
    formatDate(time){
      var date = new Date(time);
      return formatDate(date,'yyyy-MM-dd hh:mm');
    }
  },
  data () {
    return {
      msg: '首页新闻',
      loading : true,
      articles:[]
    }
  },
  methods:{
    getDatas(){
      axios.get('http://houyishuai.dev.dc.wallan-tech.com').then(function (res){
        console.log(res.data);
        this.loading = false;
        this.articles = res.data.articles;
      }.bind(this))
      .catch(function (error) {
        console.log(error);
      });
    },

  },
  
  mounted(){
    
    // 缓存指针  
    let _this = this;  
    // 设置一个开关来避免重负请求数据  
    let sw = true;  
    // 此处使用node做了代理  
    this.getDatas(); 
    
    window.addEventListener('scroll',function(){  
         //console.log(getScrollTop()); // 可视区域高度  
         //console.log(getWindowHeight()); // 滚动高度  
         //console.log(getScrollHeight()); // 文档高度  
        // 判断是否滚动到底部  
        if(getScrollTop() + getWindowHeight() >= getScrollHeight()) {  
            // console.log(sw);  
            // 如果开关打开则加载数据  
          if(sw==true){  
            // 将开关关闭  
            sw = false;  
            axios.get('http://houyishuai.dev.dc.wallan-tech.com').then(function(res){  
            console.log(res.data);  
              // 将新获取的数据push到vue中的data，就会反应到视图中了  
              res.data.articles.forEach(function(val,index){  
                          _this.articles.push(val);  
                //console.log(val);  
              });  
              // 数据更新完毕，将开关打开  
              sw = true;  
            })  
            .catch(function(error){  
              console.log(error);  
            });     
          }  
        }  
    });  
          
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  
</style>
