<template>

<head>
 
  <link href="//maxcdn.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
  
</head>

<!------ student update page by admin(sumit)  ---------->
<form method="post">

  <div class="container register-form">
    <div class="form">
      <div class="note">
        <p>Update Student Details</p>
      </div>

      <div class="form-content">
        <div class="row">
          <div class="col-md-6">
              <div class="form-group">
                <div class="field">                     
                      <input type="text" class="input" placeholder="First Name">
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="User Name" >
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="Contact">
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="Class">
                </div>
              </div>

          </div>

          <div class="col-md-6">
              <div class="form-group">
                <div class="field">                     
                      <input type="text" class="input" placeholder="Last Name">
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="Password" >
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="Fee">
                </div>
              </div>

              <div class="form-group">
                <div class="field">
                      <input type="text" class="input" placeholder="Roll">
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

    .note {
      text-align: center;
      border-radius: 1.5rem;
      height: 80px;
      background: -webkit-linear-gradient(left, #24a0ed, #607d8b);
      color: #fff;
      font-weight: bold;
      line-height: 80px;
    }

    .form-content {
      padding: 5%;
      border-radius: 1.5rem;
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



