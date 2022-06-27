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