 <template>
  <div id="app">
	<div class="indexContainer withHeader">
  	<headers></headers>
    <div>
      
  		<top-menu-bar></top-menu-bar>
  		
      <div id="div1" class="content0">
        <div class="scroll_bar">
          <div class="bar1">⇣</div>
          <div class="bar2">下拉刷新</div>
        </div>
        
        <div id="div2">
          <content id="pageletListContent" class="feed-list-container">
            <div class="list-content">
              <transition enter-active-class="animated bounceInLeft" leave-active-class="animated bounceOutRight">
                <router-view></router-view>
              </transition>
              
            </div>
            <div class="list_bottom">
              <section class="loadmoretip">
                <a href="#">加载中...</a>
              </section>
            </div>
          </content>
        </div>
        
      </div>
      
    </div>
  </div>
    
  </div>
</template>

<script>
import Headers from '@/components/Headers'
import TopMenuBar from '@/components/TopMenuBar'
export default {
  name: 'App',
  components:{
    'headers':Headers,
    'top-menu-bar':TopMenuBar
  },
  data(){
    return{
      
    }
  },
}
</script>

<style>
/*#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
.router-link-exact-active{
  color:#00D8B7 !important;
}
</style>
