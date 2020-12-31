# How-to-add-SMTP-relay-to-php-mail-function

This is an example, that how can you add SMTP relay in your php mail() function. There are some points you have note:

1. You have you use your own website webmail email id in "from".
2. You need add your your webmail email id username, password and host. You can use localhost as well in example.
3. $headers should be an array
4. You have install Mail throw PEAR in your CPanel.
5. Include Mail.php file and php folder path as example.




<?php
	ini_set("include_path", 'your php folder path:' . ini_get("include_path") );
	require_once "Mail.php";
						
	$message="Your Message.....";
	$from = "your name <mail@yourwebmal.com>";
	$to = name." <".abc@abc.com.">";
	$subject = "SMTP Mail Test";
						
	$username = "mail@yourwebmail.com";
	$password = "yourwebmail password";
	$host = "localhost";

	$headers = array ('From' => $from,'To' => $to,'Subject' => $subject);
						
	$smtp = Mail::factory('smtp',array ('host' => $host,'auth' => true,'socket_options' => array('ssl' => array('verify_peer_name' => false, 'allow_self_signed' => true)),'username' => $username,'password' => $password,'port' => '25'));
						
	$mail = $smtp->send($to, $headers, $message);
						
	if (PEAR::isError($mail))
	{
		echo "<p>Error Inside: " . $mail->getMessage() . "</p>";
	}
	else
	{
		echo "<p>Message successfully sent!</p>";
	}
?>
