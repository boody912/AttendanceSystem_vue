<template>
    <div  v-if= "this.$store.state.user.isAuthenticated && userGroup === 'ADMIN'">
        <!DOCTYPE html>
        <html lang="en" dir="ltr">

        <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>SMS - Django</title>
        

        <title></title>
        </head>

        <body>

       
        <br><br>
        <center>
            <h3 class='alert alert-success' style="margin-bottom:0px;">About Us !</h3>
        </center>
        <div class="jumbotron" style="margin-bottom: 0px;margin-top: 0px;">
            <h1 class="display-4">TEXT TEXT</h1>
            <p class="lead">TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT</p>
            <hr class="my-4">
            <p>Explore our Website.</p>
            <p class="lead">
            <a class="btn btn-primary btn-lg" href="/" role="button">HOME</a>
            </p>
        </div>

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

<style media="screen">
        .jumbotron {
        margin-top: 0px;
        margin-bottom: 0px;
        }

        .jumbotron h1 {
        text-align: center;
        }

        .alert {
        margin: 0px;
        }
    </style>