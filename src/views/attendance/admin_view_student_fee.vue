<template>
<head>
<link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
</head>

<div class="container">
  <div class="row">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h6 class="panel-title">FEE of students</h6>
      </div>
      <table class="table table-hover table-striped table-bordered" id="dev-table">
        <thead>
          <tr>
            <th>Student Name</th>
            <th>Roll</th>
            <th>Contact</th>
            <th>Dues</th>
          </tr>
        </thead>
        <tr v-for="student in students" :key = "student.id">
          <td>{{ student.first_name }}</td>
          <td>{{ student.roll }}</td>
          <td>{{ student.mobile }}</td>
          <td>{{ student.fee }}</td>
        </tr>
      </table>
      
    </div>
  </div>
  <button class="backbutton" onclick="history.back()"> Back</button>

</div>

</template>




<script>
  import axios from 'axios'
  export default {
    data() {
        return {
          students: [],
          
        }
    },
  
    async mounted() {
        console.log('mounted')

        this.getStudents()
    },
    methods: {
      getStudents() {
            axios
                .get(`/attendance/ad_view_students/`)
                .then(response => {
                    console.log(response.data)
                    
                    this.students = response.data
                  

                    
                })
        }
    }
};

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