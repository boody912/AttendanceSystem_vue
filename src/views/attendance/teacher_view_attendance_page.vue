<template>
<head>
  <link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
</head>
<div class="container">
  <div class="row">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h6 class="panel-title">Attendance of class {} and date {}</h6>
      </div>
      <table class="table table-hover table-striped table-bordered" id="dev-table">
        <thead>
          <tr>
            <th>Student Name</th>
            <th>Student Roll</th>
            <th>Present/Absent</th>
          </tr>
        </thead>
        <tr>
          <td>{}</td>
          <td>{}</td>
          <td>{}</td>
        </tr>
        
      </table>
    </div>
  </div>
</div>

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
  </style>