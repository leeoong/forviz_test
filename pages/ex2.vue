<template>
	<div class="content-container">
		<div class="wrapper">

			<div class="flex" style="padding: 15px 15px 15px 15px;">

				<div class="form">
					<div class="flex flex-wrap">

						<div class="w-full p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Check Availability
							</label>
						</div>
						
						<div class="w-full p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Room
							</label>
							<div class="relative">
								<select
									v-model="Room"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
								>
									<option
										v-for="(r, i) in Rooms" :key="i"
										:value="r.value"
										name="room"
									>{{ r.label }}</option>
								</select>
							</div>
						</div>
						
						<div class="w-6/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Start time
							</label>
							<div class="relative">
								<input
									v-model="StartDate"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="date"
								/>
							</div>
						</div>
						<div class="w-3/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Hour
							</label>
							<div class="relative">
								<input
									v-model="StartHour"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="text"
								/>
							</div>
						</div>
						<div class="w-3/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Minute
							</label>
							<div class="relative">
								<input
									v-model="StartMinute"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="text"
								/>
							</div>
						</div>

						<div class="w-6/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								End time
							</label>
							<div class="relative">
								<input
									v-model="EndDate"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="date"
								/>
							</div>
						</div>
						<div class="w-3/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Hour
							</label>
							<div class="relative">
								<input
									v-model="EndHour"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="text"
								/>
							</div>
						</div>
						<div class="w-3/12 p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Minute
							</label>
							<div class="relative">
								<input
									v-model="EndMinute"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="text"
								/>
							</div>
						</div>

						<div class="w-full p-1 mb-4" style="text-align: center;">
							<span
								:class="MessageColor == 'green' ? 'message-green' : 'message-red'"
								style="font-size: 16px;"
							>{{ Message }}</span>
						</div>

						<div class="w-full p-1">
							<button
								@click="handleCheckAvailability"
								class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
							>Check Availability</button>
						</div>

					</div>
				</div>

				<div class="form">
					<div class="flex flex-wrap">

						<div class="w-full p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Get Bookings For Week
							</label>
						</div>

						<div class="w-full p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Room
							</label>
							<div class="relative">
								<select
									v-model="TodayRoom"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
								>
									<option
										v-for="(r, i) in Rooms" :key="i"
										:value="r.value"
										name="room"
									>{{ r.label }}</option>
								</select>
							</div>
						</div>
						
						<div class="w-full p-1 mb-4">
							<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
								Today
							</label>
							<div class="relative">
								<input
									v-model="Today"
									class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
									value=""
									type="date"
								/>
							</div>
						</div>

						<div class="w-full p-1 mb-4">
							<table style="color: #000;" width="100%" border="1" cellpadding="5" cellspacing="0">
								<thead>
									<tr style="text-align: left;">
										<th colspan="5">BookingsToday</th>
									</tr>
									<tr>
										<th>id</th>
										<th>roomId</th>
										<th>startTime</th>
										<th>endTime</th>
										<th>title</th>
									</tr>
								</thead>
								<tbody>
									<tr v-for="(r, i) in BookingsToday" :key="i">
										<td>{{ r.id }}</td>
										<td>{{ r.roomId }}</td>
										<td>{{ r.startTime }}</td>
										<td>{{ r.endTime }}</td>
										<td>{{ r.title }}</td>
									</tr>
								</tbody>
							</table>
						</div>

						<div class="w-full p-1 mb-4">
							<table style="color: #000;" width="100%" border="1" cellpadding="5" cellspacing="0">
								<thead>
									<tr style="text-align: left;">
										<th colspan="5">BookingsThisWeek</th>
									</tr>
									<tr>
										<th>id</th>
										<th>roomId</th>
										<th>startTime</th>
										<th>endTime</th>
										<th>title</th>
									</tr>
								</thead>
								<tbody>
									<tr v-for="(r, i) in BookingsThisWeek" :key="i">
										<td>{{ r.id }}</td>
										<td>{{ r.roomId }}</td>
										<td>{{ r.startTime }}</td>
										<td>{{ r.endTime }}</td>
										<td>{{ r.title }}</td>
									</tr>
								</tbody>
							</table>
						</div>

						<div class="w-full p-1 mb-4">
							<table style="color: #000;" width="100%" border="1" cellpadding="5" cellspacing="0">
								<thead>
									<tr style="text-align: left;">
										<th colspan="5">BookingsNextWeek</th>
									</tr>
									<tr>
										<th>id</th>
										<th>roomId</th>
										<th>startTime</th>
										<th>endTime</th>
										<th>title</th>
									</tr>
								</thead>
								<tbody>
									<tr v-for="(r, i) in BookingsNextWeek" :key="i">
										<td>{{ r.id }}</td>
										<td>{{ r.roomId }}</td>
										<td>{{ r.startTime }}</td>
										<td>{{ r.endTime }}</td>
										<td>{{ r.title }}</td>
									</tr>
								</tbody>
							</table>
						</div>

						<div class="w-full p-1">
							<button
								@click="getBookingsForWeek"
								class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
							>Get Bookings For Week</button>
						</div>

					</div>
				</div>

			</div>

		</div>
	</div>
</template>

<script>

import moment from 'moment'

export default {
	head: {
		title: 'Forviz - 02 - Venue Booking System (Javascript Test)'
	},
	data () {
		return {

			Rooms: [
				{
					value: "A101",
					label: "Room - A101"
				},
				{
					value: "A102",
					label: "Room - A102"
				},
				{
					value: "Auditorium",
					label: "Room - Auditorium"
				},
			],
			Room: "A101",
			// StartDate: moment().format('YYYY-MM-DD'),
			StartDate: "2019-10-05",
			StartHour: "00",
			StartMinute: "00",
			// EndDate: moment().format('YYYY-MM-DD'),
			EndDate: "2019-10-05",
			EndHour: "23",
			EndMinute: "59",
			Message: "",
			MessageColor: "",

			TodayRoom: "A101",
			Today: "2019-09-28",

			BookingsToday: [],
			BookingsThisWeek: [],
			BookingsNextWeek: [],
			BookingsWholeMonth: [],

		}
	},
	created () {
	},
	methods: {
		handleCheckAvailability () {
			this.$axios.post('http://localhost:8888/checkAvailability',{
				room: this.Room,
				startTime: this.StartDate+" "+this.StartHour+":"+this.StartMinute+":00",
				endTime : this.EndDate+" "+this.EndHour+":"+this.EndMinute+":59",
			}).then((res) => {
				console.log("Found booking")
				console.table(res.data)
				if( res.data.length == 0 ){
					this.Message = "Room "+this.Room+" is available for booking";
					this.MessageColor = "green";
				}else{
					this.Message = "Room "+this.Room+" is not available for booking";
					this.MessageColor = "red";
				}
			}).catch((errors) => { console.log(errors) })
		},
		getBookingsForWeek () {
			this.$axios.post('http://localhost:8888/getBookingsForWeek',{
				room: this.TodayRoom,
				today: this.Today,
			}).then((res) => {
				console.table(res.data)
				this.BookingsToday = []
				this.BookingsToday = res.data.BookingsToday
				this.BookingsThisWeek = res.data.BookingsThisWeek
				this.BookingsNextWeek = res.data.BookingsNextWeek
				this.BookingsWholeMonth = res.data.BookingsWholeMonth
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
		font-family: Tahoma; font-size: 14px;
		color: #e7e7e7; background-color: #282627;
	}

	#__nuxt {
		width: 100%; min-height: 100%;
	}
	#__layout {
		width: 100%; min-height: 100%;
	}

	.content-container {
		display: flex; justify-content: center; align-items: center;
		width: 100%; height: 100%;
	}
	.content-container > .wrapper {
		width: auto;
	}

	.form {
		margin: 15px 15px 15px 15px;
		padding: 15px 15px 15px 15px;
		width: 480px;
		background-color: #fafafa;
		border-radius: 8px;
	}
	.message-green {
		color: green;
	}
	.message-red {
		color: red;
	}

	th {
		font-weight: normal;
	}
	th, td {
		border: 1px solid #eaeaea;
	}

</style>
