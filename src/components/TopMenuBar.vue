<template>
  <div class="top_menu_bar">
    <div class="top_menu_more">
      <div class="list_shadow"></div>
      <a class="more_btn" href="javascript:void(0)"></a>
    </div>
    <div class="top_menu_list">
      <router-link :to="item.url" :data-channel="item.channel" data-query="" class="btn" v-for='(item,index) in navbar' :key="index">
        {{item.text}}
      </router-link>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TopMenuBar',
    data(){
      return {
        //频道数据
        navbar:[
        {
          text:'推荐',
          url:'/home',
          channel:'_all_'
        },
        {
          text:'热点',
          url:'/hot/',
          channel:'news_hot'
        },
        {
          text:'社会',
          url:'/society/',
          channel:'news_society'
        },
        {
          text:'汽车',
          url:'/car/',
          channel:'news_car'
        },
        {
          text:'关注',
          url:'/focus/',
          channel:'news_focus'
        },
        {
          text:'上海',
          url:'/shanghai/',
          channel:'news_shanghai'
        },
        {
          text:'军事',
          url:'/military/',
          channel:'news_military'
        },
        {
          text:'体育',
          url:'/sports/',
          channel:'news_sports'
        },
        {
          text:'财经',
          url:'/finance/',
          channel:'news_finance'
        },
        ]
      }
    }
  }

</script>

<style>
</style>