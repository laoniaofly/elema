<template>
	<div class="seller" ref="seller">
		<div class="seller-content">
			<div class="overview">
				<h1 class="title">{{ seller.name }}</h1>
				<div class="desc">
					<star :size="36" :score="seller.score"></star>
					<span class="text">({{ seller.ratingCount }})</span>
					<span class="text">月销{{ seller.sellCount }}单</span>
				</div>
				<ul class="remark">
					<li class="block">
						<h2>{{ remark.qsPrice }}</h2>
						<div class="content"><span class="stress">{{ seller.minPrice }}</span>元</div>
					</li>
					<li class="block">
						<h2>{{ remark.jspsPrice }}</h2>
						<div class="content"><span class="stress">{{ seller.deliveryPrice }}</span>元</div>
					</li>
					<li class="block">
						<h2>{{ remark.psTime }}</h2>
						<div class="content"><span class="stress">{{ seller.deliveryTime }}</span>分钟</div>
					</li>
				</ul>
				<div class="favorite">
					<span class="icon_favorite" :class="{active:favActive}" @click.stop.prevent="toggleActive">♥</span>
					<span class="text">{{ favActive?'已收藏':'收藏' }}</span>
				</div>
			</div>
			<split></split>
			<div class="bulletin">
				<h1 class="title">{{ sellerMsg.sjgg }}</h1>
				<div class="content-wrapper">
					<p class="content">{{ seller.bulletin }}</p>
				</div>
				<ul class="supports">
					<li class="supports-item border-1px" v-for="(supprt,index) in seller.supports">
						<span class="icon" :class="classMap[seller.supports[index].type]"></span>
						<span class="text">{{ seller.supports[index].description }}</span>
					</li>
				</ul>
			</div>
			<split></split>
			<div class="pics">
				<h1 class="title">{{ sellerMsg.sjsj }}</h1>
				<div class="pic-wrapper" ref="picwrapper">
					<ul class="pic-list" ref="piclist">
						<li class="pic-item" v-for="(pic,index) in seller.pics">
							<img :src="seller.pics[index]" width="120" height="90" alt="" />
						</li>
					</ul>
				</div>
			</div>
			<split></split>
			<div class="info">
				<h1 class="title">{{ sellerMsg.sjxx }}</h1>
				<ul>
					<li class="info-item border-1px" v-for="(info,index) in seller.infos">{{ seller.infos[index] }}</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
import split from './split'
import star from './star'
import iscroll from '../../node_modules/iscroll/build/iscroll-probe'

export default {
  props:{
  	seller:{
  		type:Object
  	}
  },
  data () {
    return {
		favActive:false,
		sellerMsg:{sjgg:'商家公告',sjsj:'商家实景',sjxx:'商家信息'},
		remark:{qsPrice:'起送价',jspsPrice:'商家配送',psTime:'平均配送时间'},
		classMap:['decrease','discount','special','invoice','guarantee']
    }
  },
  methods:{
	_initScroll(){
		if(!this.sellerScroll){
			this.sellerScroll = new iscroll(this.$refs.seller,{
				click:true
			});
		}else{
			this.sellerScroll.refresh();
		}
	},
	_initLScroll(){
		if(this.seller.pics){
			let picWidth = 120,
				margin = 6,
				width = (picWidth+margin)*this.seller.pics.length - margin;
			this.$refs.piclist.style.width = width + "px";
			if(!this.picwrapper){
				this.picwrapper = new iscroll(this.$refs.picwrapper,{
					scrollX:true,
					eventPassthrough: 'vertical'
				});
			}else{
				this.picwrapper.refresh();
			}
		}
	},
	toggleActive(){
		this.favActive = !this.favActive;
		this.$nextTick(()=>{
			this.sellerScroll.refresh();
		});
	}
  },
  mounted(){
  	this._initScroll();
  	this._initLScroll();
  },
  watch:{
  	seller(){
  		this.$nextTick(() => {
  			this._initScroll();
  			this._initLScroll();
  		})
  	}
  },
  components:{
  	split,
  	star
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.seller{
		touch-action: none;
		position: absolute;
		top: 174px;
		bottom: 48px;
		overflow: hidden;
		width: 100%;
	}
	.seller .seller-content .overview{
		position: relative;
		padding: 18px;
	}
	.seller .seller-content .overview .title{
		font-size: 14px;
		margin-bottom: 8px;
		line-height: 14px;
		color: #07111b;
	}
	.seller .seller-content .overview .desc{
		padding-bottom: 18px;
		font-size: 0;
		position: relative;
	}
	.seller .seller-content .overview .desc .star{
		margin-right: 8px;
	}
	.seller .seller-content .overview .text{
		display: inline-block;
		font-size: 10px;
		color: #4d555d;
		margin-right: 8px;
		vertical-align: top;
		line-height: 15px;
	}
	.seller .seller-content .overview .remark{
		padding-top: 18px;
		display: flex;
		border-top: 1px solid rgba(7,17,27,0.1);
	}
	.seller .seller-content .overview .remark .block{
		text-align: center;
		border-right: 1px solid rgba(7,17,27,0.1);
		flex: 1;
	}
	.seller .seller-content .overview .remark .block:last-child{
		border: none;
	}
	.seller .seller-content .overview .remark .block h2{
		margin-bottom: 4px;
		font-size: 10px;
		color: #93999f;
		line-height: 10px;
	}
	.seller .seller-content .overview .remark .block .content{
		font-size: 10px;
		color: #07111b;
	}
	.seller .seller-content .overview .remark .block .stress{
		font-size: 24px;
	}
	.seller .seller-content .overview .favorite{
		position: absolute;
		top: 40px;
		right: 20px;
		font-size: 10px;
		text-align: center;
	}
	.seller .seller-content .overview .icon_favorite{
		display: block;
		font-size: 36px;
		color: #d4d6d9;
		margin-top: -30px;
	}
	.seller .seller-content .overview .icon_favorite.active{
		color: #f01414;
	}
	.seller .seller-content .overview .favorite .text{
		margin: 0;
	}
	.seller .seller-content .bulletin{
		padding: 18px 18px 0 18px;
		font-size: 0;
	}
	.seller .seller-content .bulletin .title{
		font-size: 14px;
		line-height: 14px;
		margin-bottom: 8px;
		color: #07111b;
	}
	.seller .seller-content .bulletin .content-wrapper{
		padding: 0 12px 16px 12px;
		display: flex;
	}
	.seller .seller-content .bulletin .content-wrapper .content{
		font-size: 12px;
		color: #f01414;
		line-height: 24px;
	}
	.seller .seller-content .bulletin .supports .supports-item,
	.seller .seller-content .info .info-item{
		padding: 16px 12px;
		font-size: 12px;
	}
	.border-1px{
		border-top: 1px solid rgba(7,17,27,0.1);
		content: ' ';
	}
	.seller .seller-content .bulletin .supports .supports-item .icon{
		display: inline-block;
		width: 16px;
		height: 16px;
		background-size: 16px 16px;
		margin-right: 4px;
		background-repeat: no-repeat;
	}
	.seller .seller-content .bulletin .supports .supports-item .icon.decrease{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MjIzOTZBNDY1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MjIzOTZBNDc1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoyMjM5NkE0NDVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoyMjM5NkE0NTVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PtgZ4joAAAKtSURBVHjazJevU1tBEMcvjzSlhTaIoMGg+Q/AMFNVTNEYmKEKgwaDxqBqYtAgoIqZGNAYNAY0JmGAFkJJ73PMppvj7v2YafO6M5e83NvbH9/97h5U2o1Gwxjzza5Pdo2b4citXcd2fa3aj6Zdi2a4QqJf7KpVLAIPPJhy5DEp0TlSS/62xffNphnd3DS15WX3+81ienUpQS/0ojo/b36dn5teu/2iODFhKvW66XU6/b2QfDg7M8nUlHt+Ojnp27lbWgqeCyJA9GP7++bjxYV5u77u9kZmZ51x9urX17nQwOnz1ZU7CyrBREObHBDhIDD+3N4e0MkThNYBCVD0UQgG8GNjw8HIIQmoOjc3oBMrA05COs+Xl8EzUQ7gdLzV6kOJUBaRzuRkJgdiOpkIIBCne3RkHvf2+mTSItzQvAlmGIA9FwJa4AFkerezU6gl71dWXFsSABwimdwIiEBAsgURLT4ppeboSgmS6elXvMjVhgPZb229zEwvepzBE8hFiQiU71g3gWAhDgj0ZMNh3wDGcaonHQTU9dYB+MFlIgBsMk5DtdOZSXlwrkslpYhlnxoAhBMGP+zuRg2QmQTImI7pFAqAlhNon05PCzE/FATtXCgAPbdD8Kf1tf8O+NMQCJJQaicj1N/TWbKv28xvVxKgnOjJRM1EQMM+dnDwitHaiS6Xj4DwB+cyE3IF0D08HMiQO0AjoN9TX01SmRvSSQSHcx+ZzFHMvR+aYGR1MzPjWpTs5a6QzpHW1frYQY9bNncbxiKWEYxBZr04x7E412WQJGL2krQBIxBLG2Ek1BU4kYuKcyDkMz92H0RL4E9BWpPn2FQTBG4XFv4Q2HKHMoEI+6Gzua7jfymJKVn+iwDuSvTv/jVrlRjAMXfBKh1m12f+AhuS465d3+1a+y3AAKPKcE07d0OiAAAAAElFTkSuQmCC);
	}
	.seller .seller-content .bulletin .supports .supports-item .icon.discount{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MjAyNzlCNUI1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MjAyNzlCNUM1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoxRUVCMkU2NDVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoyMDI3OUI1QTVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PjMTN9QAAAJ8SURBVHjaxFfPaxNBFH6JaVpQGlNEUTDSqkUvIlS96akhHhovmv4FxQr9A9o/oQWvBRW9eWq99VSak15ECUjx4A8MNIKiYNoUA602tPMNvGEymd2dZJfsg7dZdib7vvfe983MJujx21NE9ER4QfgJ6o/9Fb4u/FFKXF4Iv0f9NSR6X3g6KS53KT4rAEA6RgCyAp728Nppqs9N0MaDK7RSvEzZoZQaK42P0Fhm0PftT/Oj9G3muu+cVBBEBJ28kJH3zzZ/U3mrIe8X7+QUgGpjny4+/6Dmz988K8EzYIDg8a4BuFh28Bgt3j4vgU6cOd4xDqCoYv7Vp3AAEAhBuAp6leZvneuYv713IKuz+qUuq+dcAS6t2WPwADa99rUj0NL7n7T6+Y96hsAuZgWwUbrqSzAAQVAFYL9FS+9+9NQ+K4CF1zUaOzkk+wm2syEIgqEFpiq8DIlgXuVX0x0AesYy1AGUa7sd/TfbZnID5MMv2sbvjVwFCB6kd1QMKjAT6BoA5AbCmSTkEiNbXYo8huxt1esKAMrJQdoACF6wxiFTngdDcJv+2ZJ+ZdX73ya5HhnvREJksDJ1ycpwzkaXYFhL2oJ4yWvhzfdIg1sB6IQKYr7+n8gA8DoAxiJjF827LrvOAEAyv17z9qwAa3tAJACCTAcAkLYVLhQALMEos5mpApAbbiNmpDKEYW/HccoLHKsEZPXa58ORUPTU1v/qzp46eGDcPBdEBgBlNUvL6zhORQh+4+XHUOwP3AtALC41MmeijSxX5HMvhWAu2gJwuA9aUxLi0+wwxu+C3mQYNYBmjPH/AUA5RgDrYNmM8JbwovCBPgX+L3xN+OyRAAMApt4SIIixgnYAAAAASUVORK5CYII=);
	}
	.seller .seller-content .bulletin .supports .supports-item .icon.special{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MUVFQjJFNUU1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MUVFQjJFNUY1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoxRUVCMkU1QzVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoxRUVCMkU1RDVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PsPuJEUAAALHSURBVHjaxFc7TFRBFL27cUk0aPCTiImJUmBhoRAaCzYKjSEEPwW1LjHRRo3tNkIDpUEbKxbrLVyiQjDE31rYGHYbCyFhjSYshQZxkSgYmDN6J/Pem3kMC+47yc2+nd89d+6ZO+/F6Gn7ISJ6KOy8sHqqDSrCJoXdiAkCY+LhAkWDJyDwSzzURUTgdzxC50BdfLMRd5tTtN6dp7nOLL08c9845tzBVjkG/Y/bBunq0S5nBrtMjVigtFKmwtKMaju+u1FaGEAEaEjU0+iXCdX26uv01ghcEQR4sf6PI6HOgJZ9zZ4+EEA/1kEwqeKgIuREwAX3Tt4MONYJ6enKnE7LXcCuOhHg6ExbB02MLbylOx8e0NkDLX/Ts+eIJ+9wNPp5XP0v/pg1OgdwDNf9jRBUGBZXK9Tx7pbSCAjrEYM4+qsWIQMOGhJ7PeLjXSmtzDs5wFysoQs6lICe11RxiC4ebqf+E32qDZEhYn2cTYT4zZxKq3kmEgECmMR5xAQQ2IoATSIEppMj1PSiN6CFAAEWVq78xupgeC5Lxyw1QRckK7/0c94qxACBT2IQRAYnJuBIwYEpGhYkE8Az6sjATMYaTKAUo2Dsf96lFueU6FUSBCEsF1xqTMry7F/HegyhWq6EyKV/Ip8MbKsJGG/SB+ZBiCAfmoLFtYpH9X5gEUSkl2IXFJZmA86NKcAgW93m/svv02oM6nzsWVKZvwBBA2jHOCcNAI/+LQ4V224y3gGIEuW5WhgJwGlrvk9GYyKAXRjQbkmkDER2jACLJgxIgX4MbaKsmoALsAvYDeT39beCTAsXsm29Ebkit5CXKbrd1LvzKXABouc02O77/0qAgZcTlGb8+oHUbCsFuBty5bwU5fe15U2EOe65PYdL2dAXUusbUS0Rp4gBAssR+pefZlMREpiECK8J+yOsR1iiRo5X8WUs7PqGAAMAbV9KOzs8mYkAAAAASUVORK5CYII=);
	}
	.seller .seller-content .bulletin .supports .supports-item .icon.invoice{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MjAyNzlCNjM1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MjAyNzlCNjQ1RTQ1MTFFNjk5QTJBOUEwOEVGNzIyMDEiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoyMDI3OUI2MTVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoyMDI3OUI2MjVFNDUxMUU2OTlBMkE5QTA4RUY3MjIwMSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PlhCbkEAAAIWSURBVHjaxFe9TsMwEE6qUAYYOrB0aphZwhPQTjDCwEyLGBjpxIJEK9hbmFig4QkqRiSkhidoJlbCE2AJurCUM7pIJ2MntlXMSV9buY7vu/P9xb9evljzPO8GsA1Y9dzIJ+ARcFyBj1vAC6AO8B2hjjrvAvjYAewDvjx3wj1wCfjgHqg6Vp4L11mtOFB0DpgAarI/A8VD8z8gwkls6hIYAiLJek1YT/C7SdZSAJM8e2/igS5xG8NDu6hoQva1JB7rIjH+7BTQIUS1CeQSEQs5kVByv6IcALYAu7ifE+4B+jYEqPQ019oF+36RMMkCn7icrvnCWgvXEiEupB6oOMp5ZhsDZak5V6SbtpgQSAytjlTFR5dAhkozxLNFBWxiWg5tCDwAxgu4/wEGYWJKILFwu0xS20LEJGlnIyPAK2APyZQS4IHz/kfNaF1MyUBheUzKbohgggVilNPGlAeu2IyY7hV0yO8p8YyHrmRoUVOogGOyN1FVP5NKOBLab1ZU1ZB4igR6ePeRLYG20FhiDYvywGXk+rgHT0yzoI3WU8tizUkpJ0HHsAEZdEo9EBLlGY5ReVAOJcElazZi91NWw0BRgrnFDcAVOTzDg/ro1lAY4WRjXQOjPzW9grjExX08/A0PTwtGu4V1Q12CRuJqICkkMAOs/IPunzcyTuAJcApYcqic6zrjb8icwBFgAz0xd4QZ6jz8FmAAE/eVb2xSKbkAAAAASUVORK5CYII=);
	}
	.seller .seller-content .bulletin .supports .supports-item .icon.guarantee{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6NDg3RDgyNTc1RDlBMTFFNjk5QTJBOUEwOEVGNzIyMDEiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6NDg3RDgyNTg1RDlBMTFFNjk5QTJBOUEwOEVGNzIyMDEiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDo0ODdEODI1NTVEOUExMUU2OTlBMkE5QTA4RUY3MjIwMSIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDo0ODdEODI1NjVEOUExMUU2OTlBMkE5QTA4RUY3MjIwMSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PjsZE8gAAAIBSURBVHjaxFe9TgJBEF4uSKMmV9hQCbXN+QQelS2+gRgLO73KxgR8Aii1UPEJpDUxEXuLtbGVRyBRCmzOWTOXTCb7cwvHMcnHLZfZnW9n52evIt5vd4QQN4BDwJYoR34Az4CzAH7uAJ+AOqBSEupo874CHpjDYBvwK8qVGuA7wEHZxgXarAU5FGPAK+AC0CDvYsc8pfsEiGxK1RwEDojBPiDBZyYTwFAzTxEOcV5i0MlFoM3+jzU77VnmKxIPOB76EmgwF6rdSqZj8gAlNVrUA3z31xqdieE9JSBNBlxBeE7GU9xJoRI4or/BdjEtmoDtCLo514gwTQsl0M6R5zTK4yIJhCzPXTLEQKRBp+r9F75XePMhELGz10mLxYTuuJpkvciHgCo0++gJfrbHgF1SIWnAmuInq4jaQqS6YYou00nKiElccFFpsUqaVj0XeGSpaGtKA6b7oSnjwpeAJFUtxCOx1ZGWq3YES7iz6wjWrD6EqyAQs1iYGjpmhOkYF0kgu2jQOjCwNK0sm/o6b/gSCNE4TauOIZXHGq8t7QF6xRoYjGfSIUcjTQHpSyDBRY5wbJMJkpC2bFgkDZsebXnkukO4CPRII5GGiBeok9huPiZxleJVSxqINYsiMANsrsH2/xeZIvACuARslGhc2bpSX8iKwClgDz2RloQZ2jz5E2AAhkCLabtFR1IAAAAASUVORK5CYII=);
	}
	.seller .seller-content .bulletin .supports .supports-item .text{
		color: #07111b;
		line-height: 16px;
		vertical-align: top;
	}
	.seller .seller-content .pics,
	.seller .seller-content .info{
		padding: 18px;
	}
	.seller .seller-content .pic-wrapper{
		width: 100%;
		overflow: hidden;
		white-space: nowrap;
	}
	.seller .seller-content .pics .title,
	.seller .seller-content .info .title{
		font-size: 14px;
		color: #07111b;
		padding-bottom: 12px;
		line-height: 14px;
	}
	.seller .pics .pic-wrapper .pic-list{
		font-size: 0;
	}
	.seller .seller-content .pics .pic-list .pic-item{
		display: inline-block;
		margin-right: 6px;
		width: 120px;
		height: 90px;
	}
	.seller .seller-content .info .info-item{
		color: #07111b;
	}
</style>
