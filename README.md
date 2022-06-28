# dic_format
English | [中文文档](README-CN.md)

Text formatting for various development languages.


## JavaScript
``` JavaScript
function dic_format(str, dic) {
    return str.replace(/\{([^{}]+)\}/gi, function(match, Key) {
        if (dic[Key]) {
            return dic[Key];
        }
        return '';
    });
}

// use
let s_str = `Hello, {name}!`;
let s_dic = {
    name: 'Ryder'
};
console.log(dic_format(s_str, s_dic));
// echo Hello, Ryder!
```


## PHP
``` PHP
<?php
function dic_format($str, $dic) {
    $tf = preg_match_all('/\{([^{}]+)}/', $str, $MatObj, PREG_PATTERN_ORDER);
    if ($tf) {
        for ($i = 0; $i < count($MatObj[0]); $i++) {
            $Key = $MatObj[1][$i];
            $str = str_replace($MatObj[0][$i], $dic[$Key], $str);
        }
    }
    return $str;
}

// use
$s_str = 'Hello, {name}!';
$s_dic = array(
    'name' => 'Ryder'
);
var_dump(dic_format($s_str, $s_dic));
// echo string(15) "Hello, Ryder!"
```