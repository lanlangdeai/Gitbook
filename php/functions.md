# 常用方法&函数





## 函数

- base_convert 在任意进制之间转换数字

```
详见：https://www.php.net/manual/zh/function.base-convert.php

base_convert ( string $number , int $frombase , int $tobase ) : string
返回一字符串，包含 number 以 tobase 进制的表示。number 本身的进制由 frombase 指定。frombase 和 tobase 都只能在 2 和 36 之间（包括 2 和 36）。高于十进制的数字用字母 a-z 表示，例如 a 表示 10，b 表示 11 以及 z 表示 35。

示例：
$hexadecimal = 'A37334';
echo base_convert($hexadecimal, 16, 2);

>>> 101000110111001100110100
```





## 方法



1. ### ************************** 数组 ******************

- 从二维数组中取出key

```php
/**
 * 从二维数组中取出自己要的KEY值(去除为空字符并根据结果排序)
 * @param  array $arrData
 * @param string $key
 * @param $im true 返回逗号分隔
 * @return array
 */
function filter_value($arrData, $key, $im = false)
{
    $re = [];
    foreach ($arrData as $k => $v) {
        if (isset($v[$key])) $re[] = $v[$key];
    }
    if (!empty($re)) {
        $re = array_flip(array_flip($re));
        sort($re);
    }

    return $im ? implode(',', $re) : $re;
}
```



- 多维数组合并（同样维度的数组合并）

```php
/**
 * 多维数组合并（支持多数组）
 * @return array
 */
function array_merge_multi()
{
    $args = func_get_args();
    $array = [];
    foreach ($args as $arg) {
        if (is_array($arg)) {
            foreach ($arg as $k => $v) {
                if (is_array($v)) {
                    $array[$k] = isset($array[$k]) ? $array[$k] : [];
                    $array[$k] = array_merge_multi($array[$k], $v);
                } else {
                    $array[$k] = $v;
                }
            }
        }
    }

    return $array;
}
```



2. ### *************  字符串  *************

- 格式化字节大小

```php
/**
 * 格式化字节大小
 * @param  number $size      字节数
 * @param  string $delimiter 数字和单位分隔符
 * @return string            格式化后的带单位的大小
 */
function format_bytes($size, $delimiter = '')
{
    $units = ['B', 'KB', 'MB', 'GB', 'TB', 'PB'];
    for ($i = 0; $size >= 1024 && $i < 5; $i++) $size /= 1024;

    return round($size, 2) . $delimiter . $units[$i];
}
```



- 生成一定长度的UUID

```php
/**
 * 生成一定长度的UUID
 *
 * @param int $length
 *
 * @return string
 */
function get_uuid($length = 16)
{
    mt_srand((double)microtime()*10000);
    $uuid = sprintf('%04X%04X-%04X-%04X-%04X-%04X%04X%04X', mt_rand(0, 65535), mt_rand(0, 65535), mt_rand(0, 65535), mt_rand(16384, 20479), mt_rand(32768, 49151), mt_rand(0, 65535), mt_rand(0, 65535), mt_rand(0, 65535));
    $str = base64_encode($uuid);
    return substr($str,  mt_rand(0, strlen($str) - $length), $length);
}
```







