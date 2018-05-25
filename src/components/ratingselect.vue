<template>
	<div class="ratingselect">
		<div class="rating-type border-1px">
			<span @click.stop.prevent='select(2)' class="block positive" :class='{active:selectType===2}'>{{ desc.all }} <span class="count">{{ ratings.length }}</span></span>
			<span @click.stop.prevent='select(0)' class="block positive" :class='{active:selectType===0}'>{{ desc.positive }} <span class="count">{{ positives.length }}</span></span>
			<span @click.stop.prevent='select(1)' class="block nagative" :class='{active:selectType===1}'>{{ desc.nagative }} <span class="count">{{ nagatives.length }}</span></span>
		</div>
		<div class="switch">
			<span class="icon-check_cicle" :class="{on:onlyContent===true}" @click.stop.prevent="toggleSwitch">√</span>	
			<span class="text">只看有内容的评价</span>
		</div>
	</div>
</template>

<script>

const ALL = 2;
const POSITIVE = 0;
const NAGATIVE = 1;
	
export default {
  name:'ratingselect',
  props:{
  	ratings:{
		type:Array,
		default:() => {
			return [];
		}  
  	},
  	selectType:{
  		type:Number,
  		default:() => {
  			return ALL
  		}
  	},
  	onlyContent:{
  		type:Boolean,
  		default:() => {
  			return false;
  		}
  	},
  	desc:{
  		type:Object,
  		default:() => {
  			return {
  				all:'全部',
  				positive:'满意',
  				nagative:'不满意'
  			}
  		}
  	}
  },
  data(){
  	return {
  	}
  },
  methods:{
	select(type){
		this.$emit('typeChange',type);
	},
	toggleSwitch(){
		this.$emit('onlyContentChange');
	}
  },
  computed:{
	positives(){
		return this.ratings.filter((item) => {
			return item.rateType === POSITIVE;
		});
	},
	nagatives(){
		return this.ratings.filter((item) => {
			return item.rateType == NAGATIVE;
		});
	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.ratingselect .rating-type{
		position: relative;
		padding: 18px 0;
		margin: 0 18px;
		font-size: 0;
	}
	.ratingselect .rating-type::after{
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		border-top: 1px solid rgba(7,17,27,0.1);
		content: ' ';
	}
	.ratingselect .rating-type .block{
		display: inline-block;
		padding: 8px 12px;
		font-size: 12px;
		line-height: 16px;
		margin-right: 8px;
		border-radius: 1px;
		color: #4d555d;
	}
	.ratingselect .rating-type .block .count{
		margin-left: 2px;
		font-size: 10px;
	}
	.ratingselect .rating-type .positive{
		background: rgba(0,160,220,0.2);
	}
	.ratingselect .rating-type .positive.active{
		background: #00a0dc;
	}
	.ratingselect .rating-type .nagative{
		background: rgba(77,85,93,0.2);
	}
	.ratingselect .rating-type .nagative.active{
		background: rgba(77,85,93,0.5);
	}
	.ratingselect .rating-type .positive.active,
	.ratingselect .rating-type .nagative.active{
		color: #fff;
	}
	.ratingselect .switch{
		padding: 12px 18px;
		font-size: 0;
		color: #93999f;
		border-bottom: 1px solid rgba(7,17,27,0.1);
	}
	.ratingselect .switch .icon-check_cicle{
		display: inline-block;
		margin-right: 6px;
		font-size: 18px;
		width: 18px;
		height: 18px;
		background-color: #ccc;
		text-align: center;
		border-radius: 9px;
		color: #fff;
		vertical-align: middle;
	}
	.ratingselect .switch .icon-check_cicle.on{
		background-color: #00c850;
	}
	.ratingselect .switch .text{
		font-size: 10px;
		line-height: 24px;
		vertical-align: middle;
	}
</style>
