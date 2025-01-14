<?php
$project_name = 'InfixEdu';
function getStorageFile($file_name)
{
    $file = 'storage/app/.' . $file_name;
    if (file_exists($file)) {
        return file_get_contents($file);
    }
    return false;
}

?>
<!DOCTYPE html>
<html>

<head>
    <meta name="author" content="spondonit">
    <meta name="descripton" content="A project of spondonit">
    <title>Version | InfixEdu</title>
</head>

<body>
    <h1 style="text-align: center;">Your current version of <?php echo $project_name . ' is ' . getStorageFile('version') ?></h1>
</body>

</html>



<?php

if (isset($_GET['phpinfo'])) {
    phpinfo();
}
