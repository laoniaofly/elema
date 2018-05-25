<template>
  <div class="header">
		<div class="content-wrapper">
				<div class="avatar">
					<img width="64" height="64" :src="headerData.imgPath">
				</div>
			  <div class="content">
			  	<div class="title">
			  		<span class="brand"></span>
			  		<span class="name">{{ headerData.name }}</span>
			  	</div>
			  	<div class="description">{{ headerData.sendWay }}</div>
			  	<div class="support">
			  		<span class="icon decrease"></span>
			  		<span class="text">{{ headerData.action }}</span>
			  	</div>
			  </div>
			  <div class="support-count" @click='showDetail'>
		  		<span class="count">5个<span class="icon-keyboard_arrow_right">></span></span> 
		  		
		  	</div>
		</div>
  	<div class="bulletin-wrapper" @click='showDetail'>
  		<span class="bulletin-title"></span>
  		<span class="bullentin-text">{{ headerData.describe }}<span class="icon-keyboard_arrow_right next">></span></span>
  	</div>
  	<div class="background">
  		<img :src='headerData.imgPath' width="100%" height="100%"/>
  	</div>
  	<div class="detail" v-if='headerData.isDetailShow' @click='hideDetail'>
  		<div class="detail-wrapper clearfix">
  			<div class="detail-content">
  				<h1 class="name">{{ headerData.name }}</h1>
  				<div class="star-wrapper">
  					<div class="star star_48">
  						<span class="star-item on"></span>
  						<span class="star-item on"></span>
  						<span class="star-item on"></span>
  						<span class="star-item on"></span>
  						<span class="star-item off"></span>
  					</div>
  				</div>
  				<div class="title">
  					<div class="line"></div>
  					<div class="text">优惠信息</div>
  					<div class="line"></div>
  				</div>
  				<ul class="supports">
  					<li class="supports-item">
  						<span class="icon decrease"></span> 
  						<span class="text">在线支付满28减5</span>
  					</li>
  					<li class="supports-item">
  						<span class="icon discount"></span> 
  						<span class="text">VC无限橙果汁全场8折</span>
  					</li>
  					<li class="supports-item">
  						<span class="icon special"></span> 
  						<span class="text">单人精彩套餐</span>
  					</li>
  					<li class="supports-item">
  						<span class="icon invoice"></span> 
  						<span class="text">该商家支持发票,请下单写好发票抬头</span>
  					</li>
  					<li class="supports-item">
  						<span class="icon guarantee"></span> 
  						<span class="text">已加入“外卖保”计划,食品安全保障</span>
  					</li>
  				</ul>
  			</div>
  		</div>
  	</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      headerData:{
      	imgPath:'http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg',
      	name:'粥品香坊（回龙观）',
      	sendWay:'蜂鸟专送/38分钟到达',
      	action:'在线支付满28减5',
      	describe:'粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。',
      	isDetailShow:false
      }
    }
  },
  methods:{
  	showDetail(){
  		this.headerData.isDetailShow = true;
  	},
  	hideDetail(){
  		this.headerData.isDetailShow = false;
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.header{
		position: relative;
		overflow: hidden;
		color: #fff;
		background-color: rgba(7,17,27,0.5);
	}
	.header .content-wrapper{
		position: relative;
		padding: 24px 12px 18px 24px;
		font-size: 0;
	}
	.header .content-wrapper .avatar{
		display: inline-block;
		vertical-align: top;
		border-radius: 2px;
	}
	.header .content-wrapper .content{
		display: inline-block;
		margin-left: 16px;
	}
	.header .content-wrapper .content .title{
		margin: 2px 0 8px 0;
	}	
	.header .content-wrapper .content .title .brand{
		display: inline-block;
		width: 30px;
		height: 18px;
		vertical-align: top;
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADwAAAAkCAYAAADVeVmEAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6NjhCMERGODc0RDYwMTFFNkJGNzlFOUVCREZEMzI2ODciIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6NjhCMERGODg0RDYwMTFFNkJGNzlFOUVCREZEMzI2ODciPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDo2OEIwREY4NTRENjAxMUU2QkY3OUU5RUJERkQzMjY4NyIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDo2OEIwREY4NjRENjAxMUU2QkY3OUU5RUJERkQzMjY4NyIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PpkNE6kAAAOnSURBVHja7Fm/M2NRFL75wSaxsxoKBX8BnYqKjoaSSmFnVHTMFootaOiomNlCp6ShVNHp6FTMrh2aZdaSZCN7v+OdzMl138t9eTEbSc7MneTFyb33O/ec73w3Yr+6usaUUt/06FGNbdd6zMY04B9NALYEOt5EYGE9cdVk1gLc6Jb4ksl8dXH8MDenkqOjKjkwoGKpFH1WvL/3j2Rvr+rY3yffwump22b6+1Vme5u+m+jrU4Wzs9f7WFxU6dVVlRgcJB+VzarizY0zYLB00cWxY29PJYeHS89/j49pBAUo1tlJ7/MHB+pxYUEV7+5ebT61tETAaL7DQ1qH53+YnCSf4tWVesa4vFQfj45K8+J7j/Pz9Iq9Be2HLVltamABGYAgaxsfp9c/MzO+J4tgALBpCAgbgJlBhGV2dmiN7NaWelpefhvAud1dldcjKCOkZdfXo9efDowMIgdSZhV8EFgzmyIDRnq5pJA8naiW8wLcPjVVVlbt09NU97Qvnfp+YN8dS+eNrAJYZA6CL33eJKXjmiFda7gaQ62mVlbKucA7WckjvBdn7ql2Q0irdmMDUetTAsSzrFmZytUQZ/Qa9tpEEIuHPdGEx8B+xgzMgWHixLMZnJoAZpB4xUJBpCX7qYtx3zWt8/bWl/iYOINIKhRgpFBybOxFGOgeiT7Hp0GCQC/Em0CU8TmdulZgcvOYB/6urclPRJg1DXaGr+vpVgQc01Qv+50Eh0XQ95BmCASeZRqzb2JoqCQe4GNTXCZRIUA2EWECQyvidvQmNWyKCQYft0TY5ovAJbQWf5iYoLIwT/XTxUW5dvcCyKVEde6tJVtSenOTfBHISukdCvDT2loplWRkC3rxuMGg7GsyKTZqgqWLiFce0hfy8ffICAFNb2yU/Y3nxXzQ07Y5IwPmGsRCDBgLgi3NHinrtQyEjzAAWNS9JCnMwSkuNTT6rkxvgIUP5qik6OpGadlICqAAFANAUNM5fX006x7pj7TGTaqSNkiqOrY2IW5IiBgsbfscGZHXHaXml4daW+HkxFpC1iujEBp88rI3BxFX/QC21B7dkS2pLgH5+dS0Lbk0evYNEvZMZgAbRi1FsVCAw+hjF19m3pyn4OruV8u77m4aLinEvtyPrZcF76edvKVO/8sJg0iwYZNQQBLcKjgV+TJh+j6fn7+A1vra7JOYx1RHLEyCbmJyrbCl4PyrZaNY6z8PLcAtwO8f8HUT4f0JwJ/xpgnAftdj9p8AAwCeZRLH3XUY/AAAAABJRU5ErkJggg==);
		background-size: 30px 18px;
		background-repeat: no-repeat;
	}
	.header .content-wrapper .content .title .name{
		margin-left: 6px;
		font-size: 16px;
		font-weight: bold;
		line-height: 18px;
	}
	.header .content-wrapper .content .description{
		margin-bottom: 10px;
		line-height: 12px;
		font-size: 12px;
		font-weight: normal;
	}
	.header .content-wrapper .content .support{
		margin: 10px 0 2px 0;
		font-size: 10px;
	}
	.header .content-wrapper .content .support .icon{
		display: inline-block;
		width: 12px;
		height: 12px;
		margin-right: 4px;
		vertical-align: middle;
		background-size: 12px 12px;
		background-repeat: no-repeat;
	}
	.header .content-wrapper .content .support .icon.decrease{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MUE1QTdFNjU0REI0MTFFNkJGNzlFOUVCREZEMzI2ODciIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MUE1QTdFNjY0REI0MTFFNkJGNzlFOUVCREZEMzI2ODciPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoyOTQ0OEQwRTREOEYxMUU2QkY3OUU5RUJERkQzMjY4NyIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoxQTVBN0U2NDREQjQxMUU2QkY3OUU5RUJERkQzMjY4NyIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PoFQatoAAAN2SURBVHjatFbNS1RRFP/d+94MmqSW5UeiC8EvUCpFxYULRQtx0dK97lr0h7gM7B9wEYESim4sqEhTMINE/EAjm/xoEmWmdNT33r23c+5k6DjaRg9c5+o77/zO+Z3fOaMwxjwE8JROAS7XonSeCAKI0KUEV2PrDJCgS+YVARy49MM7F8AYQIj0ryoF/9UrCnEAWVkJs7cHt74ecJyTXp5MfS94/x7e8+f2BQ7uDw/DGxiA3tw87UiB9OIivBcvYL5/RzA6Cp/u0PqUm5uaVTA9DTUxAb2yArezE+rzZwQfP0LNz0Pm5yer+mt6ZweysBDB3BzM79/w372D294OwX5pAaRE6NEjmK9foRYW4Ny7B5GdDXnrFmRBAURJiU0CoRCYOPPrlw0ssrIgm5shwmEgI+OCCogSp6ICTlMTQnfuwO3owGFfnw3ilJXBbW2lAgwMZW6CAHprC5qS4aRkcXHaVrGKYvSZc+qvvm+rUbOz8F+/ho5EIG/ehMjJgTk8tIe5FuRj4nGEurstkCwttUmcEEbcTQtLFPhjYwgmJ235oICsFLelxdKgPc8mEYyPQ8di0BsbCKhvzt27cNvaLqDouHnRqAUIPXgA/fMnDPXDVsTNpOAmkYBwXStRq6ZoNEkH0ZpqaQH8wUFIapbb0ABvaMgG5yoUydFQUEH0cBXi2jUIqpZlCgJ0iKJUOzMHrB41NQVZWwtBjeNsj4dOZGYi3NUF5/592w9ZVGR7wTPDEpbl5f8BoGD+yAhAmbGeUxVmP1iKXBFRI/LykoNFR5KERW7uxQDMt15ehiDFyONhITlaKm7csHd/ZgbqyxeI69cB8jPUbPZ3qGLeAmZ393wAcfs2ZHU1zI8fdkXo9XU7TIIGjRuoSZKKEjAEYI6OAD5MHVXCz4M3b5ISPq/JLEmnpgaa1BJ8+AD97Ruwv2/7wQOoP32CbGyEJD9Fe0i9fQvBy43XBCVkJ5orvUhFdiJ53EklanXVZuhSUK4i3NNj+8PPeJNqqk5S1Xp7GyAlMU0p2/QsANPkVFXBoaCaAHglOHV1yYccnJXGfaClGO7ttZQe9fdDUbUOJ5YCwLslZk6a7xuazuQ9kTDEtTlj+/smWFr696taWzPey5dGRSKpnjHeRXHCyb6ib7S4PG+aL8nCDLB9hQA74u+/Lc/o5F12cDqP/wgwAJG54Y1udZHlAAAAAElFTkSuQmCC);
	}
	.header .content-wrapper .content .support .text{
		line-height: 12px;
	}
	.header .content-wrapper .support-count{
		position: absolute;
		bottom: 14px;
		right: 12px;
		line-height: 12px;
		background-color: rgba(0,0,0,0.2);
		padding: 0 8px;
		height: 24px;
		text-align: center;
		border-radius: 14px;
	}
	.header .content-wrapper .support-count .count{
		vertical-align: top;
		font-size: 10px;
		line-height: 24px;
	}
	.header .content-wrapper .support-count .icon-keyboard_arrow_right{
		margin-left: 3px;
		font-size: 10px;
		line-height: 24px;
	}
	.icon-keyboard_arrow_right.next{
		position: absolute;
		top: 0;
		right: 8px;
		font-size: 10px;
	}
	.header .bulletin-wrapper{
		position: relative;
		height: 28px;
		padding: 0 22px 0 12px;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		background: rgba(7,17,27,0.1);
	}
	.header .bulletin-wrapper .bulletin-title{
		display: inline-block;
		width: 22px;
		height: 12px;
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAYCAYAAACBbx+6AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6Mjk0NDhEMDg0RDhGMTFFNkJGNzlFOUVCREZEMzI2ODciIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6Mjk0NDhEMDk0RDhGMTFFNkJGNzlFOUVCREZEMzI2ODciPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoyOTQ0OEQwNjREOEYxMUU2QkY3OUU5RUJERkQzMjY4NyIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoyOTQ0OEQwNzREOEYxMUU2QkY3OUU5RUJERkQzMjY4NyIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/Puq6d8sAAAM6SURBVHja1FdLTFNBFL0YdrZbS7cI7vjuqoZEI0EwGhKIGkxABbugKNJFaWJ1IZC0JLapKS6IqDVKRK2BxL+uiIaVIrqTzw7aurTt+vnOwAzT+qYfNeo7ycvrm++59557Z1qmaVorEU3pj53+b8T1p7dMJ7xhArKCNAhrZCLsIJOhvJhB8+8WqKG+hqwWy3ZsEkn2NNbXFo6jPg6wV9jY+9nLN7S49IV9V++upKb9jj9HGJt5r4yQxbKTmvY5yDfspuXVNXINDbP+2PTtLEOMMOD2snVAcLDfSYnkN3r+6i3ra6irKYlwQUlMRe+zdzqdEZ6CV3hbeGIy7/yPnz6LeYygHikVUuk0cwQcokLepMMCLceOi+9I0C8k8ODxLF2/sUn2kmeIjhxuNlwDBBD+UoBoRicjQkJFS+JhbG7bM3roZL2e7GynR0/mmPfGxkOsLZc0vMvJ9vacYmsAkAOXBKI16HJmzbNaLYZk8xIGkZnYrLAY2uXJAi1Dd/As9AkYkeZyAVk8HLLHsXYxiVtQw9AuNAogUWDxrbvTzDNIQoQaG7W1HBJzQDqsywRSAnxeN/mvXs4iWwjQb0fXGaWOy1WJwkMGQvAavCsnz4mO9k1j9HAur6yJDWZ0bXMjes4NFCQIb+892GaofSMd/5R08M5p53lGDhtDCgCs5oTldu4VbICIyOGH4SWdu1ulj+uYV6MsaDnYiCe05qOd2oj/mmi7eeee5jjQyp7uPpf2PZVi7R8Wl1gf8HVlVeu/6MldjrXxeRijwtMXr9k4jOfrG8GwrMmWwuPwLryHBJkIBYTl3Ou5SfXXy5o8cCwQyko+OUxnu7tYoiFBizliL+jz91RVGvbJpa6xrrb0ssbP/Pn3C8rDAd+oHPDy6HiQolUR5UYAyKpKmByFaoVReQmDbHjrJEOIcP6PBoIi8fAtVw1EAf2QzD+5rYEQlwLe/E4hg8uA98FLuNmppIGDBMar9vstwihduST58Qyi8nUTJOPJJPk87rw6RqhVksm9JP3S5QeyACm73WZcE6U6XGHbZXjNxCUpk8mwfhijuoqCMK9EMEw1zpR/keIm4psA4T78MAHZdVz8fggwAAhHLI5JzyRSAAAAAElFTkSuQmCC);
		background-size: 22px 12px;
		background-repeat: no-repeat;
		vertical-align: middle;
	}
	.header .bulletin-wrapper .bullentin-text{
		font-size: 10px;
		line-height: 28px;
		vertical-align: middle;
		padding-left: 0;
	}
	/*.icon-keyboard_arrow_right:before{
		content: '\E905';
		content: '<';
	}*/
	.header .background{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: -1;
		filter: blur(10px);
	}
	.header .detail{
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(7,17,27,0.8);
		overflow: auto;
		z-index: 100;
		transition: all 0.5s;
	}
	.header .detail .detail-wrapper{
		margin-top: 64px;
		padding-bottom: 64px;
	}
	/*.header .detail .detail-wrapper .detail-content{
		text-align: center;
	}*/
	.header .detail .detail-wrapper .detail-content .name{
		line-height: 16px;
		font-size: 14px;
		font-weight: 700;
		text-align: center;
	}
	.header .detail .detail-wrapper .detail-content .star-wrapper{
		margin-top: 18px;
		padding: 2px 0;
		text-align: center;
	}
	.star{
		font-size: 0;
	}
	.star.star_48 .star-item.on{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAmCAYAAAC29NkdAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6RTY5NUIxMDc2QjdFMTFFNkFFQjVFRkIyNzZERjNFOEQiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6RTY5NUIxMDg2QjdFMTFFNkFFQjVFRkIyNzZERjNFOEQiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDpFNjk1QjEwNTZCN0UxMUU2QUVCNUVGQjI3NkRGM0U4RCIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDpFNjk1QjEwNjZCN0UxMUU2QUVCNUVGQjI3NkRGM0U4RCIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/Pob91EYAAAJZSURBVHjazJg7SyNRGIYn8QpaiZcINm61LgveGjeJ2Ii47IIWCv4AdxRBK7VUUHALsREstFKw1EJFccuAbKdtGkFXLbykEBaN7oLH9wyvECTOJX5J5oOHmZzbPMmcOfOdBNSyIRkdPMZc9zCVbXWhIRujQHkSdAhJwTrQm3J+ITFoUFBwBBSQEalBpQRLwI+Uz4Ms843gAKhM+VzFMt8Ijrksy4vgF9CSplyXtflBcNTjL5tTwVrQZ1PfxzZ5ExwCRTb1us7Ml2AxBZ1imG1zLqhvX8hFu5DDNLCNwBvJQinXtRDXNE0Nj9Wk2aWgjitwBK7JDctuyCVIIHF4SCc4gWOUF32RKjfyE38pnuAXOdCCWmoLhA1/xW/QE6RtJ9j0kdym5WSqxMtDkgT9YMEHcguWi6mSr/NBnWiOgxOwKJyKuYkn681jqiWnZWaJiWcyh3JJ65qv5OzWwR3Qzicq23FlXctUO14X6kNmI/EsysWta5jqMNM3ySmXn1gW5GLW2KY6fe+r7hZ0gXVBuXWOeSv1Lv4H1gQFVzmmaLIQERSMZiObiQoKRqQFC7j3kIowxxQTbAJlgoJ6rEZJwYghH1FJQbfzL+5hYY/kUvAOTPK2NfL83qFPu5TgB4et4wZoAPPgP9HnH1lnt2WtlxB861Ycg27mkedp6s9Z95VtM5o6wQxur97YTIHP4JeL/vtsO82+nuahV8Fd8AnMgkcPT6xuO8O+e17moZNgBQf9ozcw4Dsz7kxD9/3Gsc6subsSqHiPoP6Hao6S24Jr4DYfrJ+g1a7hswADAP0Eerk/kTZKAAAAAElFTkSuQmCC);
	}
	.star.star_48 .star-item.off{
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACgAAAAmCAYAAAC29NkdAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMDY3IDc5LjE1Nzc0NywgMjAxNS8wMy8zMC0yMzo0MDo0MiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTUgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6NTRGNkRGNjg2QjgyMTFFNkFFQjVFRkIyNzZERjNFOEQiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6NTRGNkRGNjk2QjgyMTFFNkFFQjVFRkIyNzZERjNFOEQiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDoxRDVDQkIwRDZCODIxMUU2QUVCNUVGQjI3NkRGM0U4RCIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDoxRDVDQkIwRTZCODIxMUU2QUVCNUVGQjI3NkRGM0U4RCIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PlMPbBkAAAJCSURBVHjazJhLS8NAEMeTtmJVLIiPxoMi9aJUEfEievSLePLkt9GLXvTuRYSCot5UPPhAxYMWFV/UQw/F+kLr4z8wQghpdmOmJgN/NtlsZn+7m8xOYs7MLRiC1sllQfeG6alJz+sJQ9YGoG8/gCqTBGyCemzHzxJOY4KAWchkZaWcSgHGoT7beR/XRQawF0razpNcFxnAAc26UADTUJtLPdV1RAEw63Nm/xWwEcp4XM9wm9AA+xU+YtwmFEDdzvuD9BMEUHf5VI+Bp5lVkoU4x7JGLhtY9uNWH8/XK1TkkvTmOH6hEonDpxvgEErLAVBnhGMfjgE80BKfMRjFrFSIcAb3nWIWYjqLMW0OujKiY8SSw5K//b4kFWgdOo4AHDGsA67ilg/uQmVojNOm/zRKdHcAdqpKWKnBEzRRg4y7mtFsbQLuWjcOUsMVfpNqbdTHihucKlBT3FqGSjWEI9/LgCv+dScpM2ShBnAFhisH3ereOQzlBeHy7PNdai/+gs4FAc/Zp2iyYAkCavsKCzAtDWj6cao5WFMSsFU4aCfYpxigZcibFQZgyUdgt3SnWsIZ7aX70AmfD0IjCv9igClFan/JWdCTre4IuoBGPb5HyGcz71aBAKu9vY/QFnRX5ToBb0Bd0DgP1G0WA291zqWgD5s9aMkDzm633HaP7/W1zAmfgDfQtmrULkZgB7wH02x26wKqZrAeauHlWoNW/wDnzI5W2Rf5bJmdX6wPMoP0h+qQVRGMgZSc3kPDULvXo/IjwADcHoKDst/q9gAAAABJRU5ErkJggg==);
	}
	.star.star_48 .star-item{
		margin-right: 22px;
		width: 20px;
		height: 20px;
	}
	.star .star-item{
		display: inline-block;
		width: 20px;
		height: 20px;
		background-size: 20px 20px;
	}
	.header .detail .detail-wrapper .detail-content .title{
		display: flex;
		width: 80%;
		margin: 28px auto 24px auto;
	}
	.header .detail .detail-wrapper .detail-content .title .line{
		flex: 1;
		position: relative;
		top: -6px;
		border-bottom: 1px solid rgba(255,255,255,0.2);
	}
	.header .detail .detail-wrapper .detail-content .text{
		padding: 0 12px;
		font-size: 14px;
		font-weight: 700;
	}
	.header .detail .detail-wrapper .detail-content .supports{
		margin: 0 auto;
		width: 80%;
	}
</style>
