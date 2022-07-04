# 字典格式化文本
中文文档 | [English](README.md)

各种开发语言的文本格式化.

## JavaScript
``` JavaScript
function dic_format(str, dic) {
    return str.replace(/\{([^{}]+)}/gi, function(match, Key) {
        if (dic[Key]) {
            return dic[Key];
        }
        return '';
    });
}

// 如何使用
let s_str = `你好, {name}!`;
let s_dic = {
    name: '莱德'
};
console.log(dic_format(s_str, s_dic));
// 输出 你好, 莱德!
```

## PHP
``` PHP
<?php
function dic_format($str, $dic) {
    $tf = preg_match_all('/\{([^{}]+)}/', $str, $MatObj, PREG_PATTERN_ORDER);
    if ($tf) {
        for ($i = 0; $i < count($MatObj[0]); $i++) {
            $Key = $MatObj[1][$i];
            $str = str_replace($MatObj[0][$i], $dic[$Key], $str); // 替换
        }
    }
    return $str; // 返回替换后的结果
}

// 用法
$s_str = '你好, {name}!';
$s_dic = array(
    'name' => '莱德'
);
var_dump(dic_format($s_str, $s_dic));
// 输出 string(15) "你好, 莱德!"
```

## C# 创建Common.cs文件, 贴入以下代码
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

## C# 使用 (框架为.net 6.0.6)
``` C#
using static Common.Common;
using Newtonsoft.Json.Linq;

string str = @"你好, {name}!";
JObject dic = new JObject()
{
    ["name"] = "莱德"
};

Console.WriteLine(Dic_format(str, dic));
// 控制台输出 你好, 莱德!
```