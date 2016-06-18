# postpaid-web
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <script src="//code.jquery.com/jquery-1.10.2.js"></script>
        <script src="//code.jquery.com/ui/1.11.4/jquery-ui.js"></script>

        <!--function buat div-->
        <script>
            $(function() {
                $( "#tabs" ).tabs();
            });
        </script>

        <style>
            body {
                margin: 0;
            }

            #horizontal-nav {
                list-style-type: none;
                margin: 0;
                padding: 0;
                overflow: hidden;
                background-color: #333;
            }

            .horizontal-li {
                float: right;
            }

            .horizontal-li a, .dropbtn {
                display: inline-block;
                color: white;
                text-align: center;
                padding: 14px 16px;
                text-decoration: none;
            }

            .horizontal-li a:hover, .dropdown:hover .dropbtn {
                background-color: red;
            }

            .horizontal-li.dropdown {
                display: inline-block;
            }

            .dropdown-content {
                display: none;
                position: absolute;
                background-color: #f9f9f9;
                min-width: 160px;
                box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            }

            .dropdown-content a {
                color: black;
                padding: 12px 16px;
                text-decoration: none;
                display: block;
                text-align: left;
            }

            .dropdown-content a:hover {background-color: #f1f1f1}

            .dropdown:hover .dropdown-content {
                display: block;
            }

            #vertical-nav {
                list-style-type: none;
                margin: 0;
                padding: 0;
                width: 15%;
                background-color: #f1f1f1;
                position: fixed;
                height: 100%;
                overflow: auto;
            }

            .vertical-li a {
                display: block;
                color: #000;
                padding: 8px 0 8px 16px;
                text-decoration: none;
            }

            .vertical-li a.active {
                background-color: #4CAF50;
                color: white;
            }

            .vertical-li a:hover:not(.active) {
                background-color: #555;
                color: white;
            }

            #konten {
                margin-left: 15%;
                padding: 1px 16px;
                height: 1000px;
            }

        </style>
    </head>

    <body>
        <?php
            $con = mysqli_connect("127.0.0.1","root","","web_report");

            // Check connection
            if (mysqli_connect_errno()) {
                echo "Failed to connect to MySQL: " . mysqli_connect_error();
            }
        ?>

        <!--Navbar horizontal paling atas-->
        <ul id="horizontal-nav">
            <li class="horizontal-li"><a href="index.php">Nasional</a></li>
            <li class="horizontal-li dropdown">
                <a href="#" class="dropbtn">Regional</a>
                <div class="dropdown-content">
                <a href="sumbagut.php">Sumbagut</a>
                <a href="#">Link 2</a>
                <a href="#">Link 3</a>
                </div>
            </li>
        </ul>

        
        <div id="tabs">
            <ul id="vertical-nav">            
                <li class="vertical-li"><a href="#tabs-1">Revenue</a></li>
                <li class="vertical-li"><a href="#tabs-2">Total CB</a></li>
                <li class="vertical-li"><a href="#tabs-3">Sales</a></li>
                <li class="vertical-li"><a href="#tabs-4">Churn</a></li>
                <li class="vertical-li"><a href="#tabs-5">Net Add</a></li>
                <li class="vertical-li"><a href="#tabs-6">Data User</a></li>
                <li class="vertical-li"><a href="#tabs-7">Smartphone User</a></li>
                <li class="vertical-li"><a href="#tabs-8">LTE</a></li>
            </ul>

            <?php
                function destroy_semua() {
                    unset($GLOBALS['filteryear']);
                    unset($GLOBALS['filtermonth1']);
                    unset($GLOBALS['filtermonth2']);
                }
            ?>
            </br>
            <div id="konten">
                <form action="index.php" method="POST">
                    <select id="firstmonth" name="firstmonth">
                        <option value="1">Januari</option>
                        <option value="2">Februari</option>
                        <option value="3">Maret</option>
                        <option value="4">April</option>
                        <option value="5">Mei</option>
                        <option value="6">Juni</option>
                        <option value="7">Juli</option>
                        <option value="8">Agustus</option>
                        <option value="9">September</option>
                        <option value="10">Oktober</option>
                        <option value="11">November</option>
                        <option value="12">Desember</option>
                    </select>

                    <select id="secondmonth" name="secondmonth">
                        <option value="1">Januari</option>
                        <option value="2">Februari</option>
                        <option value="3">Maret</option>
                        <option value="4">April</option>
                        <option value="5">Mei</option>
                        <option value="6">Juni</option>
                        <option value="7">Juli</option>
                        <option value="8">Agustus</option>
                        <option value="9">September</option>
                        <option value="10">Oktober</option>
                        <option value="11">November</option>
                        <option value="12">Desember</option>
                    </select>

                    <select id="year" name="year">
                        <option value="2015">2015</option>
                        <option value="2016">2016</option>
                    </select>

                    <input type="submit" value="Filter">

                </form>
            
                <?php
                    //filter bulan dan tahun berdasarkan input user
                    $filteryear = (isset($_POST['year']) ? $_POST['year'] : "2015");
                    $filtermonth1 = (isset($_POST['firstmonth']) ? $_POST['firstmonth'] : "1");
                    $filtermonth2 = (isset($_POST['secondmonth']) ? $_POST['secondmonth'] : "2"); ?>

                <div id="tabs-1">
                    
                    <!--<form action="index.php" method="POST">
                        <select id="firstmonth" name="firstmonth">
                            <option value="1">Januari</option>
                            <option value="2">Februari</option>
                            <option value="3">Maret</option>
                            <option value="4">April</option>
                            <option value="5">Mei</option>
                            <option value="6">Juni</option>
                            <option value="7">Juli</option>
                            <option value="8">Agustus</option>
                            <option value="9">September</option>
                            <option value="10">Oktober</option>
                            <option value="11">November</option>
                            <option value="12">Desember</option>
                        </select>

                        <select id="secondmonth" name="secondmonth">
                            <option value="1">Januari</option>
                            <option value="2">Februari</option>
                            <option value="3">Maret</option>
                            <option value="4">April</option>
                            <option value="5">Mei</option>
                            <option value="6">Juni</option>
                            <option value="7">Juli</option>
                            <option value="8">Agustus</option>
                            <option value="9">September</option>
                            <option value="10">Oktober</option>
                            <option value="11">November</option>
                            <option value="12">Desember</option>
                        </select>

                        <select id="year" name="year">
                            <option value="2015">2015</option>
                            <option value="2016">2016</option>
                        </select>

                        <input type="submit" value="Filter">

                    </form>-->
                    </br>                
                    <h2>Revenue Report Nasional</h2>
                    <?php
                        function growth($bulan1, $bulan2) {
                            $g=($bulan2/$bulan1)-1;
                            return $g;   
                        }
                        
                    ?>
                    <?php
                        //filter bulan dan tahun berdasarkan input user
                        //$filteryear = (isset($_POST['year']) ? $_POST['year'] : "2015");
                        //$filtermonth1 = (isset($_POST['firstmonth']) ? $_POST['firstmonth'] : "1");
                        //$filtermonth2 = (isset($_POST['secondmonth']) ? $_POST['secondmonth'] : "2");            
                    
                        //query untuk mendapatkan revenue berdasarkan input user
                        
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM revenue 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>   
                </div>

                <div id="tabs-2">                
                   
                    <!--<form action="index.php" method="POST">
                        <select id="firstmonth" name="firstmonth">
                            <option value="1">Januari</option>
                            <option value="2">Februari</option>
                            <option value="3">Maret</option>
                            <option value="4">April</option>
                            <option value="5">Mei</option>
                            <option value="6">Juni</option>
                            <option value="7">Juli</option>
                            <option value="8">Agustus</option>
                            <option value="9">September</option>
                            <option value="10">Oktober</option>
                            <option value="11">November</option>
                            <option value="12">Desember</option>
                        </select>

                        <select id="secondmonth" name="secondmonth">
                            <option value="1">Januari</option>
                            <option value="2">Februari</option>
                            <option value="3">Maret</option>
                            <option value="4">April</option>
                            <option value="5">Mei</option>
                            <option value="6">Juni</option>
                            <option value="7">Juli</option>
                            <option value="8">Agustus</option>
                            <option value="9">September</option>
                            <option value="10">Oktober</option>
                            <option value="11">November</option>
                            <option value="12">Desember</option>
                        </select>

                        <select id="year" name="year">
                            <option value="2015">2015</option>
                            <option value="2016">2016</option>
                        </select>

                        <input type="submit" value="Filter">
                    </form>-->
                    </br>                
                    <h2>Total CB Report Nasional</h2>
                    <?php
                        //filter bulan dan tahun berdasarkan input user
                        //$filteryear = (isset($_POST['year']) ? $_POST['year'] : "2015");
                        //$filtermonth1 = (isset($_POST['firstmonth']) ? $_POST['firstmonth'] : "1");
                        //$filtermonth2 = (isset($_POST['secondmonth']) ? $_POST['secondmonth'] : "2");            
                    
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM total_cb 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>   
                </div>

                <div id="tabs-3">                   
                    </br>                
                    <h2>Sales Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM sales 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>

                <div id="tabs-4">
                    </br>                
                    <h2>Churn Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM churn 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>

                <div id="tabs-5">
                    </br>                
                    <h2>Net Add Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM net_add 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>

                <div id="tabs-6">
                    </br>                
                    <h2>Data User Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM data_user 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>

                <div id="tabs-7">
                    </br>                
                    <h2>Smartphone User Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM smartphone_user 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>

                <div id="tabs-8">
                    </br>                
                    <h2>LTE Report Nasional</h2>
                    <?php         
                        //query untuk mendapatkan revenue berdasarkan input user
                        $query = sprintf("SELECT ROUND(nilai,2) as roundednilai,bulan,tahun,id_kategori FROM lte 
                            WHERE id_kategori=1 AND tahun='$filteryear' AND (bulan BETWEEN '$filtermonth1' AND '$filtermonth2')");

                         // Perform Query
                        $result = mysqli_query($con,$query);

                        // Check result
                        // This shows the actual query sent to MySQL, and the error. Useful for debugging.
                        if (!$result) {
                            $message  = 'Invalid query: ' . mysql_error() . "\n";
                            $message .= 'Whole query: ' . $query;
                            die($message);
                        }

                        // Use result
                        // Attempting to print $result won't allow access to information in the resource
                        // One of the mysql result functions must be used
                        // See also mysql_result(), mysql_fetch_array(), mysql_fetch_row(), etc.
                        while ($row = mysqli_fetch_assoc($result)) {
                            echo $row['id_kategori'];
                            echo " ";
                            echo $row['bulan']; 
                            echo " ";
                            echo $row['tahun'];
                            echo " ";
                            echo $row['roundednilai'];
                            echo'<br>';
                        }

                        // Free the resources associated with the result set
                        // This is done automatically at the end of the script
                        mysqli_free_result($result);
                    ?>                   
                </div>
            </div>
            
        </div>     
    </body>
</html>
  
