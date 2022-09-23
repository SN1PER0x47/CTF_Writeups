# ASCWG WEB Writeup
## Challenge Name: Behind Hood

## Level: Easy - 300 points
- Flag is in flag.php
- you got a link for page with the following source code:

```PHP
<?php  
if(!empty($_GET['url'])){

    $data= file_get_contents($_GET['url']) ?? null;

    echo "preg_match:".preg_match ('#[a-zA-Z0-9_-]{2,}#', $data);

    if (preg_match ('#[a-zA-Z0-9_-]{2,}#', $data)) {

        die("Try Again!!!!");

    }

    echo $data;

} else {

    highlight_file(__FILE__);

}
```

- the trick here is that the `preg_match` function is working on the data coming out of the specified file.
- `preg_match ('#[a-zA-Z0-9_-]{2,}#', $data)` : searching for any lower / upper case letters and numbers.
- **conclusion**: your payload must convert the data inside the specified file to something that does not match letters or numbers.
- payload: ?url=`php://filter/convert.iconv.utf-8.utf-16/resource=flag.php` 

