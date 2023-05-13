<template>
    <head>

<link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">

</head>


<form method="post">
<div class="container">

  <div class="row">

    <div class="panel panel-primary">
      <div class="panel-heading">
        <h6 class="panel-title">Attendance</h6>

      </div>

      <table class="table table-hover table-striped table-bordered" id="dev-table">
        <thead>

          <tr>
            <th>Student Name</th>
            <th>Present/Absent</th>
          </tr>
        </thead>


    
        <tr>
          <td>{{}}</td>
          <td>{{}}</td>
        </tr>
   



      </table>
        <div class="field">
                      <input type="text" class="input" placeholder="Enter date mm/dd/yyyy">
        </div>
      <input type="submit" style="margin-left: 50px; margin-top: 20px; margin-bottom: 20px;" name="submit" class="btn btn-success" value="Submit Attendance">
    </div>
  </div>
</div>
</form>



</template>


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

  .btnSubmit {
    text-align: center;
  }
</style>


