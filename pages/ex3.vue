<template>
	<div class="content-container">
		<div class="wrapper">
			<div class="panel">
				<div class="panel-left">
					<div class="panel-title">{{ TodayRoom }}</div>
					<div style="padding-top: 85px;">Upcoming</div>
					<div style="padding-top: 30px; font-size: 36px; opacity: 0.5;">{{ DateOfWeek }}</div>
					<div style="padding-top: 0px; font-size: 36px;">{{ DateShow }}</div>
					<div style="height: 60px;"></div>
					<div
						v-for="(r, i) in BookingsToday" :key="i"
						style="padding-bottom: 20px;"
					>
						<div style="opacity: 0.65;">{{ r.begin }} - {{ r.end }}</div>
						<div>{{ r.title }}</div>
					</div>
					<div style="position: absolute; left: 0px; bottom: 0px; width: 100%; height: 225px; background-color: rgba(215,215,215,0.05);"></div>
				</div>
				<div class="panel-right">

					<div class="tab-container">
						<div class="tab" tabindex="-1" @click="getTabContent('thisweek')">
							<div style="padding-bottom: 5px;">THIS WEEK</div>
							<div class="tab-highlight"></div>
						</div>
						<div class="tab" tabindex="-1" @click="getTabContent('nextweek')">
							<div style="padding-bottom: 5px;">NEXT WEEK</div>
							<div class="tab-highlight"></div>
						</div>
						<div class="tab" tabindex="-1" @click="getTabContent('wholemonth')">
							<div style="padding-bottom: 5px;">WHOLE MONTH</div>
							<div class="tab-highlight"></div>
						</div>
					</div>

					<div class="tab-content">
						<div
							v-for="(r, i) in DateLists" :key="i"
							style="padding-top: 40px;"
						>
							<div class="date-title">{{ r.DateOfWeek }}, {{ r.DateShow }}</div>
							<div
								v-for="(booking, i_booking) in r.Bookings" :key="i_booking"
								style="position: relative; padding: 20px 0px 0px 60px;"
							>
								<div style="opacity: 0.65;">{{ booking.begin }} - {{ booking.end }}</div>
								<div>{{ booking.title }}</div>
								<div class="dot"></div>
							</div>
						</div>
					</div>

					<pre>{{ DateLists }}</pre>

					<div class="vertical-line"></div>

				</div>
			</div>
		</div>
	</div>
</template>

<script>

import moment from 'moment'

export default {
	head: {
		title: 'Forviz - 03 - (Optional) Venue Booking System (Front-end Test) '
	},
	data () {
		return {

			DateOfWeek: moment(this.$route.query.today, 'YYYY-MM-DD').format('dddd'),
			DateShow: moment(this.$route.query.today, 'YYYY-MM-DD').format('DD MMM'),

			TodayRoom: this.$route.query.roomId,
			Today: this.$route.query.today,

			BookingsToday: [],
			BookingsThisWeek: [],
			BookingsNextWeek: [],
			BookingsWholeMonth: [],

			DateLists: [],

		}
	},
	mounted () {
		this.getBookingsForWeek()
	},
	methods: {
		getBookingsForWeek () {
			this.$axios.post('http://localhost:8888/getBookingsForWeek',{
				room: this.TodayRoom,
				today: this.Today,
			}).then((res) => {
				console.table(res.data)
				this.BookingsToday = res.data.BookingsToday
				this.BookingsThisWeek = res.data.BookingsThisWeek
				this.BookingsNextWeek = res.data.BookingsNextWeek
				this.BookingsWholeMonth = res.data.BookingsWholeMonth

				this.BookingsToday.forEach(function( r, i ){
					console.log(r)
					r.begin = moment(r.startTime, 'YYYY-MM-DD hh:mm:ss').format('hh:mm')
					r.end = moment(r.endTime, 'YYYY-MM-DD hh:mm:ss').format('hh:mm')
				})
				
				this.getTabContent('thisweek')

			}).catch((errors) => { console.log(errors) })
		},
		getTabContent (type) {

			let CurrentBookings = []

			if( type == "thisweek" ){
				CurrentBookings = this.BookingsThisWeek
			}else if( type == "nextweek" ){
				CurrentBookings = this.BookingsNextWeek
			}else if( type == "wholemonth" ){
				CurrentBookings = this.BookingsWholeMonth
			}

			let DateLists = []
			CurrentBookings.forEach(function( r, i ){
				let CurrentDate = moment(r.startTime, 'YYYY-MM-DD hh:mm:ss').format('YYYY-MM-DD')
				if( !DateLists.includes(CurrentDate) ){
					DateLists.push(CurrentDate)
				}
			})

			DateLists.forEach(function( DateList, i_DateList ){
				DateLists[i_DateList] = {
					Date: DateList,
					DateOfWeek: moment(DateList, 'YYYY-MM-DD').format('dddd'),
					DateShow: moment(DateList, 'YYYY-MM-DD').format('DD MMM'),
					Bookings: []
				}
				CurrentBookings.forEach(function( r, i ){
					let CurrentDate = moment(r.startTime, 'YYYY-MM-DD hh:mm:ss').format('YYYY-MM-DD')
					if( DateList == CurrentDate ){
						r.begin = moment(r.startTime, 'YYYY-MM-DD hh:mm:ss').format('hh:mm')
						r.end = moment(r.endTime, 'YYYY-MM-DD hh:mm:ss').format('hh:mm')
						DateLists[i_DateList].Bookings.push(r)
					}
				})
			})

			this.DateLists = DateLists

			console.log(this.DateLists)

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
		font-family: Tahoma; font-size: 14px;
		color: #e7e7e7; background-color: #282627;
	}

	#__nuxt {
		width: 100%; height: 100%;
	}
	#__layout {
		width: 100%; height: 100%;
	}

	.content-container {
		display: flex; justify-content: center; align-items: center;
		width: 100%; height: 100%;
	}
	.content-container > .wrapper {
		position: relative;
	}

	.panel {
		display: flex; justify-content: center; align-items: flex-start;
		width: 960px; height: 640px;
		letter-spacing: 1px;
		font-family: Arial;
		background-color: #414141;
		overflow: hidden;
	}
	.panel-left {
		position: relative;
		padding: 0px 0px 0px 60px;
		width: 40%; height: 100%;
		background-color: #46529e;
	}
	.panel-left > .panel-title {
		padding: 0px 0px 0px 40px;
		height: 60px; line-height: 75px;
		font-size: 26px; font-weight: bold;
		color: #fff; background-color: #2ebaef;
	}
	.panel-right {
		flex-grow: 1;
		position: relative;
		height: 100%;
		color: #000; background-color: #fff;
	}

	.tab-container {
		position: absolute;
		z-index: 3;
		left: 0px; top: 0px;
		display: flex; justify-content: flex-start; align-items: flex-end;
		padding: 0px 20px 0px 20px;
		width: 100%; height: 60px;
		background-color: #fafafa;
		-webkit-box-shadow: inset rgba(0,0,0,0.1) 10px -7px 10px;
		-moz-box-shadow: inset rgba(0,0,0,0.1) 10px -7px 10px;
		box-shadow: inset rgba(0,0,0,0.1) 10px -7px 10px;
	}
	.tab-container > .tab {
		padding: 0px 20px 0px 20px;
		font-weight: bold;
		cursor: pointer;
	}
	.tab-container > .tab:focus > .tab-highlight {
		background-color: #46529e;
	}
	.tab-container > .tab > .tab-highlight {
		margin: 0px auto;
		width: 30px; height: 3px;
		background-color: transparent;
	}

	.tab-content {
		position: relative;
		z-index: 2;
		min-height: 100%;
		padding: 60px 0px 0px 0px;
	}
	.vertical-line {
		position: absolute;
		z-index: 1;
		left: 40px; top: 0px;
		width: 1px; height: 100%;
		background-color: #eaeaea;
	}

	.date-title {
		padding: 0px 0px 0px 60px;
		height: 30px; line-height: 30px;
		font-size: 14px; font-weight: bold;
		color: #aeaeae; background-color: #fafafa;
		border: 1px solid #eaeaea;
	}

	.dot {
		position: absolute;
		left: 37px; top: 27px;
		width: 6px; height: 6px;
		background-color: #e00;
		border-radius: 50%;
	}

</style>
