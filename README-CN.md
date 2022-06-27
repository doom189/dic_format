# 字典格式化文本
中文文档 | [English](README.md)

各种开发语言的文本格式化.

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

// 如何使用
let s_str = `你好, {name}!`;
let s_dic = {
    name: '莱德'
};
console.log(dic_format(s_str, s_dic));
// 输出 你好, 莱德!
```