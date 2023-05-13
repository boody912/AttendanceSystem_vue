<template>
  <div  v-if= "this.$store.state.user.isAuthenticated && userGroup === 'ADMIN'">
<br>
<br>
<div class="jumbotron" style="margin-bottom:0px;">
  <h1 class="display-4">Admin Login Panel</h1>
  <p class="lead">Welcome to School Management System.</p>
  <hr class="my-4">
  <p>Please select any to contiue...</p>
  <p class="lead">
    <a class="btn btn-danger btn-lg" href="" role="button">Sign Up</a>
    <a class="btn btn-success btn-lg" href="" role="button">Login</a>
  </p>
</div>
</div>
<div v-else>
  <h2 style="margin-left: 40%;">{{ userGroup }} Can't Access this Page </h2>

</div>
</template>
<script>
import axios from 'axios'



export default {
    data() {
        return {
          TeacherCount: null,
          PendingTeacherCount: "0",
          StudentCount: null,
          PendingStudentCount: "0",
          TeacherSalary: null,
          PendingTeacherSalary: "0",
          StudentFee: null,
          PendingStudentFee: "0",

          userGroup: null,
          
          notices: []
        }
    },
  
  
    async mounted() {
        console.log('mounted')

        axios.get('courses/user_group/')
        .then(response => {
        this.userGroup = response.data.group;
        })
        .catch(error => {
        console.log(error);
        });

        this.getDashData()
        this.getNotice()
    },
    methods: {
        getDashData() {
            axios
                .get(`/attendance/ad_dashboard_data/`)
                .then(response => {
                    console.log(response.data)
                    
                    this.TeacherCount = response.data.teachercount
                    this.PendingTeacherCount = response.data.pendingteachercount

                    this.StudentCount = response.data.studentcount
                    this.PendingStudentCount = response.data.pendingstudentcount

                    this.TeacherSalary = response.data.teachersalary
                    this.PendingTeachersalary = response.data.pendingteachersalary

                    this.StudentFee = response.data.studentfee
                    this.PendingStudentfee = response.data.pendingstudentfee

                  
                    
                })
        },
        getNotice() {
            axios
                .get(`/attendance/ad_notice/`)
                .then(response => {
                    console.log(response.data)
                    
                    this.notices = response.data
                   
                    
                })
        }
    }
}
</script>