<template>
	<div class="container">
		<p v-if="loadingTip!==''" class="loading-tip">{{ loadingTip }}</p>
		<img :src="loadingImage" class="loading-image"/>
	</div>
</template>

<script>
import loadingImage from './loading.gif';
export default {
	props: {
		tip: {
			type: String,
			default() {
				return ''
			}
		}
	},
	data() {
		return {
			loadingImage: loadingImage,
			loadingTip: this.tip
		}
	},
	watch: {
		tip: function(newString) {
			this.loadingTip = newString;
		}
	}
}
</script>

<style scoped>
.container {
	align-items: center;
	color: #212121;
	display: flex;
	font-size: 14px;
	height: 40px;
	justify-content: center;
	width: 100%;
}
.loading-tip {
	margin-right: 10px;
}
.loading-image {
	height: 20px;
	width: 20px;
	display: inline-block;
}
</style>
