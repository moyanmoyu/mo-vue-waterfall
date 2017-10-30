<template>
	<div class="item">
		<div class="item-img">
			<img src="./../assets/logo.png" />
		</div>
		<p class="item-content">{{item.content}}</p>
	</div>
</template>
<script>
	export default {
		props: {
			item:{
				type: Object
			}
		}
	}
</script>
<style>
	.item{
		position: absolute;
		left: 0;
		top: 10px;
		width: 200px;
		float: left;
		transition-duration: 1s;
		/* overflow: hidden; */
		box-shadow: 1px 1px 4px rgba(0,0,0,.1);
		background-color: rgb(255,255,255);
		/*transform: translate(-200px,0);*/
	}
	.item img{
		max-width: 100%;
		height: 200px;
	}
	.item-content{
		line-height: 30px;
		word-wrap: break-word;
	}
</style>