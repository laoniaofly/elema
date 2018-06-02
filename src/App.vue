<template>
  <div id="app">
    <v-header :header-data="seller"></v-header>
    <div class="tab border-1px">
			<div class="tab-item">
				<router-link to='/goods'>商品</router-link>
			</div>
			<div class="tab-item">
				<router-link to='/rating'>评论</router-link>
			</div>
			<div class="tab-item">
				<router-link to='/seller'>商家</router-link>
			</div>
		</div>
		<keep-alive>
			<router-view :seller='seller'></router-view>
		</keep-alive>
		<shopcart :select-foods='selectedFoods' :seller='seller'></shopcart>
  </div>
</template>

<script>
import header from '@/components/include/header'
import shopcart from '@/components/include/shopcart'

const ERR_OK = 0;

export default {
	name: 'App',
	components: { 
		'v-header':header,
		shopcart
	},
	data(){
		return {
			seller:{}
		};
	},
 	created(){
 		this.$http.get('/api/seller').then(response => {
 			if(response.data.errno === ERR_OK){
 				this.seller = response.data.data;
 			}
 		},response => {
 			console.log('data wrong or no data');
 		})
	},
	computed:{
		selectedFoods(){
			return this.$store.state.foods;
		}
	} 
}
</script>

<style lang="stylus" scope>
@import "./common/stylus/mixin.styl"
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7,17,27,0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77,85,93)
        &.router-link-active
          color: rgb(240,20,20)
</style>
