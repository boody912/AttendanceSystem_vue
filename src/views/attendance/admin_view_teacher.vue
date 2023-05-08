<template>
<head>

  <meta name="viewport" content="width=device-width, initial-scale=1">

<link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
</head>


<div class="container">

    	<div class="row" >

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
              <tr  v-for="teacher in teachers" :key="teacher.id">
                  <td> {{ teacher.first_name }}</td>
                  <td>{{ teacher.mobile }}</td>
                  <td>{{ teacher.salary }}</td>
                  <td>{{ teacher.joindate }}</td>
                  <td>
                    <a class="btn btn-primary btn-xs" href="{% url 'update-teacher' t.id  %}"  ><span class="glyphicon glyphicon-edit"></span></a>
                    <a class="btn btn-danger btn-xs" href="/attendance/admin-view-teacher"  ><span class="glyphicon glyphicon-trash"></span></a>
                  </td>
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
          teachers: [],
          
        }
    },
  
    async mounted() {
        console.log('mounted')

        this.getTeachers()
    },
    methods: {
      getTeachers() {
            axios
                .get(`/attendance/ad_view_teachers/`)
                .then(response => {
                    console.log(response.data)
                    
                    this.teachers = response.data
                  

                    
                })
        }
    }
};

</script>







  <style media="screen">
    a:link {
      text-decoration: none;
    }
    h6{
      text-align:center;
    }
    .row{
      margin:100px;
    }

  .backbutton {

  padding: 15px 25px;
  font-size: 20px;
  text-align: center;
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #607d8b;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
  width: 3cm;
}

.backbutton:hover {background-color: #850505}

.button:active {
  background-color: #3e8e41;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

  </style>