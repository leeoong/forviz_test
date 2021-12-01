<template>
	<div>

		<div class="container">
			asdf
		</div>

		<!-- <pre>{{ this.Images }}</pre> -->

	</div>
</template>

<style>

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

	html, body {
		margin: 0px 0px 0px 0px;
		padding: 0px 0px 0px 0px;
		width: 100%; height: 100%;
	}
	body {
		font-family: Tahoma; font-size: 12px;
		color: #e7e7e7; background-color: #282627;
	}

</style>

<script>
export default {
	head: {
		title: 'Forviz - 02 - Venue Booking System (Javascript Test)'
	},
	data () {
		return {
			Images: [],
			BookingData: [
				{
					"id": 1,
					"roomId": "A101",
					"startTime": "2019-09-28 13:00:00",
					"endTime": "2019-09-28 14:00:00",
					"title": "Lunch with Petr"
				},
				{
					"id": 2,
					"roomId": "A101",
					"startTime": "2019-09-28 14:00:00",
					"endTime": "2019-09-28 15:00:00",
					"title": "Sales Weekly Meeting"
				},
				{
					"id": 3,
					"roomId": "A101",
					"startTime": "2019-09-28 16:00:00",
					"endTime": "2019-09-28 18:00:00",
					"title": "Anastasia Website Warroom"
				},
				{
					"id": 4,
					"roomId": "A101",
					"startTime": "2019-09-29 13:00:00",
					"endTime": "2019-09-29 14:00:00",
					"title": "One-on-One Session"
				},
				{
					"id": 5,
					"roomId": "A101",
					"startTime": "2019-09-29 16:00:00",
					"endTime": "2019-09-29 18:00:00",
					"title": "UGC Sprint Planning"
				},
				{
					"id": 6,
					"roomId": "A102",
					"startTime": "2019-09-30 09:00:00",
					"endTime": "2019-10-04 18:00:00",
					"title": "5-Day Design Sprint Workshop"
				},
				{
					"id": 7,
					"roomId": "Auditorium",
					"startTime": "2019-09-19 09:00:00",
					"endTime": "2019-09-23 19:00:00",
					"title": "Thai Tech Innovation 2019"
				},
				{
					"id": 8,
					"roomId": "A101",
					"startTime": "2019-09-28 10:00:00",
					"endTime": "2019-09-28 13:00:00",
					"title": "Raimonland project"
				},
				{
					"id": 9,
					"roomId": "A102",
					"startTime": "2019-09-30 18:00:00",
					"endTime": "2019-09-30 20:00:00",
					"title": "Management Meetinng"
				},
				{
					"id": 10,
					"roomId": "A101",
					"startTime": "2019-10-04 14:00:00",
					"endTime": "2019-10-06 11:00:00",
					"title": "3-day workshop Corgi costume"
				}
			],
		}
	},
	created () {
		// this.load_subjects()
	},
	methods: {
		load_subjects () {
			this.$axios.get('https://picsum.photos/v2/list').then((res) => {
				this.Images = res.data
			}).catch((errors) => { console.log(errors) })
		}
	}
}
</script>