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



---



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



- 将对象数据转换成数组

```php
/**
 * 将对象数据转换成数据
 * @param $object
 * @return array
 */
function objectToArray($object)
{
    if(!is_array($object) && !is_object($object)){
        return $object;
    }
    if( is_object($object) ){
        $object = get_object_vars($object);
    }
    return array_map('objectToArray',$object);
}

》》》
$data = ['name'=>'xing','age'=>20];
$obj = (object)$data;
objectToArray($obj)
>>> Array
(
    [name] => xing
    [age] => 20
)
```



- 数组中数据求和（支持多维数组）

```php
/**
 * 数组中数据的求和（支持多维数组）
 * @param array $array
 * @return int|mixed
 */
function arraySum(array $array)
{
    $total = 0;
    foreach(new RecursiveIteratorIterator( new RecursiveArrayIterator($array) ) as $num){
        $total += $num;
    }
    return $total;
}

》》》
$arr = [[11,22],33, [44,55,[66,77]]];
print_r(arraySum($arr));
>>> 308
```



- 将多维数组转化成一维数组（索引数组）

```php
function reduceArray($array) {
	    $return = [];
	    array_walk_recursive($array, function ($x) use (&$return) {
	        $return[] = $x;
	    });
	    return $return;
}
》》》
$data = [
    ['php','python','golang'],
    ['mysql','sqlite','mongodb','redis','Memcache']
];
print_r(reduceArray($data));
>>> Array
(
    [0] => php
    [1] => python
    [2] => golang
    [3] => mysql
    [4] => sqlite
    [5] => mongodb
    [6] => redis
    [7] => Memcache
)
```



- 生成一定数量的不重复的随机数

```php
/**
 * 生成一定数量的不重复随机数
 * @param  integer $min 最小值
 * @param  integer $max 最大值
 * @param  integer $num 随机数数量
 * @return array        返回值
 */
function generateUniqueRand(int $min, int $max,int $num)
{
    $count = 0;
    $return = [];
    if(($max-$min+1)<$num){
        return $return;
    }

    while ($count < $num) {
        $return[] = mt_rand($min, $max);
        $return   = array_flip(array_flip($return));
        $count    = count($return);
    }
    shuffle($return);
    return $return;
}

》》》
print_r(generateUniqueRand(1, 10, 10));
>>>Array
(
    [0] => 7
    [1] => 9
    [2] => 8
    [3] => 4
    [4] => 5
    [5] => 10
    [6] => 1
    [7] => 2
    [8] => 6
    [9] => 3
)
```



- 提取数组中字段数据

```php
/**
 * 过滤并获取有用数据
 * @param  array $data      原数据
 * @param  array $standard  保留的参数
 */
function filterData($data, array $standard){
    if(empty($data) || !is_array($data) || !is_array($standard)) return [];

    $standardArr = array_fill_keys($standard, '');

    $data = array_intersect_key($data,$standardArr);

    return array_merge($standardArr,$data);
}

》》》
$arr = ['name'=>'xing','age'=>23,'sex'=>1];
$standard = ['age'];


$ret = filterData($arr, $standard);
var_dump($ret);
>>> array(1) {
  'age' =>
  int(23)
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



- 过滤emoji表情特殊符号

```php
/**
 * 过滤emoji表情
 * $str 字符串
 */
function filterEmoji($str)  
{  
    $str = preg_replace_callback( 
    '/./u',
    function (array $match) {  
        return strlen($match[0]) >= 4 ? '' : $match[0];  
    },
    $str);  
  
  return $str;  
} 
```



- 获取数据库分表

```php
/**
 * 获取分表
 * @param  string  $tableSuffix 表前缀
 * @param  string  $code  字符串
 * @param  integer $size  表数量
 * @return string         表名
 */
function get_hash_table($tableSuffix,$code,$size=100)
{
    $hash = sprintf("%u", crc32($code));
    $hash1 = intval(fmod($hash, $size));
    return $tableSuffix."_".$hash1;
}
```





---



3. ### *************  验证类  *************

- 手机号验证

```php
/**
 * 验证手机号
 * 13[0-9],14[5,7],15[0,1,2,3,5,6,7,8,9],17[6,7,8],18[0-9],170[0-9]
 * 移动号段: 134,135,136,137,138,139,150,151,152,157,158,159,182,183,184,187,188,147,178,1705
 * 联通号段: 130,131,132,155,156,185,186,145,176,1709
 * 电信号段: 133,153,180,181,189,177,1700
 */
public function checkMobile($mobile)
{
    if(preg_match('/^1(3[0-9]|4[57]|5[0-35-9]|8[0-9]|7[0-9])\\d{8}$/', $mobile)){
        return 1;
    }
    elseif(preg_match('/(^1(3[4-9]|4[7]|5[0-27-9]|7[8]|8[2-478])\\d{8}$)|(^1705\\d{7}$)/', $mobile)){
        return 2;
    }
    elseif(preg_match('/(^1(3[0-2]|4[5]|5[56]|7[6]|8[56])\\d{8}$)|(^1709\\d{7}$)/', $mobile)){
        return 3;
    }
    elseif(preg_match('/(^1(33|53|77|8[019])\\d{8}$)|(^1700\\d{7}$)/', $mobile)){
        return 4;
    }else{
        return 0;
    }
}
```



- 验证时间是否正确和是否是零点

```php
/**
 * 验证日期与是否是整点
 * @param  string 日期
 * @param  bool   整点验证
 */
function validateDate($date,$isZero=false)
{
    $timestamp = strtotime($date);
    if(false === $timestamp){
        return false;
    }
    if($isZero){
        $today = strtotime('today');
        $interval = abs($timestamp - $today);
        if( !is_int($interval/(24*60*60) ) ){
            return false;
        }
    }
    return $timestamp;
}
```



- 判断是否在微信浏览器中

```php
// 判断是否是微信浏览器
function isWechat()
{
    return strpos($_SERVER['HTTP_USER_AGENT'], 'MicroMessenger') !== false;
}
```



- 判断PHP环境是否是cli

```php
// 判断PHP环境是否是cli
function isCli()
{
  return PHP_SAPI == 'cli';
}
```



- 判断当前环境是否是Windows

```php
function isWin()
{
  return strncasecmp(PHP_OS,'win',3) === 0;
}

function isWin()
{
  return strncasecmp(php_uname('s'),'win',3) === 0;
}

function isWin()
{
  return DIRECTORY_SEPARATOR === chr(92);
}

function isWin()
{
  return PATH_SEPARATOR === chr(59);
}

function isWin()
{
  return strcasecmp(PHP_SHLIB_SUFFIX,'dll') === 0;
}
```



- 判断数据是否为多维数组

```php
/**
 * 判断数据是否为多维数组
 * @param  Array $data    数据
 * @return Boolean         是/否
 */
function isMultidimensionalArray(Array $data)
{
  return count($data,1) === count($data);
}
```



- 判断字符串中是否存在中文字符

```php
function isExistChinese($char)
{
  return preg_match("/[\x{4e00}-\x{9fa5}]+/u",$char); // /([\x81-\xfe][\x40-\xfe])/
}
```



- 判断数据中是否有非法字符

```php
function illegalCharacters($strOrArr)
{
    $IllegalArr = [
      '"','\'','\\','\/','&','||','%','*','(',')',
      'select','update','delete','insert','create','modify',
    ];
    if(is_array($strOrArr)){
        foreach($strOrArr as $str){
            foreach($IllegalArr as $char){
                if(strpos(strtolower($str), $char) !== false){
                    return false;
                }
            }
        }
    }else{
        foreach($IllegalArr as $char){
            if(strpos(strtolower($strOrArr), $char) !== false){
                return false;
            }
        }
    }
    
    return true;
}
```



- 判断是否是GIF图

```php
function isGif($img)
{
  $handle = fopen($img,'rb');
    $img = fread($handle,'1024');
    fclose($handle);
    return strpos($img,chr(0x21).chr(0xff).chr(0x0b).'NETSCAPE2.0') !== FALSE;
}
```



- 判断Session是否开启

```php
function isActived()
{
  if( !isCli() ){
    if( version_compare(phpversion(), '5.4.0', '>=') ){
      return session_status() === PHP_SESSION_ACTIVE;
    }else{
      return !empty( session_id() );
    }
  }
  return false;
}
```



- 验证IP地址是否正确

```php
function checkIp( $ip ) 
{
    if ( empty( $ip ) )
        return false;

    if ( ! preg_match( '#^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$#', $ip ) ) {
        return false;
    }

    $ip_array = explode( '.', $ip );

    //真实的ip地址每个数字不能大于255（0-255）
    return ( $ip_array[0] <= 255 && $ip_array[1] <= 255 && $ip_array[2] <= 255 && $ip_array[3] <= 255 ) ? true : false;
}
```



- 验证是否是HTTPS协议

```php
function isHttps()
{
  return ( isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] == 'on' ) 
    || ( isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https' );
}
```



- 判断文件是否存在（本地+远程）

```php
function isExistFile($file)
{
  if($file){
    if(stripos($file,'http') === 0){
      $header = get_headers($file,1);
      return isset($header[0]) && ( strpos($header[0],'200') || strpos($header[0],'304') ) && stripos($header[0],'OK');
    }else{
      if( self::isExistChinese($file) ){
        $file = iconv('UTF-8', 'GBK', $file);
      }
      return file_exists($file);
    }
  }
  return false;
}
```



- 验证身份证号是否正确

```php
function isCreditNo($vStr)
{
    $vCity = array(
        '11','12','13','14','15','21','22',
        '23','31','32','33','34','35','36',
        '37','41','42','43','44','45','46',
        '50','51','52','53','54','61','62',
        '63','64','65','71','81','82','91'
    );
 
    if (!preg_match('/^([\d]{17}[xX\d]|[\d]{15})$/', $vStr)) return false;
 
    if (!in_array(substr($vStr, 0, 2), $vCity)) return false;
 
    $vStr = preg_replace('/[xX]$/i', 'a', $vStr);
    $vLength = strlen($vStr);
 
    if ($vLength == 18)
    {
        $vBirthday = substr($vStr, 6, 4) . '-' . substr($vStr, 10, 2) . '-' . substr($vStr, 12, 2);
    } else {
        $vBirthday = '19' . substr($vStr, 6, 2) . '-' . substr($vStr, 8, 2) . '-' . substr($vStr, 10, 2);
    }
 
    if (date('Y-m-d', strtotime($vBirthday)) != $vBirthday) return false;
    if ($vLength == 18)
    {
        $vSum = 0;
 
        for ($i = 17 ; $i >= 0 ; $i--)
        {
            $vSubStr = substr($vStr, 17 - $i, 1);
            $vSum += (pow(2, $i) % 11) * (($vSubStr == 'a') ? 10 : intval($vSubStr , 11));
        }
 
        if($vSum % 11 != 1) return false;
    }
 
    return true;
} 
```



- 验证参数类型

```php
/**
 * 参数验证(仅类型)
 * @param array      $para    数据
 * @param array      $standard  参数要求
 * @return boolen
 * 使用:
 *    Validate::verifyParams($data,[
            'REQUIRED' => [
                'username'    => 'string',
            ],
            'OPTIONAL' => [
                'ip'          => 'string',
            ],
        ]);
 */
function verifyParams($para, $standard)
{
    if ($para === false || empty($para)) {
        return false;
    }

    foreach ($standard['REQUIRED'] as $k => $v) {
        if (!array_key_exists($k, $para)) {
            return false;
        }
        if(empty($para[$k])){
            return false;
        }

        if ('string' == $v) {
            if (false === is_string($para[$k])) {
                return false;
            }
        } else if ('int' == $v) {
            if ((string)((int)($para[$k])) != $para[$k]) {
                return false;
            }
        } else {
            return false;
        }
    }

    foreach ($standard['OPTIONAL'] as $k => $v) {
        if (!array_key_exists($k, $para)) {
            continue;
        }

        if ('string' == $v) {
            if (!empty($para[$k]) && false === is_string($para[$k])) {
                return false;
            }
        } else if ('int' == $v) {
            if (!empty($para[$k]) && (string)((int)($para[$k])) != $para[$k]) {
                return false;
            }
        } else {
            return false;
        }
    }

    return true;
}
```



---



4. ### *************  数据导出类  *************

- 导出CSV格式数据

```php
/**
 * 导出CSV文件
 * @param  string 文件名称
 * @param  Array  数据头
 * @param  Array  数据体
 */
function exportCsv($fileName, $titleArr=[], $dataArr=[])
{
    ini_set('memory_limit','128M');
    ini_set('max_execution_time',0);
    ob_end_clean();
    ob_start();
    header("Content-Type: text/csv");
    header("Content-Disposition:filename=".$fileName);
    $fp=fopen('php://output','w');
    fwrite($fp, chr(0xEF).chr(0xBB).chr(0xBF));//防止乱码(比如微信昵称)
    fputcsv($fp,$titleArr);
    $index = 0;
    foreach ($dataArr as $item) {
        if($index==1000){
            $index=0;
            ob_flush();
            flush();
        }
        $index++;
        fputcsv($fp,$item);
    }

    ob_flush();
    flush();
    ob_end_clean();
}
```



- 导出CSV格式数据

```php
/**
 * 导出CSV格式数据
 * @param $fileName
 * @param array $titleArr
 * @param array $dataArr
 */
function exportCsv2($fileName, $titleArr=[], $dataArr=[])
{
    ini_set('memory_limit', '128M');
    ini_set('max_execution_time',0);

    $output = fopen($fileName, 'w');
    //add BOM to fix UTF-8 in Excel
    fputs($output, $bom =( chr(0xEF) . chr(0xBB) . chr(0xBF) ) );
    //告诉浏览器这个是一个csv文件  
    header("Content-Type: application/csv;charset=utf-8");
    header("Content-Disposition: attachment; filename={$fileName}");
    header('Cache-Control:must-revalidate,post-check=0,pre-check=0');
    header('Expires:0');
    header('Pragma:public');

    fputcsv($output, $titleArr); //输出表头    

    foreach ($dataArr as $v) { //输出每一行数据到文件中   
        fputcsv($output, array_values($v));
    }

    fclose($output);
}
```



5. ### *************  计算类  *************

- 浮点数求和

```php
/**
 * 浮点数求和（如果是减 就把参数前加 - 号）
 * @param array ...$params(5.6以上写法)
 * @return mixed 保留两位小数
 */
function add(...$params) {
    return array_reduce($params,function($base,$n){
        $base = bcadd($base,+$n,2);
        return $base;
    });
}

》》》
$ret1 = add(10.01, 20.22, 0.1);
print_r($ret1);
>>> 30.33

```



6. ### *************  时间日期类  *************

- 获取指定月份始末时间戳

```php
/**
 * 获取指定月份始末时间戳
 * @param  integer $year  年份
 * @param  integer $month 月份
 */
function getMonthTimestamps($year,$month)
{
    if( !checkdate($month, 1, $year) ){
        return false;
    }

    $start = mktime(0, 0, 0, $month, 1, $year);
    $end   = mktime(23, 59, 59, $month, date('t',$start), $year);
    return $start && $end ? [$start,$end] : false;
}
```



















