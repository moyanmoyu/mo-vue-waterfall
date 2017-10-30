<template>
	<div>
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
			items: {
				required: true
			}
		},
		data() {
			return {
				itemLength: 0,
				itemWidth: 0,
				rowHeight: []
			}
		},
		watch: {
			items: function (items) {
				let length = this._data.itemLength
				let newItems = items.slice(length)
				var self = this
				setTimeout(function () {
					self.addNewItems(newItems,length)
					self.setItemLength()
				},100)
			}
		},
		methods: {
			waterFall,
			setItemLength,
			setItemWidth,
			setRowHeight,
			moveItems,
			addNewItems,
			getChildren,
			listenResize
		},
		mounted: function () {
			this.waterFall()
			this.listenResize(this.autoResize)
		},
		beforeDestroy: function () {
			this.listenResize(false)
		}
	}

	function getChildren() {
		return this.$el.children
	}

	function listenResize(autoResize) {
		if (autoResize) {
			window.addEventListener('resize', this.waterFall, false)
		}else{
			window.removeEventListener('resize', this.waterFall, false)
		}
	}

	function waterFall() {

		this.setItemLength()
		this.setItemWidth()

	}

	function setItemLength() {
		this._data.itemLength = this._props.items.length
	}

	function setRowHeight(col) {
		this._data.rowHeight.length = col
		let rowHeight = this._data.rowHeight
		for(let i = 0; i < rowHeight.length; i++) {
			this._data.rowHeight[i] = 0
		}
	}

	function setItemWidth() {
		const contentWidth = this.$el.clientWidth
		const margin = this._props.margin
		const minWidth = this._props.minWidth
		const col = Math.floor((contentWidth - margin) / (minWidth + margin))

		this.setRowHeight(col)

		const width = (contentWidth- margin*(col+1))/col
		this._data.itemWidth = width

		let children = this.getChildren()
    let items = this._props.items

		for(let i = 0;i<children.length;i++){
    	children[i].style.width = width +'px'
    }

    this.moveItems(items,0)
	}

	function moveItems(items,index) {
		let children = this.getChildren()
		const width = this._data.itemWidth
		const margin = this._props.margin
		let rowHeight = this._data.rowHeight
		const length = this._props.items.length
		
		for (let i = index; i < children.length; i++) {
			console.log(children[i].clientHeight)
			const currentHeight = children[i].clientHeight
			const minHeight = Math.min.apply(null, rowHeight)
			const minIndex = rowHeight.indexOf(minHeight)
			const x = width * minIndex + margin * (minIndex + 1)
			const y = minHeight + margin
			children[i].style.transform = 'translate('+x+'px,'+y+'px)'
			rowHeight[minIndex] += currentHeight + margin
		}
		console.log(rowHeight)

		let maxHeight = Math.max.apply(null,rowHeight)
		this.$el.style.height = maxHeight + 2*margin + 'px'
	}

	function addNewItems(items,index) {
		let children = this.getChildren()
		let width = this._data.itemWidth
		for (let i = index; i < children.length; i++) {
			children[i].style.width = width +'px'
		}
		this.moveItems(items,index)
	}

</script>