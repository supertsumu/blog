---
title: "Secret Access"
date: 2022-12-28T18:07:47+08:00
---

[Home](/)

## Secret Access - 200 points - Web

Description:

You want the access? Give me the secret code!

Flag Format: picoCTF{}

Author: Shroomish

This web challenge comes with a zip file that contains the source code of the challenge. The goal is to bypass the security checks mentioned in the source code.
```php
<?php

if (isset($_POST['egg'])) {

    $secretHash = '00e39786989574093743872279278460';
   
    $eggWorthyStatus = false;

    // First, you need to show me that you are worthy.
    if (isset($_GET['eggSecret'])) {

        if (md5($_GET['eggSecret']) == $secretHash) {
            $eggWorthyStatus = true;
        } else {
            $eggWorthyStatus = false;
        }
    }

    $egg = $_POST['egg'];

    // Final check to make sure you are a true egg connoisseur
    if (preg_match("/^(.*?)+$/s", $egg)) {
        echo "Find me the egg please";
    } else {
        if ($eggWorthyStatus) {
            echo "You are a true egg connoisseur! Here is your egg flag: " . file_get_contents('flag.txt');
        } else {
            echo "Find me the egg please";
        }
    }
} else {
    echo "You're not even touching the egg...?!!!<br><br>";
    echo "Anyway, here's a picture of an egg <br><br><img src='img/togepi.gif'>";
}

?>
```

Flag: CYBERGRABS{3VERY_8YTE_4RE_REAL_VALUE}