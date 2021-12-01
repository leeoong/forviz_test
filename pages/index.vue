<template>
  <b-container class="h-100" fluid style="background-color: #e00000;">
    <b-row>
      <b-col>1 of 3</b-col>
      <b-col>2 of 3</b-col>
      <b-col>
        aaaa {{ this.$route.params.order_id }} bbbb
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  head: {
    title: 'Forviz - test'
  },
  data () {
    return {
      subject_add: false,
      subject_code: '',
      subject_name: '',
      term: 1,
      year: (parseInt(new Date().getFullYear()) + 543),
      file: null,
      subject: null,
      subjects: [],
      table_columns: [
        { name: 'subject_code', label: 'รหัสวิชา', field: 'subject_code', sortable: true, align: 'center' },
        { name: 'subject_name', label: 'ชื่อวิชา', field: 'subject_name', sortable: true, align: 'left' },
        { name: 'ty', label: 'เทอม/ปี', field: 'term', sortable: true },
        { name: 'name', label: 'ชื่อไฟล์', field: 'name', sortable: true, required: true, align: 'left' },
        { name: 'remove' }
      ],
      table_data: []
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
</style>