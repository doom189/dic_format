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
// Console output "Hello, Ryder!"
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

## C# Crate "Common.cs" file, copy the following code
``` C#
using Newtonsoft.Json.Linq;
using System.Text.RegularExpressions;

namespace Common
{
    public static class Common
    {
        public static string Dic_format(string str, JObject dic)
        {
            Regex s_reg = new Regex(@"\{([^{}]+)}", RegexOptions.ECMAScript);

            if (s_reg.IsMatch(str))
            {
                MatchCollection matches = s_reg.Matches(str);
                foreach (Match match in matches)
                {
                    string key = match.Groups[1].Value;
                    str = str.Replace(match.Value, Convert.ToString(dic[key]));
                }
                return str;
            } else
            {
                return str;
            }
        }
    }
}
```

## C# use (frame is .net 6.0.6)
``` C#
using static Common.Common;
using Newtonsoft.Json.Linq;

string str = @"Hello, {name}!";
JObject dic = new JObject()
{
    ["name"] = "Ryder"
};

Console.WriteLine(Dic_format(str, dic));
// Console output "Hello, Ryder!"
```

## Python
``` Python
import re
def dic_format(s_str, s_dic):
    reg = re.compile(r'\{(?P<content>[^{} ]+)}', re.A)
    matchs = reg.finditer(s_str)
    for mat in matchs:
        key = mat[1]
        rep = mat[0]
        s_str = s_str.replace(rep, s_dic[key], 1)  # 替换一次
    return s_str


# use
s_str = 'Hello, {name}!'
s_dic = {
    'name': 'Ryder'
}
print(dic_format(s_str, s_dic))
# Console output "Hello, Ryder!"

```