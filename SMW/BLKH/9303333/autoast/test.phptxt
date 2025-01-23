<?php

error_reporting(0);

echo '<b>Email Tester [Sending test].<b><br><br><form method="post">
<input type="text" placeholder="email" name="email" value="'.$_POST['email'].'">
<input type="text" placeholder="ID" name="orderid" value="'.$_POST['orderid'].'">
<input type="submit" value="Send">
</form>
<br>';

if (!empty($_POST['email'])) {
	if (!empty($_POST['email']) && trim($_POST['orderid']) != '') {
		$rand = trim($_POST['orderid']);
	} else {
		$rand = rand();
	}
	mail(trim($_POST['email']),$_SERVER['HTTP_HOST']." - Sending is Working Fine. [Result] ID: (".$rand.")"," [Sending test].");
	echo '<b>Send an report to ['.$_POST['email'].'] - ID: '.$rand.'</b>';
	echo '<!-- <id>'.$rand.'</id> -->';
}

?>
