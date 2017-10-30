<template>
	<div id="vue-waterfall">
		<slot></slot>
	</div>
</template>
<script>
	export default {
		props: {
			autoResize: {
				type: Boolean,
				default: true
			},
			margin: {
				type: Number,
				default: 12
			},
			minWidth: {
				required: true
			},
			maxWidth: {
				required: true
			},
			items: {
				required: true
			}
		},
		// data() {
		// 	return {
		// 		items: this.items
		// 	}
		// },
		watch: {
			items: function () {
				waterFall(this.$props)
			}
		},
		mounted: function () {
			// console.log(this.$props);
			waterFall(this.$props);
			let self = this;
			window.onresize = function () {
				waterFall(self.$props);
			}
		}
	}

	function $(id) {
		return document.getElementById(id)
	}

	function getChildren() {
		return $('vue-waterfall').children
	}

	function waterFall(obj) {
		let minWidth = obj.minWidth
		let maxWidth = obj.maxWidth
		let margin = obj.margin
		const contentWidth = $('vue-waterfall').clientWidth
		setItemWidth(contentWidth,minWidth,maxWidth,margin)
	}

	function setItemWidth(contentWidth,minWidth,maxWidth,margin) {
		const col1 = Math.floor((contentWidth + margin) / (minWidth + margin))
		const col2 = Math.floor((contentWidth + margin) / (maxWidth + margin))
		const col = Math.max(col1,col2)
		const width = (contentWidth- margin*(col+1))/col
		let children = getChildren()

		console.log(children)

		for(let i = 0;i<children.length;i++){
    	children[i].style.width = width +'px'
    }
    moveArticle(width,col,margin)
	}

	function moveArticle(width,col,margin) {
		let children = getChildren()
		let rowHeight = []
		rowHeight.length = col
		for(let i = 0; i < rowHeight.length; i++) {
			rowHeight[i] = 0
		}
		for (let i = 0; i < children.length; i++) {
			const currentHeight = children[i].clientHeight
			const minHeight = Math.min.apply(null, rowHeight)
			const minIndex = rowHeight.indexOf(minHeight)
			const x = width * minIndex + margin * (minIndex + 1)
			const y = minHeight + margin

			children[i].style.transform = 'translate('+x+'px,'+y+'px)'
			rowHeight[minIndex] += currentHeight + margin
		}
		let maxHeight = Math.max.apply(null,rowHeight)
		$('vue-waterfall').style.height = maxHeight + margin + 'px'
	}
</script>