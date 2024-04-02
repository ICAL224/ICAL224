<?php 

$include = true;
include_once 'inc/dbconn.php';
include_once 'inc/class.php';
include_once 'inc/imgitem.php';

$connectionInfo = array( "UID"      =>  $uid        ,
                         "PWD"      =>  $pwd        ,
                         "Database" =>  "RohanUser"
                       );

$oConn = sqlsrv_connect( $serverName, $connectionInfo);

$online_chk = 'SELECT COUNT(*) as online FROM RohanGame.dbo.TCharacterLogin where login = 1';
$req_c = sqlsrv_query($oConn, $online_chk);
$online = sqlsrv_fetch_array($req_c);

$account_chk = 'SELECT COUNT(*) as users from Rohanuser.dbo.tuser';
$req_us = sqlsrv_query($oConn, $account_chk);
$userc = sqlsrv_fetch_array($req_us);

$users = $userc['users'];
?>
<?php 
	session_start();
	if($_SESSION['user_t'] == ""){
		echo '<meta http-equiv="refresh" content="0;URL=/">';
	}else{
		$uidx = $_SESSION['user_t'];
		$get_user_info = "SELECT * FROM RohanUser.dbo.TUser where login_id = '$uidx'";
		$inf_exc = sqlsrv_query($oConn, $get_user_info);
		$userx = sqlsrv_fetch_array($inf_exc);

		$user_id = $userx['user_id'];
		$username = $userx['login_id'];
		$sess_date = $userx['session_date']->format('Y-m-d');
		$create_date = $userx['created_date']->format('Y-m-d');
		$point = $userx['points'];
		$IPV4 = $userx['REMOTE_ADDR'];
		$email = $userx['email'];
		$rps = $userx['points'];
		$fps = $userx['login_points'];
?>
<?php 
$include = true						;
include_once 'datasql.php'  ;
include './php/db.php';
include './php/class.php';
include './php/gender.php';
$include = false					;
ini_set("error_reporting","E_ALL & ~E_NoTICE");
//$_SESSION['UserID'] = 0;
session_start();
$idsx = $_SESSION['UserID'];
?>
<?php if ( !empty($errors) ) : ?>
	<?php foreach($errors as $error): ?> 
		<div class="alert">
	<span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span> 
	<?php echo $error; ?>
	</div>
	<?php endforeach; ?> 
	<?php endif; ?>

<!doctype html>
<html lang="en">

<!-- Head -->
<head>
    <!-- Page Meta Tags-->
    <meta charset="utf-8">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="">
    <meta name="author" content="">
    <meta name="keywords" content="">

    <!-- Favicon -->
    <link rel="apple-touch-icon" sizes="180x180" href="./assets/images/favicon/apple-touch-icon.png">
    <link rel="icon" type="image/png" sizes="32x32" href="./assets/images/favicon/favicon-32x32.png">
    <link rel="icon" type="image/png" sizes="16x16" href="./assets/images/favicon/favicon-16x16.png">
    <link rel="mask-icon" href="./assets/images/favicon/safari-pinned-tab.svg" color="#5bbad5">
    <meta name="msapplication-TileColor" content="#da532c">
    <meta name="theme-color" content="#ffffff">

    <!-- Google Font-->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Overpass:wght@200;300;400;600&display=swap" rel="stylesheet">

    <!-- Vendor CSS -->
    <link rel="stylesheet" href="./assets/css/libs.bundle.css" />

    <!-- Main CSS -->
    <link rel="stylesheet" href="./assets/css/theme.bundle.css" />

    <!-- Fix for custom scrollbar if JS is disabled-->
    <noscript>
        <style>
          /**
          * Reinstate scrolling for non-JS clients
          */
          .simplebar-content-wrapper {
            overflow: auto;
          }
        </style>
    </noscript>

    <!-- Page Title -->
    <title>Immortals | Rohan</title>
    
</head>
<body class="">

    <!-- Navbar-->
    <nav class="navbar navbar-expand-lg navbar-light border-0 py-0 fixed-top bg-dark-800">
      <div class="container-fluid">
        <div class="d-flex justify-content-between align-items-center flex-grow-1 navbar-actions">
    
          <!-- Menu Toggle-->
          <div class="menu-toggle cursor-pointer me-4 text-primary-hover transition-color disable-child-pointer">
            <i class="ri-menu-fold-line ri-lg fold align-middle" data-bs-toggle="tooltip" data-bs-placement="right"
              title="Close menu"></i>
            <i class="ri-menu-unfold-line ri-lg unfold align-middle" data-bs-toggle="tooltip" data-bs-placement="right"
              title="Open Menu"></i>
          </div>
          <!-- / Menu Toggle-->
    
          <!-- Navbar Actions-->
          <div class="d-flex align-items-center">
    
            <!-- Language-->
            <div class="dropdown me-2">
              <button class="btn-icon btn-hover-dark" type="button" id="language"
                data-bs-toggle="dropdown" aria-expanded="false">
                <i class="ri-global-line align-bottom text-body lh-1"></i>
              </button>
              <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="language">
                <li>
                  <a class="dropdown-item d-flex justify-content-between align-items-center" href="#">English 
                    <span class="text-muted ms-5">EN</span></a></li>
                <li><a class="dropdown-item d-flex justify-content-between align-items-center" href="#">French<span class="text-muted ms-5">FR</span></a></li>
                <li><a class="dropdown-item d-flex justify-content-between align-items-center" href="#">Espanol<span class="text-muted ms-5">ES</span></a></li>
                <li><a class="dropdown-item d-flex justify-content-between align-items-center" href="#">Turkish<span class="text-muted ms-5">TR</span></a></li>
                <li><a class="dropdown-item d-flex justify-content-between align-items-center" href="#">Russian<span class="text-muted ms-5">RU</span></a></li>
              </ul>
            </div>
            <!-- / Language-->
    
            <!-- Notifications-->
            <a class="btn-icon btn-hover-dark position-relative p-2 disable-child-pointer" data-bs-toggle="offcanvas" href="#offcanvasNotifications" role="button"
            aria-controls="offcanvasNotifications">
              <i class="ri-notification-fill align-bottom text-body lh-1"></i>
              <span class="badge bg-primary text-white position-absolute top-0 end-0">3</span>
            </a>
            <!-- / Notifications-->
    
          </div>
          <!-- / Navbar Actions-->
        
        </div>
      </div>
    </nav>    <!-- / Navbar-->

    <!-- Page Content -->
    <main id="main">

        <!-- Content-->
        <section class="container-fluid">

            <!-- Breadcrumbs-->
            <nav class="mb-4 pb-2 border-bottom" aria-label="breadcrumb">
                <ol class="breadcrumb">
                  <li class="breadcrumb-item"><a href="index.php"><i class="ri-home-line align-bottom me-1"></i> Dashboard</a></li>
                </ol>
                <ol class="breadcrumb">
                    <li class="breadcrumb-item"><a href="index.php">Home</a></li>
                    <li class="breadcrumb-item active">Downloads</li>
                </ol>
            </nav>            <!-- / Breadcrumbs-->

            <!-- Bottom Row Widgets-->
            <div class="row g-4 mb-4">

			<div class="col-12 col-md-15">
				<!-- Top Row Widgets-->
                    <div class="row">
                        <div class="card">
                            <div class="card-header">
                                <h5 class="card-title">Item Mall</h5>
<?php
error_reporting(0);
$errors = array(); 
if (!empty($_POST)){

	include("inject.php");
    $cRohanUser = sql_connect('RohanUser');
    $cRohanGame = sql_connect('RohanGame');

	include"priva.php";
	$bad_c = array("'", "\"", ";", "?", "@", "(", ")", "[" ,"]", "^", "!" ,"#", "%", "*" ,"`", "-", "+" ,"/" ,"=", "&", "$"," " ,"<" ,">");
	$val_c = array("", "", "", "", "", "", "", "" ,"", "", "" ,"", "", "" ,"", "", "", "", "", "", "","" ,"" ,"");

	$uidx = $_POST['uidx'];
	$idx = $_POST['idx'];
	$uidx_n = str_replace($bad_c,$val_c,$uidx);
	$idx_n = str_replace($bad_c,$val_c,$idx);
	$idx_count = strlen($idx_n);

	if($idx_count > 6){
		$errors[] = "Invalid action, please try again.";
	}else{
		$chk_idsame = "select * from rohango.dbo.item where id = $idx";
			$q_chk_idsame = sqlsrv_query($cRohanUser,$chk_idsame);
			$r_chk_idsame = sqlsrv_fetch_array($q_chk_idsame);

			$i_id = $r_chk_idsame['code_item'];
			$i_stack = $r_chk_idsame['jumlah'];
			$i_name = $r_chk_idsame['nama_item'];
			$price = $r_chk_idsame['harga_item'];

			$userpoint = "SELECT * FROM RohanUser.dbo.TUser where user_id = $uidx_n";
			$quserpoint = sqlsrv_query($oConn,$userpoint);
			$ruserpoint = sqlsrv_fetch_array($quserpoint);
			$urps = $ruserpoint['points'];
			if($urps > $price)
			{
				$sql = "INSERT INTO [RohanMall].[dbo].[TItem]
				([type]
				,[attr]
				,[stack]
				,[rank]
				,[equip_level]
				,[equip_strength]
				,[equip_dexterity]
				,[equip_intelligence]
				,[user_id]
				,[date]
				,[checkup])
		  VALUES
				($i_id
				,0x00
				,$i_stack
				,0
				,0
				,0
				,0
				,0
				,$uidx
				,GETDATE()
				,1)";
		
				sqlsrv_query($cRohanUser,$sql);

				$updrps = "UPDATE RohanUser.dbo.TUser set points = points - $price where user_id = $uidx_n";
				sqlsrv_query($cRohanUser,$updrps);
				echo ('<div class="alert alert-warning" role="alert">You have successfully purchase. '. $i_name .'</div>');
				//$errors[] = 'You have successfully purchase '. $i_name . '.';

			}else{
				echo ('<div class="alert alert-warning" role="alert">Insuficient RPs, please reload your account.</div>');
				//$errors[] = 'Insuficient RPs, please reload your account.';
			}	
	}
}
?>
                                <p class="text-muted mb-0">Your RPs. <img src="images/custom/img/ecoins.png"> <?php echo $rps;?></p>
                            </div><!--end card-header-->
                            <div class="card-body">
                                <div class="table-responsive">
                                    <table class="table table-bordered mb-0 table-centered">
                                        <thead>
                                            <tr>
                                                <td class="fw-bold">#</td>
                                                <td class="fw-bold">Item</td>
                                                <td class="fw-bold">Description</td>
                                                <td class="fw-bold">Cost</td>
                                                <td class="fw-bold">Purchase</td>
                                            </tr>
                                        </thead>
				<?php 
				$sql_list = "SELECT * FROM rohango.dbo.item WHERE type_item='etc'";
				$objQueryzlist = odbc_exec($connection, $sql_list);
				// $sql_log = odbc_do($connection,$sql_list);
				while($rsql_list = odbc_fetch_array($sql_log)){
					$code ="$rsql_list[id]";
					$stack = $rsql_list['jumlah'];
					$name = $rsql_list['nama_item'];
					$image = $rsql_list['gambar_item'];
					$desc = $rsql_list['desc'];
					$price = $rsql_list['harga_item'];
					$itemid = $rsql_list['code_item'];
					
				?>
                                        <tbody>
                                            <tr>
												<td><img src="images/custom/img/item/<?php echo $imgitem[$itemid];?>.png" alt="" width="70px" height="50px"></td>
                                                <td class=""><?php echo $name;?></td>
                                                <td class=""><?php echo $desc;?></td>
                                                <td class="text-success"><?php echo $price;?></span><img src="images/custom/img/ecoins.png" title="RPs"></td>
												<form method="post">					
												<input type="hidden" value="<?php echo $code; ?>" name="idx" id="idx">
												<input type="hidden" value="<?php echo $user_id; ?>" name="uidx" id="uidx">
												<input type="hidden" value="" name="recaptcha_response" id="recaptchaResponse">
												<td><button type="submit" class="button-style" value="Submit">Purchase</button></td>
												</form>
											</tr>
											<?php } ?> 
                                        </tbody>
                                    </table><!--end /table-->
                                </div><!--end /tableresponsive-->
                            </div><!--end card-body-->
                        </div>                      
                    </div>
				<!-- / Top Row Widgets-->
			</div>

            </div>
            <!-- Bottom Row Widgets-->

            <!-- Footer -->
            <footer class="  footer">
                <p class="small text-muted m-0">Copyright © 2023 Immortals Rohan</p>
                <p class="small text-muted m-0">Terms of Service | <a href="https://www.pixelrocket.store/">Privacy Policy</a></p>
            </footer>
            
            
            <!-- Sidebar Menu Overlay-->
            <div class="menu-overlay-bg"></div>
            <!-- / Sidebar Menu Overlay-->
            
            <!-- Modal Imports-->
            <!-- Place your modal imports here-->
            
            <!-- Default Example Modal Import-->
            <!-- Modal -->
            <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      Here goes modal body content
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                      <button type="button" class="btn btn-primary">Save changes</button>
                    </div>
                  </div>
                </div>
              </div>
            <!-- Offcanvas Imports-->
            <!-- Place your offcanvas imports here-->
            
            <!-- Default Example Offcanvas Import-->
            <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasExample" aria-labelledby="offcanvasExampleLabel">
                <div class="offcanvas-header">
                  <h5 class="offcanvas-title" id="offcanvasExampleLabel">Offcanvas</h5>
                  <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
                </div>
                <div class="offcanvas-body">
                  <div>
                    Some text as placeholder. In real life you can have the elements you have chosen. Like, text, images, lists, etc.
                  </div>
                  <div class="dropdown mt-3">
                    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-bs-toggle="dropdown">
                      Dropdown button
                    </button>
                    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                      <li><a class="dropdown-item" href="#">Action</a></li>
                      <li><a class="dropdown-item" href="#">Another action</a></li>
                      <li><a class="dropdown-item" href="#">Something else here</a></li>
                    </ul>
                  </div>
                </div>
            </div>
            <!-- Navbar Notifications offcanvas-->
            <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasNotifications"
              aria-labelledby="offcanvasNotificationsLabel">
              <div class="offcanvas-header">
                <h5 class="offcanvas-title" id="offcanvasNotificationsLabel">Notifications</h5>
                <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
              </div>
              <div class="offcanvas-body">
            
                <!-- Notification-->
                <div class="d-flex justify-content-start align-items-start p-3 rounded bg-light mb-3">
                  <div class="position-relative mt-1 ">
                    <picture class="avatar avatar-sm">
                      <img src="./assets/images/profile-small-2.jpeg"
                        alt="HTML Bootstrap Admin Template by Pixel Rocket">
                    </picture>
                    <span
                    class="dot bg-success avatar-dot border-light dot-sm"></span>
                  </div>
                  <div class="ms-4">
                    <p class="fw-bolder mb-1">John Jackson</p>
                    <p class="text-muted small mb-0">Just sent over regional sales. If you can let me know by the end...</p>
                    <span class="fs-xs fw-bolder text-muted text-uppercase">5 mins ago</span>
                  </div>
                </div>
                <!-- / Notification-->
            
                <!-- Notification-->
                <div class="d-flex justify-content-start align-items-start p-3 rounded bg-light mb-3">
                  <div class="position-relative mt-1 ">
                    <picture class="avatar avatar-sm">
                      <img src="./assets/images/profile-small-3.jpeg"
                        alt="HTML Bootstrap Admin Template by Pixel Rocket">
                    </picture>
                    <span
                    class="dot bg-success avatar-dot border-light dot-sm"></span>
                  </div>
                  <div class="ms-4">
                    <p class="fw-bolder mb-1">Peter Smith</p>
                    <p class="text-muted small mb-0">Hi Rob, can we setup a meeting for tomorrow around 2pm...</p>
                    <span class="fs-xs fw-bolder text-muted text-uppercase">30 mins ago</span>
                  </div>
                </div>
                <!-- / Notification-->
            
                <!-- Notification-->
                <div class="d-flex justify-content-start align-items-start p-3 rounded bg-light mb-3">
                  <div class="position-relative mt-1 ">
                    <picture class="avatar avatar-sm">
                      <img src="./assets/images/profile-small-4.jpeg"
                        alt="HTML Bootstrap Admin Template by Pixel Rocket">
                    </picture>
                    <span
                    class="dot bg-danger avatar-dot border-light dot-sm"></span>
                  </div>
                  <div class="ms-4">
                    <p class="fw-bolder mb-1">Helen Lewis</p>
                    <p class="text-muted small mb-0">Need to arrange for this year's Office lisences. Have to add two team licenses...</p>
                    <span class="fs-xs fw-bolder text-muted text-uppercase">43 mins ago</span>
                  </div>
                </div>
                <!-- / Notification-->
            
                <!-- View all Btn-->
                <a href="#" class="btn btn-outline-secondary w-100 mt-4" role="button">View all notifications</a>
                <!-- / View all btn-->
            
              </div>
            </div>            <!-- / Footer-->

        </section>
        <!-- / Content-->

    </main>
    <!-- /Page Content -->

    <!-- Page Aside-->
    <aside class="aside bg-dark-700">
    
        <div class="simplebar-wrapper">
            <div data-pixr-simplebar>
                <div class="pb-6 pb-sm-0 position-relative">
    
                    <!-- Mobile close btn-->
                    <div class="cursor-pointer close-menu me-4 text-primary-hover transition-color disable-child-pointer position-absolute end-0 top-0 mt-3 pt-1 d-xl-none">
                        <i class="ri-close-circle-line ri-lg align-middle me-n2"></i>
                    </div>
                    <!-- / Mobile close btn-->
    
                    <!-- Mobile Logo-->
                    <div class="d-flex justify-content-center align-items-center py-3">
                        <a class="m-0" href="index.php">
                            <div class="d-flex align-items-center justify-content-center">
							<span class="fw-bold fs-3 text-white">Immortals</span>
                            </div>                    </a>
                    </div>
                    <!-- / Mobile Logo-->
                    <ul class="list-unstyled mb-6 aside-menu">
    
                        <!-- Dashboard Menu Section-->
                        <li class="menu-section">Menu</li>
                        <li class="menu-item"><a href="#"><i class="ri-home-4-line me-3"></i>
                                <span>Home</span></a>
						</li>
                        <!-- / Dashboard Menu Section-->
    
                        <!-- UI Kit Menu Section-->
                        <li class="menu-item"><a href="#"><i class="ri-file-download-line me-3"></i>
                                <span>Downloads</span></a>
                        </li>
                        <!-- / UI Kit Menu Section-->
    
                        <!-- Pages Menu Section-->
                        <li class="menu-item"><a class="d-flex align-items-center collapsed menu-link" href="#"
                                data-bs-toggle="collapse" data-bs-target="#collapseMenuItemPages" aria-expanded="false"
                                aria-controls="collapseMenuItemPages"><i class="ri-list-check me-3"></i> <span>Info</span></a>
                            <div class="collapse" id="collapseMenuItemPages">
                                <ul class="nav-second-level">
                                    <li><a class="submenu-link" href="information.php">Information</a></li>
                                    <li><a class="submenu-link" href="#">Game Rules</a></li>
                                    <li><a class="submenu-link" href="#">Guides</a></li>
                                    <li><a class="submenu-link" href="#">Drop List</a></li>
                                </ul>
                            </div>
                        </li>
                        <!-- / Pages Menu Section-->
						
                        <!-- Rank Kit Menu Section-->
                        <li class="menu-item"><a href="ranking.php"><i class="ri-honor-of-kings-line me-3"></i>
                                <span>Ranking</span></a>
                        </li>
                        <!-- / Rank Kit Menu Section-->
						
                        <!-- Top Up Menu Section-->
                        <li class="menu-item"><a href="topup.php"><i class="ri-file-list-line me-3"></i>
                                <span>Top Up</span></a>
                        </li>
                        <!-- / Top Up Menu Section-->
						
						<!--  Auth Menu Section-->
                        <li class="menu-item"><a class="d-flex align-items-center collapsed menu-link" href="#"
                                data-bs-toggle="collapse" data-bs-target="#collapseMenuAuth" aria-expanded="false"
                                aria-controls="collapseMenuAuth"><i class="ri-rotate-lock-line me-3"></i>
                                <span>Authentication</span></a>
                            <div class="collapse" id="collapseMenuAuth">
                                <ul class="nav-second-level">
                                    <li><a class="submenu-link" href="auth-login.php">Login</a></li>
									<li><a class="submenu-link" href="auth-register.php">Register</a></li>
                                </ul>
                            </div>
						</li>
						<!-- / Auth Menu Section-->
                    </ul>
                </div>
            </div>
        </div>
    
    </aside>    <!-- / Page Aside-->

    <!-- Theme JS -->
    <!-- Vendor JS -->
    <script src="./assets/js/vendor.bundle.js"></script>
    
    <!-- Theme JS -->
    <script src="./assets/js/theme.bundle.js"></script>
</body>

</html>
	<?php } ?>
