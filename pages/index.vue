<template>
	<div class="content-container">
		<div class="wrapper">
			<div class="flex flex-wrap" style="padding: 15px 15px 15px 15px;">
				<div class="w-full p-1">
					<a href="/ex1/" target="_blank">
						<button
							class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
						>01 - CSS Test</button>
					</a>
				</div>
				<div class="w-full p-1">
					<a href="/ex2/" target="_blank">
						<button
							class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
						>02 - Venue Booking System (Javascript Test)</button>
					</a>
				</div>
				<div class="w-full p-1">
					<a href="/ex3/?roomId=A101&today=2019-09-28" target="_blank">
						<button
							class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
						>03 - (Optional) Venue Booking System (Front-end Test) </button>
					</a>
				</div>
			</div>
		</div>
	</div>
</template>

<script>

export default {
	head: {
		title: 'Forviz - Test'
	},
	data () {
		return {
		}
	},
	created () {
		this.load_subjects()
	},
	methods: {
		load_subjects () {
			this.$axios.post('http://excel.loiplus.com/q/subjects').then((res) => {
				this.subjects = res.data
				this.subject = this.subjects[0]
				console.table(this.subjects)
			}).catch((errors) => { console.log(errors) })
		}
	}
}

</script>

<style>

	html, body {
		margin: 0px 0px 0px 0px;
		padding: 0px 0px 0px 0px;
		width: 100%; height: 100%;
	}
	body {
		font-family: Tahoma; font-size: 12px;
		color: #e7e7e7; background-color: #282627;
	}

	.content-container {
		display: flex; justify-content: center; align-items: center;
		width: 100%; height: 100%;
	}
	.content-container > .wrapper {
		width: auto;
	}

</style>