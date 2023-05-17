<template>
<head>
 
  <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">

</head>

</template>

<style media="screen">

/* admin_dashboard*/
.alert {
  margin-left: 25%;
  margin-right: 25%;
  padding: 20px;
  background-color: #f44336;
  color: white;
}

.w3-panel p {
  padding-top: 10px;
}

.closebtn {
  margin-left: 15px;
  color: white;
  font-weight: bold;
  float: right;
  font-size: 22px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}

.closebtn:hover {
  color: black;
}

 /* admin_dashboard_cards*/

a:link {
        text-decoration: none;
      }

      .order-card {
        color: #fff;
      }

      .bg-c-blue {
        background: linear-gradient(45deg, #4099ff,#4a5c64);
      }

      .bg-c-green {
        background: linear-gradient(45deg, #2ed8b6, #4a5c64);
      }

      .bg-c-yellow {
        background: linear-gradient(45deg, #FFB64D, #4a5c64);
      }

      .bg-c-pink {
        background: linear-gradient(45deg, #30a33a, #4a5c64);
      }


      .card {
        border-radius: 5px;
        -webkit-box-shadow: 0 1px 2.94px 0.06px rgba(4, 26, 55, 0.16);
        box-shadow: 0 1px 2.94px 0.06px rgba(4, 26, 55, 0.16);
        border: none;
        margin-bottom: 30px;
        -webkit-transition: all 0.3s ease-in-out;
        transition: all 0.3s ease-in-out;
      }

      .card .card-block {
        padding: 25px;
      }

      .order-card i {
        font-size: 26px;
      }

      .f-left {
        float: left;
      }

      .f-right {
        float: right;
      }


/* base*/
      a:link {
  text-decoration: none;
}

body {
  margin: 0;
  padding: 0;
  font-family: "Roboto", sans-serif;
  
 
}


.noteadmin {
      text-align: center;
      height: 80px;
      background: -webkit-linear-gradient(left, #24a0ed, #607d8b);
      color: #fff;
      font-weight: bold;
      line-height: 80px;
   
    }

.left_area h3 {
  color: #fff;
  margin: 0px;
  text-transform: uppercase;
  font-size: 22px;
  font-weight: 900;
}

.left_area span {
  
  color: #19B3D3;
}

.sidebaradmin {
  border-top-right-radius: 1.5rem;
  
  color: -webkit-linear-gradient(left, #24a0ed, #2ea0e7);
  margin-top: 0px;
  padding-top: 30px;
  position: fixed;
  left: 0;
  width: 250px;
  
  transition: 0.5s;
  transition-property: left;
  overflow: hidden;
}

.sidebaradmin .profile_image {
  width: 100px;
  height: 100px;
  background: -webkit-linear-gradient(left, #24a0ed, #2ea0e7);
  border-radius: 100px;
  margin-bottom: 10px;
}

.sidebaradmin h4 {
 
  color: #ccc;
  background: -webkit-linear-gradient(bottom , #607d8b, #2ea0e7);
  height: 180px;
  margin-top: -140px;
  margin-bottom: 0px;
}

.sidebaradmin a {
  color: #fff;
  background: #607d8b;
  display: block;
  width: 100%;
  line-height: 60px;
  text-decoration: none;
  padding-left: 40px;
  box-sizing: border-box;
  transition: 0.5s;
  

}

.sidebaradmin a:hover {
  background: #e9e9e9;
}

.sidebaradmin i 
{
  padding-right: 10px;
}

label #sidebar_btn {
  
  z-index: 1;
  color: #fff;
  cursor: pointer;
  right: 650px;
  font-size: 20px;
  margin: 5px 0;
  transition: 0.5s;
  transition-property: color;
}

label #sidebar_btn:hover {
  color: #19B3D3;
}

#check:checked~.sidebaradmin {
  left: -190px;
}

#check:checked~.sidebaradmin a span {
  display: none;
}

#check:checked~.sidebaradmin a {
  font-size: 20px;
  margin-left: 170px;
  width: 80px;
}


.contentadminj {
  margin-left: 250px;
  background-position: center;
  background-size: cover;
  height: 400px;
  transition: 0.5s;

}

#check:checked~.contentadminj {
  margin-left: 60px;
}

#check {
  display: none;
}

</style>








