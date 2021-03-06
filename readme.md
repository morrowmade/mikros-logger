## Mikros Logger

Mikros Logger is intended to serve as an off-site logger API for use in analytics and debugging.

## Logging information

Once deployed on server `example.com`, a POST request to `example.com/test` would create a *project* called
"test", and would immediately log basic request information such as IP address and timestamp as a *record*.

## Viewing log

In the previous example, visiting `example.com/test` in a web browser (i.e. a GET request) would display all records
submitted to that project thus far.

## PHP implementation example

```php
<?php
function mikrosLog($data = [], $project = 'testLog' ) {

    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_URL => "http://example.com/$project",
        CURLOPT_POST => 1,
        CURLOPT_POSTFIELDS => [
            'data' => json_encode($data)
        ]
    ));
    curl_exec($ch);
    curl_close($ch);
}

mikrosLog(['User has created a new item', $user->id]);
```