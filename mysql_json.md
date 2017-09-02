# JSON in MySQL >= 5.7.8
https://scotch.io/tutorials/working-with-json-in-mysql

### Create:
**JSON_OBJECT** function accepts a list of key/value pairs in the form JSON_OBJECT(key1, value1, key2, value2, ... key(n), value(n)) and returns a JSON object. When key is repeated, only first is added
JSON_ARRAY function which returns a JSON array when passed a set of values.
```
// create data
INSERT INTO `e_store`.`products`(
    `name` ,
    `brand_id` ,
    `category_id` ,
    `attributes`
)
VALUES(
    'Desire' ,
    '2' ,
    '2' ,
    JSON_OBJECT(
        "network" ,
        JSON_ARRAY("GSM" , "CDMA" , "HSPA" , "EVDO") ,
        "body" ,
        "5.11 x 2.59 x 0.46 inches" ,
        "weight" ,
        "143 grams" ,
        "sim" ,
        "Micro-SIM" ,
        "display" ,
        "4.5 inches" ,
        "resolution" ,
        "720 x 1280 pixels" ,
        "os" ,
        "Android Jellybean v4.3"
    )
);
```

**JSON_MERGE** function takes multiple JSON objects and produces a single, aggregate object. When key is repeated, everything merge together
```
INSERT INTO `e_store`.`products`(
    `name` ,
    `brand_id` ,
    `category_id` ,
    `attributes`
)
VALUES(
    'Explorer' ,
    '3' ,
    '3' ,
    JSON_MERGE(
        '{"sensor_type": "CMOS"}' ,
        '{"processor": "Digic DV III"}' ,
        '{"scanning_system": "progressive"}' ,
        '{"mount_type": "PL"}' ,
        '{"monitor_type": "LCD"}'
    )
);
```		

### Read:
**JSON_EXTRACT** or arrow function (i.e. `attributes` -> '$.ports.usb' > 0)
```
//retrieve using particular attribute in json
SELECT
    **
FROM
    `e_store`.`products`
WHERE
    `category_id` = 1
AND JSON_EXTRACT(`attributes` , '$.ports.usb') > 0
AND JSON_EXTRACT(`attributes` , '$.ports.hdmi') > 0;
```

**JSON_EXTRACT** function has the alias -> that you can use to make your queries more readable.
```
SELECT
    **
FROM
    `e_store`.`products`
WHERE
    `category_id` = 1
AND `attributes` -> '$.ports.usb' > 0
AND `attributes` -> '$.ports.hdmi' > 0;
```

### Update:
**JSON_INSERT** function will only add the property to the object if it does not exists already.
```
//add chipset
UPDATE `e_store`.`products`
SET `attributes` = JSON_INSERT(
    `attributes` ,
    '$.chipset' ,
    'Qualcomm'
)
WHERE
    `category_id` = 2;
```

**JSON_REPLACE** function substitutes the property only if it is found.
```
//replace chipset value
UPDATE `e_store`.`products`
SET `attributes` = JSON_REPLACE(
    `attributes` ,
    '$.chipset' ,
    'Qualcomm Snapdragon'
)
WHERE
    `category_id` = 2;
```

**JSON_SET** function will add the property if it is not found else replace it.
```
//add or replace
UPDATE `e_store`.`products`
SET `attributes` = JSON_SET(
    `attributes` ,
    '$.body_color' ,
    'red'
)
WHERE
    `category_id` = 1;
```


### Delete:
**JSON_REMOVE** function which returns the updated JSON after removing the specified key based on the path expression.
```
//delete a certain key/value from your JSON columns
UPDATE `e_store`.`products`
SET `attributes` = JSON_REMOVE(`attributes` , '$.mount_type')
WHERE
    `category_id` = 3;

//delete rows using a JSON column
DELETE FROM `e_store`.`products`
WHERE `category_id` = 2
AND JSON_EXTRACT(`attributes` , '$.os') LIKE '%Jellybean%';
```
