<template>
<div  v-if= "this.$store.state.user.isAuthenticated && userGroup === 'ADMIN'">
  <!DOCTYPE html>
  <html lang="en" dir="ltr">

  <head>
    <meta charset="utf-8">
    <title>SMS - Django</title>
    <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.1/css/all.min.css">
    <link href="http://netdna.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
  </head>

  <body>

  <input type="checkbox" id="check">
  <!--header area start-->
  <header class="noteadmin">
    <label for="check">
      
      <div >
        <i ></i>
        <h3 class="fas fa-bars" id="sidebar_btn">Admin Panel</h3>
      </div>
    </label>
    

  </header>
  <!--header area end-->

  <!--sidebar start-->
  <div class="sidebaradmin">
    <center>

      <img src="" class="profile_image" alt="">
      <h4>Admin </h4>

    </center>

    <router-link to="/attendance/admin-base" class="fas fa-desktop" ><span>MY Account</span></router-link>
    <router-link to="/attendance/admin-teacher" class="fas fa-chalkboard-teacher" ><span>Teacher</span></router-link>
    <router-link to="/attendance/admin-student" class="fas fa-user-graduate" ><span>Student</span></router-link>

    <router-link to="/attendance/admin-attendance" class="fas fa-address-card" ><span>Attendance</span></router-link>
    <router-link to="/attendance/admin-fee" class="fas fa-dollar-sign" ><span>Fee</span></router-link>
    <router-link to="/attendance/admin-notice" class="fas fa-bullhorn" ><span>Notice</span></router-link>

  </div>
  <!--sidebar end-->


  <!--content start-->
  <div class="contentadminj">
    <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css" rel="stylesheet">
      <div class="container">
        <div class="row">
          
          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-blue order-card">          
              <div class="card-block">                       
                <h6 class="m-b-20">Total Teacher</h6>
                <h2 class="text-right"><i class="fas fa-chalkboard-teacher f-left"></i><span>{{TeacherCount}}</span></h2>   
                <p class="m-b-0">{{teacherCount}}<span class="f-right">{{teacherCount}}</span></p>               
              </div>
              
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-green order-card">
              <div class="card-block">
                <h6 class="m-b-20">Total Student</h6>
                <h2 class="text-right"><i class="fas fa-user-graduate f-left"></i><span>{{StudentCount}}</span></h2>
                <p class="m-b-0">{{ studentCount }}<span class="f-right">{{Studentcount}}</span></p>
              </div>
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-yellow order-card">
              <div class="card-block">
                <h6 class="m-b-20">Teacher's Salary</h6>
                <h2 class="text-right"><i class="fas fa-dollar f-left"></i><span>{{TeacherSalary}}</span></h2>
                <p class="m-b-0"><span class="f-right">{{ Teachersalary}}</span></p>
              </div>
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-pink order-card">
              <div class="card-block">
                <h6 class="m-b-20">Student Fee</h6>
                <h2 class="text-right"><i class="fas fa-dollar f-left"></i><span>{{StudentFee}}</span></h2>
                <p class="m-b-0">{{ Studentfee }}<span class="f-right">{{Studentfee}}</span></p>
              </div>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-blue order-card">
              <div class="card-block">
                <h6 class="m-b-20">Pending Teacher</h6>
                <h2 class="text-right"><i class="fas fa-spinner f-left"></i><span class="f-right"></span></h2>
                <p class="m-b-0"><span class="f-right">{{PendingTeacherCount}}</span></p>
              </div>
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-green order-card">
              <div class="card-block">
                <h6 class="m-b-20">Pending Admissions</h6>
                <h2 class="text-right"><i class="fas fa-spinner f-left"></i><span class="f-right"></span></h2>
                <p class="m-b-0"><span class="f-right">{{PendingStudentCount}}</span></p>
              </div>
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-yellow order-card">
              <div class="card-block">
                <h6 class="m-b-20">Pending Salary</h6>
                <h2 class="text-right"><i class="fas fa-spinner f-left"></i><span class="f-right"></span></h2>
                <p class="m-b-0"><span class="f-right">{{PendingTeacherSalary}}</span></p>
              </div>
            </div>
          </div>

          <div class="col-md-4 col-xl-3">
            <div class="card bg-c-pink order-card">
              <div class="card-block">
                <h6 class="m-b-20">Pending Dues</h6>
                <h2 class="text-right"><i class="fas fa-spinner f-left"></i><span class="f-right"></span></h2>
                <p class="m-b-0"><span class="f-right">{{PendingStudentFee }}</span></p>
              </div>
            </div>
          </div>
        </div>
      </div>
  <div class="w3-panel w3-black">
    <p>Notice Board</p>
  </div>

  <div class="alert" v-for="notice in notices" :key="notice.id" >
    <span class="closebtn" onclick="this.parentElement.style.display='none';" >&times;</span>
    <strong >Posted on {{notice.date}} </strong><br><b>By : {{notice.by}}</b><br> {{notice.message}}
  </div>
  
  </div>
  <!--content end-->



  </body>


  </html>
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
