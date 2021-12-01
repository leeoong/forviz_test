<template>
	<div>

		<div class="container">
			<div class="wrapper">
				<div class="images-container">
					<div
						v-for="(r, i) in this.Images" :key="i"
						class="image-wrapper"
					>
						<img class="masonry-img" :src="r.download_url" style="image-resolution: 72dpi;"/>
					</div>
				</div>
			</div>
		</div>

		<!-- <pre>{{ this.Images }}</pre> -->

	</div>
</template>

<style>

	html, body {
		margin: 0px 0px 0px 0px;
		padding: 0px 0px 0px 0px;
		width: 100%; height: 100%;
	}
	body {
		font-family: Tahoma; font-size: 14px;
		color: #e7e7e7; background-color: #282627;
	}

	.container {
		margin: 0px auto;
		padding: 4% 4% 4% 4%;
	}
	.container > .wraper {
		margin: 0px auto;
		width: 100%;
	}

	.images-container {
		display: flex;
		flex-flow: row wrap;
		width: 100%;
	}
	.images-container > .image-wrapper {
		flex: auto;
		position: relative;
		margin: 2px 2px 2px 2px;
		height: 150px;
		overflow: hidden;
	}
	.images-container > .image-wrapper > img {
		object-fit: cover;
		width: 100%;
		height: 100%;
	}

</style>

<script>
	export default {
		head: {
			title: 'Forviz - 01 - CSS Test'
		},
		data () {
			return {
				Images: [],
			}
		},
		created () {
			this.get_images()
		},
		methods: {
			get_images () {
				this.$axios.get('https://picsum.photos/v2/list').then((res) => {
					this.Images = res.data
				}).catch((errors) => { console.log(errors) })
			}
		}
	}
</script>