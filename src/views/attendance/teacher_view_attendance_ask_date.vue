<template>
    <head>
  
  <link href="//maxcdn.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
  
</head>

<!------ date page for attendance by teacher(sumit)  ---------->
<form method="post">
 
  <div class="container register-form">
    <div class="form">
      <div class="note">
        <p>PLEASE ENTER DATE FOR ATTENDANCE OF CLASS &nbsp <strong>{{}}</strong></p>
      </div>

      <div class="form-content">
        <div class="row">
          <div class="col-md-12">
            <div class="form-group">
              <div class="field">
                      <input type="text" class="input" placeholder="Enter date mm/dd/yyyy">
              </div>
            </div>

          </div>

        </div>
        <button type="submit" class="btnSubmit">Submit</button>
      </div>
    </div>
  </div>

</form>


</template>

<style media="screen">
    a:link {
      text-decoration: none;
    }

    /* .note {
      text-align: center;
      height: 80px;
       background: -webkit-linear-gradient(left, #343a40, #607d8b);
      color: #fff;
      font-weight: bold;
      line-height: 80px;
    } */

    .form-content {
      padding: 5%;
      border: 1px solid #ced4da;
      margin-bottom: 2%;
    }

    .form-control {
      border-radius: 1.5rem;
    }

    .btnSubmit {
      border: none;
      border-radius: 1.5rem;
      padding: 1%;
      width: 20%;
      cursor: pointer;
      background: #4caf50;
      color: #fff;
    }
  </style>


