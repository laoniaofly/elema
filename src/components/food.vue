<template>
	<transition name="move">
		<div class="food" ref="food" v-show="foodShow">
			<div class="food-content">
				<div class="image_wrapper">
					<img :src="food.image" alt="" class="img">
					<div class="back" @click.stop.prevent="back">
						返回<i class="icon-arrow_lift"></i>
					</div>
				</div>
				<div class="content">
					<h1 class="title">{{ food.name }}</h1>
					<div class="detail">
						<span class="sell-count">月售{{ food.sellCount }}份</span>
						<span class="rating">好评率{{ food.rating }}%</span>
					</div>
					<div class="price">
						￥<span class="now"> {{ food.price }}</span>
						<span class="old" v-show="food.oldPrice">￥{{ food.oldPrice }}</span>
					</div>
					<div class="buy">加入购物车</div>
					<div class="cartcontrol-wrapper">
						<div class="cartcontrol">
							<div class="decrease">
								<span class="inner icon-remove_circle_outline"></span>
							</div>
							<div class="count"></div>
							<div class="add icon-add_circle"></div>
						</div>
					</div>
				</div>
				<split v-show="food.info"></split>
				<div class="info" v-show="food.info">
					<h1 class="title">{{ foodMsg.spMsg }}</h1>
					<p class="text">{{ food.info }}</p>
				</div>
				<split></split>
				<div class="rating">
					<h1 class="title">{{ foodMsg.sppj }}</h1>
					<ratingSelect @onlyContentChange='onlyContentChange' @typeChange='typeChange' :only-content="onlyContent" :desc="desc" :select-type='selectType' :ratings='food.ratings'></ratingSelect>
					<div class="rating-wrapper">
						<ul v-show="food.ratings && food.ratings.length>0">
							<li class="rating-item border-1px" v-for="rating in food.ratings" v-show="needShow(rating.rateType,rating.text)">
								<div class="user">
									<span class="name">{{ rating.username }}</span>
									<img :src="rating.avatar" width="12" height="12">
								</div>
								<div class="time">{{ rating.rateTime | format }}</div>
								<p class="text">
									<span class="icon-thump_up"></span>{{ rating.text }}
								</p>
							</li>
						</ul>
						<div v-show="!food.ratings || food.ratings.length===0" class="no-rating">暂无评价</div>
					</div>
				</div>
			</div>
		</div>
	</transition>
</template>

<script>
import split from './split'
import iscroll from '../../node_modules/iscroll/build/iscroll-probe'
import ratingSelect from './ratingselect'
import { formatDate } from '../assets/js/formatDate' 

const ALL=2;
const POSITIVE=0;
const NAGATIVE=1;

export default {
  props:{
  	food:{
  		type:Object
  	},
  	foodMsg:{
  		type:Object,
  		default:() => {
  			return {
  				spMsg:'商品信息',
  				sppj:'商品评价'
  			}
  		}
  	},
	desc:{
		type: Object,
		default: () => {
			return {
				all: '全部',
				positive: '推荐',
				nagative: '吐槽'
			};
		}
	}
  },
  data () {
    return {
		favActive:false,
		onlyContent:false,
		selectType: ALL,
		foodShow:false
    }
  },
  methods:{
	show(){
		this.foodShow=true;
		this.selectType=ALL;
		this.$nextTick(() => {
			if(!this.scroll){
				this.scroll = new iscroll(this.$refs.food,{
					click: true
				});
			}
		});
	},
	onlyContentChange(){
		this.onlyContent=!this.onlyContent;
		this.$nextTick(() => {
			this.scroll.refresh();
		});
	},
	typeChange(type){
		this.selectType = type;
		this.$nextTick(() => {
			this.scroll.refresh();
		});
	},
	back(){
		this.foodShow = false;
	},
	needShow(type,text){
		if(this.onlyContent && !text){
			return false;
		}else{
			if(this.selectType === ALL){
				return true;
			}else{
				return this.selectType === type;
			}
		}
	}
  },
  filters:{
	  format(time){
		  return formatDate(new Date(time),'yyyy-MM-dd hh:mm:ss');
	  }
  },
  components:{
  	split,
  	ratingSelect
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.food{
		touch-action: none;
		position: fixed;
		top: 0;
		left: 0;
		bottom: 48px;
		z-index: 30;
		width: 100%;
		background: #fff;
		/* transition: all 0.5s; */
	}
	.food .food-content .image_wrapper{
		position: relative;
		width: 100%;
		height: 0;
		padding-top: 100%;
	}
	.food .food-content .image_wrapper .img{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}
	.food .food-content .image_wrapper .back{
		position: absolute;
		top: 0;
		left: 0;
		color: #fff;
		padding: 8px;
		background: #00a0dc;
		border-radius: 50%;
		margin: 10px 0 0 10px;
	}
	.food .food-content .content{
		position: relative;
		padding: 19px;
	}
	.food .food-content .content .title{
		font-size: 14px;
		margin-bottom: 8px;
		font-weight: 700;
		color: #07111b;
		line-height: 14px;
	}
	.food .food-content .content .detail{
		font-size: 10px;
		color: #93999f;
		line-height: 10px;
		font-size: 0;
		margin-bottom: 18px;
	}
	.food .food-content .content .detail .sell-count{
		font-size: 10px;
		margin-right: 10px;
	}
	.food .food-content .content .detail .rating{
		font-size: 10px;
	}
	.food .food-content .content .price{
		line-height: 24px;
		font-size: 10px;
		color: #f01414;
		font-weight: 700;
	}
	.food .food-content .content .price .now{
		font-size: 14px;
		margin-right: 6px;
	}
	.food .food-content .content .price .old{
		text-decoration: line-through;
		color: #93999f; 
		font-size: 12px;
	}
	.food .food-content .content .buy{
		position: absolute;
		display: inline-block;
		right: 18px;
		bottom: 20px;
		font-size: 10px;
		background: #00a0dc;
		color: #fff;
		font-weight: 400;
		line-height: 24px;
		border-radius: 10px;
		padding: 0 10px;
	}
	.food .food-content .info{
		padding: 18px;
		font-size: 0;
	}
	.food .food-content .info .title{
		font-size: 14px;
		color: #07111b;
		margin-bottom: 6px;
		line-height: 14px;
	}
	.food .food-content .info .text{
		font-size: 12px;
		color: #4d555d;
		line-height: 24px;
		padding: 0 2px;
	}
	.food .food-content .rating{
		padding-top: 18px;
	}
	.food .food-content .rating .title{
		font-size: 14px;
		line-height: 14px;
		color: #07111b;
		margin-left: 18px;
	}
	.food .food-content .rating .rating-wrapper{
		padding: 0 18px;
	}
	.food .food-content .rating .rating-item{
		position: relative;
		padding: 18px 0;
	}
	.food .food-content .rating .rating-item .user{
		position: absolute;
		display: inline-block;
		top: 18px;
		right: 18px;
		font-size: 0;
	}
	.food .food-content .rating .rating-item .user .name{
		font-size: 10px;
		color: #939d9f;
		margin-right: 6px;
		line-height: 12px;
		vertical-align: top;
	}
	.food .food-content .rating .rating-item .user img{
		display: inline-block;
		border-radius: 50%;
	}
	.food .food-content .rating .rating-item .time{
		font-size: 10px;
		color: #939d9f;
		line-height: 12px;
		margin-bottom: 6px;
	}
	.food .food-content .rating .rating-item .text{
		font-size: 12px;
		color: #07111b;
		line-height: 17px;
	}
	.border-1px{
		border-bottom: 1px solid rgba(7, 17, 27, 0.1);
		content: ' ';
	}
</style> 

