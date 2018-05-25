<template>
  <div id="app">
    <v-header></v-header>
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

<style>
	.tab{
		display: flex;
		width: 100%;
		line-height: 40px;
		height: 40px;
		position: relative;
		overflow: hidden;
	}
	.tab::after{
		display: block;
		position: absolute;
		left: 0;
		bottom: 0;
		width: 100%;
		border-top: 1px solid rgba(7,17,27,0.1);
		content: " ";
	}
	.tab .tab-item{
		/* width: 33.3%; */
		flex: 1;
		text-align: center;
	}
	.tab .tab-item>a{
		font-size: 14px;
		color: #4d555d;
		display: block;
	}
	.tab .tab-item>a.router-link-active{
		color: #f01414;
	}
	
</style>
