<template>
  <div  v-if= "this.$store.state.user.isAuthenticated && userGroup === 'ADMIN'">
    <head>

<link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">

</head>



<!--
written By : sumit kumar
-->

<div class="container">

<div class="row">

  <div class="panel panel-primary">
    <div class="panel-heading">
      <h6 class="panel-title">Teachers</h6>

    </div>

    <table class="table table-hover table-striped table-bordered" id="dev-table">
      <thead>

        <tr>
          <th>Name</th>
          <th>Contact</th>
          <th>Salary</th>
          <th>Joining Date</th>
          <th>Actions</th>
          
        </tr>
      </thead>
     
      <tr>
        <td> {{}}</td>
        <td>{{}}</td>
        <td>{{}}</td>
        <td>{{}}</td>
        <td><a class="btn btn-success btn-xs" href="{% url 'approve-teacher' t.id  %}"><span class="glyphicon glyphicon-ok"></span></a>
        <a class="btn btn-danger btn-xs" href="{% url 'delete-teacher' t.id  %}"><span class="glyphicon glyphicon-trash"></span></a></td>
      </tr>

    
    </table>
  </div>


</div>
<button class="backbutton" onclick="history.back()"> Back</button>
</div>

<!--
    written By : sumit kumar
    -->

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
  a:link {
    text-decoration: none;
  }

  h6 {
    text-align: center;
  }

  .row {
    margin: 100px;
  }
</style>


