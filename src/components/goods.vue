<template>
	<div>
		<div class="goods">
			<div class="menu-wrapper" ref="menu">
				<ul>
				<li class="menu-item" v-for="(item,index) in goods" :key="index" :class="{active:currentIndex===index}" @click="scrollTo(index)">
					<span class="text border-1px">
					<span v-if="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
					</span>
				</li>
				</ul>
			</div>
			<div class="foods-wrapper" ref="foods">
				<ul>
					<li class="food-list food-list-hook" v-for="item in goods" :key="item.name">
						<h1 class="title">{{ item.name }}</h1>
						<ul>
							<li class="food-item border-1px" v-for="food in item.foods" :key="food.name" @click="selectFood(food)">
								<div class="icon">
									<img :src="food.icon" alt="" width="57" height="57"/>
								</div>
								<div class="content">
									<h2 class="name">{{ food.name }}</h2>
									<p class="description">{{ food.description }}</p>
									<div class="extra">
										<span class="count">月销{{ food.sellCount }}份</span>
										<span>好评率{{ food.rating }}%</span>
									</div>
									<div class="price">
										￥ <span class="now">{{ food.price }}</span>
										<span class="old" v-if="food.oldPrice">￥ {{food.oldPrice}}</span>
									</div>
									<div class="cartcontrol-wrapper">
										<cartcontrol :food="food"></cartcontrol>
									</div>
								</div>
							</li>
						</ul>
					</li>
				</ul>
			</div>
		</div>
		<food :food="selectedFoods" ref="food"></food> 
	</div>
</template>

<script>
import iscroll from '../../node_modules/iscroll/build/iscroll-probe' 
import bscroll from 'better-scroll'
import cartcontrol from './cartcontrol'
import food from './food'


//import shopcart from ''
const ERR_NO = 0;   //请求成功

export default {
	components:{
		cartcontrol,
		food
	},
  data () {
    return {
      goods: [],
      foods: [],
      foodListHeight: [],
      currentY: 0,
	  isActive:true,
	  selectedFoods:{}
    }
  },
  methods:{
  	scrollTo(index){
  		  let target = this.foodListHeight[index];
  		  this.foodScroll.scrollTo(0,-target,300);
  	},
  	calcHeight(){
  		//获取每个模块的高度
  		let foodList = this.$refs.foods.getElementsByClassName('food-list-hook');
  		let height = 0;
  		this.foodListHeight.push(height);
  		for(let i=0;i<foodList.length;i++){
  			height += foodList[i].clientHeight;
  			this.foodListHeight.push(height);
  		}
  	},
  	initScroll(){
  		this.menuScroll = new iscroll(this.$refs.menu,{
  			click: true
  		});
  		this.foodScroll = new iscroll(this.$refs.foods,{
				probeType: 3,  //实时监听
  			click: true
  		});
  		let _this = this;
  		this.foodScroll.on('scroll', function () {
        _this.currentY = Math.abs(Math.round(this.y));
      });
	},
	selectFood(food){ 
		this.selectedFoods = food;
		this.$refs.food.show();
	}  
  },
  created(){
  	let _this = this;
  	this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
  	this.$http.get('/api/goods').then(response => {
  		if(response.data.errno == ERR_NO){
  			_this.goods = response.data.data;
  			_this.foods = _this.goods.foods;
  		}
  		_this.$nextTick(() => {
  			if(this.menuScroll && this.menuScroll){
  				_this.menuScroll.refresh();
  				_this.foodScroll.refresh();
  			}else{
  				_this.initScroll();
					_this.calcHeight();
  			}
  		})
  	},response => {
  		alert('error,no data');
  	})
  },
  watch:{
	  selectFoods(){}  //监听商品变化
  },
  computed:{
  	currentIndex(){
  		for(let i = 0;i < this.foodListHeight.length-1;i++){
				let hTop = this.foodListHeight[i];
				let hBottom = this.foodListHeight[i+1];
        //判断currentY当前所在的区间
        if (this.currentY >= hTop-6 && this.currentY <= hBottom-6) {	
          return i;
        }
  		}
	},
	selectFoods(){
		let foods = [];
		this.goods.forEach(good => {
			good.foods.forEach(food => {
				if(food.count){  //如果物品数量存在且大于0
					foods.push(food);  //放入数组中保存
				}
			})
		});
		this.$store.commit({
			type: 'changeFoods',  //所用的方法
			foodList: foods   //将数据保存起来
		});
	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.goods{
		display: flex;
		position: absolute;
		top: 175px;
		left: 0;
		bottom: 48px;
		overflow: hidden;
		width: 100%;
	}
	.goods .menu-wrapper{
		position: relative;
		touch-action: none;
		flex: 0 0 80px;
		width: 80px;
		background: #f3f5f7;
	}
	.goods .menu-wrapper .menu-item.active{
		position: relative;
		margin-top: -1px;
		background-color: #FFFFFF;
		z-index: 10;
	}
	.goods .menu-wrapper .menu-item{
		display: table;
		height: 54px;
		padding: 0 12px;
	}
	.goods .menu-wrapper .menu-item.active .text{
		font-weight: 700;
	}
	.goods .menu-wrapper .menu-item .text{
		font-size: 12px;
		display: table-cell;
		vertical-align: middle;
		line-height: 14px;
		width: 56px;
		position: relative;
	}
	.goods .menu-wrapper .menu-item .text::after{
		display: block;
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		border-top: 1px solid rgba(7,17,27,0.1);
		content: " ";
	}
	.goods .menu-wrapper .menu-item:first-child > .text:after{
		border: none;
	}
	.goods .foods-wrapper{
		touch-action: none;
		position: relative;
		flex: 1;
	}
	.goods .foods-wrapper .title{
		padding-left: 14px;
		line-height: 26px;
		height: 26px;
		font-size: 12px;
		color: #93999f;
		background: #f3f5f7;
		border-left: 2px solid #d0dde1;
	}
	.goods .foods-wrapper .food-item{
		display: flex;
		padding-bottom: 16px;
		margin:18px 18px 0 18px;
		position: relative;
	}
	.goods .foods-wrapper .food-item::after{
		display: block;
		position: absolute;
		left: 0;
		bottom: 0;
		width: 100%;
		border-top: 1px solid rgba(7,17,27,0.1);
		content: ' ';
	}
	.goods .foods-wrapper .food-item:last-child::after{
		border: none;
	}
	.goods .foods-wrapper .food-item .icon{
		margin-right: 10px;
	}
	.goods .foods-wrapper .food-item .content{
		flex: 1;
	}
	.goods .foods-wrapper .food-item .content .name{
		line-height: 14px;
		font-size: 14px;
		margin: 2px 0 8px 0;
		height: 14px;
		color: #07111b;
	}
	.goods .foods-wrapper .food-item .content .description,
	.goods .foods-wrapper .food-item .content .extra{
		font-size: 10px;
		color: #93999f;
		line-height: 12px;
	}
	.goods .foods-wrapper .food-item .content .extra .count{
		margin-right: 10px;
	}
	.goods .foods-wrapper .food-item .content .description{
		margin-bottom: 8px;
	}
	.goods .foods-wrapper .food-item .content .price{
		line-height: 25px;
		font-size: 10px;
		color: #F01414;
		height: 25px;
		font-weight: 700;
	}
	.goods .foods-wrapper .food-item .content .price .now{
		margin-right: 10px;
		font-size: 14px;
	}
	.goods .foods-wrapper .food-item .content .price .old{
		text-decoration: line-through;
		color: #93999f;
	}
	.goods .foods-wrapper .food-item .content .cartcontrol-wrapper{
		position: absolute;
		right: 0;
		bottom: 18px;
	}
</style>
