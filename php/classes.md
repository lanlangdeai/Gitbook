# 常用类



## 1. ===============  自封装  ===============



- ####  获取客户端代理信息



```php
<?php


//------------------------
// 根据user-agent获取浏览器版本，操作系统
//-------------------------

class Agent
{
    /**
     * 获取客户端浏览器信息 添加win10 edge浏览器判断
     * @param  null
     * @author  Jea杨
     * @return string
     */
    public static function getBroswer()
    {
        $sys = $_SERVER['HTTP_USER_AGENT'];  //获取用户代理字符串
        if (stripos($sys, "Firefox/") > 0) {
            preg_match("/Firefox\/([^;)]+)+/i", $sys, $b);
            $exp[0] = "Firefox";
            $exp[1] = $b[1];  //获取火狐浏览器的版本号
        } elseif (stripos($sys, "Maxthon") > 0) {
            preg_match("/Maxthon\/([\d\.]+)/", $sys, $aoyou);
            $exp[0] = "傲游";
            $exp[1] = $aoyou[1];
        } elseif (stripos($sys, "MSIE") > 0) {
            preg_match("/MSIE\s+([^;)]+)+/i", $sys, $ie);
            $exp[0] = "IE";
            $exp[1] = $ie[1];  //获取IE的版本号
        } elseif (stripos($sys, "OPR") > 0) {
            preg_match("/OPR\/([\d\.]+)/", $sys, $opera);
            $exp[0] = "Opera";
            $exp[1] = $opera[1];
        } elseif (stripos($sys, "Edge") > 0) {
            //win10 Edge浏览器 添加了chrome内核标记 在判断Chrome之前匹配
            preg_match("/Edge\/([\d\.]+)/", $sys, $Edge);
            $exp[0] = "Edge";
            $exp[1] = $Edge[1];
        } elseif (stripos($sys, "Chrome") > 0) {
            preg_match("/Chrome\/([\d\.]+)/", $sys, $google);
            $exp[0] = "Chrome";
            $exp[1] = $google[1];  //获取google chrome的版本号
        } elseif (stripos($sys, 'rv:') > 0 && stripos($sys, 'Gecko') > 0) {
            preg_match("/rv:([\d\.]+)/", $sys, $IE);
            $exp[0] = "IE";
            $exp[1] = $IE[1];
        } elseif (stripos($sys, 'Safari') > 0) {
            preg_match("/safari\/([^\s]+)/i", $sys, $safari);
            $exp[0] = "Safari";
            $exp[1] = $safari[1];
        } else {
            $exp[0] = "未知浏览器";
            $exp[1] = "";
        }
        return $exp[0] . '(' . $exp[1] . ')';
    }

    /**
     * 获取客户端操作系统信息包括win10
     */
    public static function getOs()
    {
        $agent = $_SERVER['HTTP_USER_AGENT'];

        if (preg_match('/win/i', $agent) && strpos($agent, '95')) {
            $os = 'Windows 95';
        } else if (preg_match('/win 9x/i', $agent) && strpos($agent, '4.90')) {
            $os = 'Windows ME';
        } else if (preg_match('/win/i', $agent) && preg_match('/98/i', $agent)) {
            $os = 'Windows 98';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 6.0/i', $agent)) {
            $os = 'Windows Vista';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 6.1/i', $agent)) {
            $os = 'Windows 7';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 6.2/i', $agent)) {
            $os = 'Windows 8';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 10.0/i', $agent)) {
            $os = 'Windows 10';#添加win10判断
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 5.1/i', $agent)) {
            $os = 'Windows XP';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt 5/i', $agent)) {
            $os = 'Windows 2000';
        } else if (preg_match('/win/i', $agent) && preg_match('/nt/i', $agent)) {
            $os = 'Windows NT';
        } else if (preg_match('/win/i', $agent) && preg_match('/32/i', $agent)) {
            $os = 'Windows 32';
        } else if (preg_match('/linux/i', $agent)) {
            $os = 'Linux';
        } else if (preg_match('/unix/i', $agent)) {
            $os = 'Unix';
        } else if (preg_match('/sun/i', $agent) && preg_match('/os/i', $agent)) {
            $os = 'SunOS';
        } else if (preg_match('/ibm/i', $agent) && preg_match('/os/i', $agent)) {
            $os = 'IBM OS/2';
        } else if (preg_match('/Mac/i', $agent)) {
            $os = 'Mac';
        } else if (preg_match('/PowerPC/i', $agent)) {
            $os = 'PowerPC';
        } else if (preg_match('/AIX/i', $agent)) {
            $os = 'AIX';
        } else if (preg_match('/HPUX/i', $agent)) {
            $os = 'HPUX';
        } else if (preg_match('/NetBSD/i', $agent)) {
            $os = 'NetBSD';
        } else if (preg_match('/BSD/i', $agent)) {
            $os = 'BSD';
        } else if (preg_match('/OSF1/i', $agent)) {
            $os = 'OSF1';
        } else if (preg_match('/IRIX/i', $agent)) {
            $os = 'IRIX';
        } else if (preg_match('/FreeBSD/i', $agent)) {
            $os = 'FreeBSD';
        } else if (preg_match('/teleport/i', $agent)) {
            $os = 'teleport';
        } else if (preg_match('/flashget/i', $agent)) {
            $os = 'flashget';
        } else if (preg_match('/webzip/i', $agent)) {
            $os = 'webzip';
        } else if (preg_match('/offline/i', $agent)) {
            $os = 'offline';
        } elseif (preg_match('/ucweb|MQQBrowser|J2ME|IUC|3GW100|LG-MMS|i60|Motorola|MAUI|m9|ME860|maui|C8500|gt|k-touch|X8|htc|GT-S5660|UNTRUSTED|SCH|tianyu|lenovo|SAMSUNG/i', $agent)) {
            $os = 'mobile';
        } else {
            $os = '未知操作系统';
        }
        return $os;
    }
}

```



- ### 文件处理（上传/下载）

```php
<?php

//------------------------
// 文件下载和图片下载
//-------------------------

class File
{
    /**
     * 文件下载
     * @param $file_path
     * @param string $file_name
     * @param string $file_size
     * @param string $ext
     */
    public static function download($file_path, $file_name = '', $file_size = '', $ext = '')
    {
        if (!$file_name) {
            $file_name = basename($file_path);
        }
        if (!$file_size && in_array(substr($file_path, 0, 1), [".", "/"])) {
            try {
                $file_size = filesize($file_path);
            } catch (\Exception $e) {
//                return $e->getMessage();
                return "文件不存在";
            }
        }
        if (!$ext) {
            $ext = pathinfo($file_path, PATHINFO_EXTENSION);
        }
        if ($ext && !strpos($file_name, ".")) {
            $file_name = $file_name . "." . $ext;
        }
        $content_type = self::getMime($ext);

        header("Cache-Control:");
        header("Cache-Control: public");

        // 文件类型
        header("Content-type: {$content_type}");

        // 处理中文文件名
        $ua = $_SERVER["HTTP_USER_AGENT"];
        if (preg_match("/MSIE/", $ua)) {
            $encoded_filename = rawurlencode($file_name);
            header('Content-Disposition: attachment; filename="' . $encoded_filename . '"');
        } else if (preg_match("/Firefox/", $ua)) {
            header("Content-Disposition: attachment; filename*=\"utf8''" . $file_name . '"');
        } else {
            header('Content-Disposition: attachment; filename="' . $file_name . '"');
        }
        // 文件大小
        if ($file_size) {
            header("Accept-Length: ". $file_size);
            header("Content-Length: " . $file_size);
        }
        readfile($file_path);
    }

    /**
     * 功能：php多种方式完美实现下载远程图片保存到本地
     * 参数：文件url,保存文件名称，使用的下载方式
     * 当保存文件名称为空时则使用远程文件原来的名称
     * @param string $url      请求图片的链接
     * @param string $filename 保存的文件名
     * @param int $type        保存图片的类型 0为curl,适用于静态图片,其他为缓冲缓存,适用于动态图片
     * @return string $filename 返回保存的文件名
     */
    public static function downloadImage($url, $filename, $type = 0)
    {
        if ($url == '') {
            return false;
        }
        $ext = pathinfo($filename, PATHINFO_EXTENSION);
        if (!in_array($ext, ['jpg', 'jpeg', 'png', 'gif', 'bmp', 'ico', 'tif', 'tiff'])) {
            $ext = pathinfo($url, PATHINFO_EXTENSION);
            if (!in_array($ext, ['jpg', 'jpeg', 'png', 'gif', 'bmp', 'ico', 'tif', 'tiff'])) {
                $ext = 'jpg';
            }
            $filename = $filename . "." . $ext;
        }

        //下载文件流
        if ($type) {
            $ch = curl_init();
            $timeout = 5;
            curl_setopt($ch, CURLOPT_URL, $url);
            curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
            curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, $timeout);
            $img = curl_exec($ch);
            curl_close($ch);
        } else {
            ob_start();
            readfile($url);
            $img = ob_get_contents();
            ob_end_clean();
        }

        //保存文件
//        try {
            $fp2 = fopen($filename, 'w');
            fwrite($fp2, $img);
            fclose($fp2);
            return $filename;
        /*} catch (\think\Exception $e) {
            //TODO 异常处理
            return false;
        }*/
    }

    /**
     * 获取文件Mime
     * @param string $ext
     * @return string
     */
    public static function getMime($ext)
    {
        $mimes = [
            'xml'   => 'text/xml',
            'json'  => 'application/json',
            'js'    => 'text/javascript',
            'php'   => 'application/octet-stream',
            'css'   => 'text/css',
            'html'  => 'text/html',
            'htm'   => 'text/html',
            'xhtml' => 'text/html',
            'rss'   => 'application/rss+xml',
            'yaml'  => 'application/x-yaml',
            'atom'  => 'application/atom+xml',
            'pdf'   => 'application/pdf',
            'text'  => 'text/plain',
            'png'   => 'image/png',
            'jpg'   => 'image/jpeg',
            'gif'   => 'image/gif',
            'csv'   => 'text/csv',
            'tif'   => 'image/tiff',
            'ai'    => 'application/postscript',
            'asp'   => 'text/asp',
            'au'    => 'audio/basic',
            'avi'   => 'video/avi',
            'rmvb'  => 'application/vnd.rn-realmedia-vbr',
            '3gp'   => 'application/octet-stream',
            'flv'   => 'application/octet-stream',
            'mp3'   => 'audio/mpeg',
            'wav'   => 'audio/wav',
            'sql'   => 'application/octet-stream',
            'rar'   => 'application/octet-stream',
            'zip'   => 'application/zip',
            '7z'    => 'application/octet-stream',
            'bmp'   => 'application/x-bmp',
            'cdr'   => 'application/x-cdr',
            'class' => 'java/*',
            'exe'   => 'application/x-msdownload',
            'fax'   => 'image/fax',
            'icb'   => 'application/x-icb',
            'ico'   => 'image/x-icon',
            'java'  => 'java/*',
            'jfif'  => 'image/jpeg',
            'jpeg'  => 'image/jpeg',
            'jsp'   => 'text/html',
            'mp4'   => 'video/mpeg4',
            'mpa'   => 'video/x-mpg',
            'mpeg'  => 'video/mpg',
            'mpg'   => 'video/mpg',
            'mpga'  => 'audio/rn-mpeg',
            'ras'   => 'application/x-ras',
            'tiff'  => 'image/tiff',
            'txt'   => 'text/plain',
            'wax'   => 'audio/x-ms-wax',
            'wm'    => 'video/x-ms-wm',
            'apk'   => 'application/vnd.android.package-archive',
            'doc'   => 'application/msword',
            'dot'   => 'application/msword',
            'docx'  => 'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
            'dotx'  => 'application/vnd.openxmlformats-officedocument.wordprocessingml.template',
            'docm'  => 'application/vnd.ms-word.document.macroEnabled.12',
            'dotm'  => 'application/vnd.ms-word.template.macroEnabled.12',
            'xls'   => 'application/vnd.ms-excel',
            'xlt'   => 'application/vnd.ms-excel',
            'xla'   => 'application/vnd.ms-excel',
            'xlsx'  => 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
            'xltx'  => 'application/vnd.openxmlformats-officedocument.spreadsheetml.template',
            'xlsm'  => 'application/vnd.ms-excel.sheet.macroEnabled.12',
            'xltm'  => 'application/vnd.ms-excel.template.macroEnabled.12',
            'xlam'  => 'application/vnd.ms-excel.addin.macroEnabled.12',
            'xlsb'  => 'application/vnd.ms-excel.sheet.binary.macroEnabled.12',
            'ppt'   => 'application/vnd.ms-powerpoint',
            'pot'   => 'application/vnd.ms-powerpoint',
            'pps'   => 'application/vnd.ms-powerpoint',
            'ppa'   => 'application/vnd.ms-powerpoint',
            'pptx'  => 'application/vnd.openxmlformats-officedocument.presentationml.presentation',
            'potx'  => 'application/vnd.openxmlformats-officedocument.presentationml.template',
            'ppsx'  => 'application/vnd.openxmlformats-officedocument.presentationml.slideshow',
            'ppam'  => 'application/vnd.ms-powerpoint.addin.macroEnabled.12',
            'pptm'  => 'application/vnd.ms-powerpoint.presentation.macroEnabled.12',
            'potm'  => 'application/vnd.ms-powerpoint.template.macroEnabled.12',
            'ppsm'  => 'application/vnd.ms-powerpoint.slideshow.macroEnabled.12',
        ];
        return isset($mimes[$ext]) ? $mimes[$ext] : 'application/octet-stream';
    }
}

```



- ### 字符串加解密

```php
class Encrypt
{
	/**
     * 加密
     * @param  string  $str    需加密字符串
     * @param  integer $factor 分类
     * @return string          加密之后的字符串
     */
    static function  doEncode(string $str , int $factor = 0){
        $len = strlen($str);
        if(!$len){
            return;
        }
        if($factor  === 0){
            $factor = mt_rand(1, min(255 , ceil($len / 3)));
        }
        $c = $factor % 8;

        $slice = str_split($str ,$factor);
        for($i=0;$i < count($slice);$i++){
            for($j=0;$j< strlen($slice[$i]) ;$j ++){
                $slice[$i][$j] = chr(ord($slice[$i][$j]) + $c + $i);
            }
        }
        $ret = pack('C' , $factor).implode('' , $slice);
        return self::base64URLEncode($ret);
    }

    /**
     * 解密
     * @param  string $str 需解密字符串
     * @return string      解密之后的字符串
     */
    static function doDecode($str)
    {  
        if($str == ''){
            return;
        }     
        $str = self::base64URLDecode($str);
        $factor =  ord(substr($str , 0 ,1));
        $c = $factor % 8;
        $entity = substr($str , 1); 
        $slice = str_split($entity , $factor);
        if(!$slice){
            return false;
        }
        for($i=0;$i < count($slice); $i++){
            for($j =0 ; $j < strlen($slice[$i]); $j++){
                $slice[$i][$j] = chr(ord($slice[$i][$j]) - $c - $i );
            }
        }
        return implode($slice);
    }

    static function base64URLEncode($data) 
    {
        return rtrim(strtr(base64_encode($data), '+/', '-_'), '=');
    }

    static function base64URLDecode($data) 
    {
        return base64_decode(str_pad(strtr($data, '-_', '+/'), strlen($data) % 4, '=', STR_PAD_RIGHT));
    }
}
```



- ### 字符串加解密2

```php
class EncryptAndDecrypt
{

    /**
     * 加解密算法
     * @param  string $string 加密数据
     * @param  string $rand   加密随机字符串
     * @param  string $action 加解密方式标识
     * @return string         加解密之后数据
     */
    public static function mymd5($string, $rand='randstring', $action="EN")
    {
        $secret_string = $rand.'5*a,.^&;?.%#@!';

        if($string=="")
            return "";
        if($action=="EN"){
            $md5code=substr(md5($string),8,10);
        }else{
            $md5code=substr($string,-10);
            $string=substr($string,0,strlen($string)-10);
        }
        //$key = md5($md5code.$_SERVER["HTTP_USER_AGENT"].$secret_string);
        $key = md5($md5code.$secret_string);
        $string = ($action=="EN" ? $string : base64_decode($string));
        $len = strlen($key);
        $code = "";
        for($i=0; $i<strlen($string); $i++){
            $k = $i%$len;
            $code .= $string[$i]^$key[$k];
        }
        $code = $action == "DE" ? (substr(md5($code),8,10) == $md5code ? $code : NULL) : base64_encode($code)."$md5code";

        return $code;
    }

    // base64_encode
    public static function b64encode( $string ) {
        $data = base64_encode( $string );
        $data = str_replace( array ( '+' , '/' , '=' ), array ( '-' , '_' , '' ), $data );
        return $data;
    }
    // base64_decode
    public static function b64decode( $string ) {
        $data = str_replace( array ( '-' , '_' ), array ( '+' , '/' ), $string );
        $mod4 = strlen( $data ) % 4;
        if ( $mod4 ) {
            $data .= substr( '====', $mod4 );
        }
        return base64_decode( $data );
    }

}
```



---



## 2.=====================  基于第三方库  ==================== 



- PHPExcel（https://github.com/PHPOffice/PHPExcel）

```php
<?php
require_once './PHPExcel/IOFactory.php';

class Excel
{
    /**
     * 一键导 出Excel
     * @param array $header       Excel 头部 ["COL1","COL2","COL3",...]
     * @param array $body         和头部长度相等字段查询出的数据就可以直接导出
     * @param null|string $name   文件名，不包含扩展名，为空默认为当前时间
     * @param string|int $version Excel版本 2003|2007
     * @return string
     */
    public static function export($head, $body, $name = null, $version = '2007')
    {
        try {
            // 输出 Excel 文件头
            $name = empty($name) ? date('YmdHis') : $name;

            $objPHPExcel = new \PHPExcel();
            $sheetPHPExcel = $objPHPExcel->setActiveSheetIndex(0);
            $char_index = range("A", "Z");

            // Excel 表格头
            foreach ($head as $key => $val) {
                $sheetPHPExcel->setCellValue("{$char_index[$key]}1", $val);
            }

            // Excel body 部分
            foreach ($body as $key => $val) {
                $row = $key + 2;
                $col = 0;
                foreach ($val as $k => $v) {
                    $sheetPHPExcel->setCellValue("{$char_index[$col]}{$row}", $v);
                    $col++;
                }
            }

            // 版本差异信息
            $version_opt = [
                '2007' => [
                    'mime'       => 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
                    'ext'        => '.xlsx',
                    'write_type' => 'Excel2007',
                ],
                '2003' => ['mime'       => 'application/vnd.ms-excel',
                           'ext'        => '.xls',
                           'write_type' => 'Excel5',
                ],
                'pdf'  => ['mime'       => 'application/pdf',
                           'ext'        => '.pdf',
                           'write_type' => 'PDF',
                ],
                'ods'  => ['mime'       => 'application/vnd.oasis.opendocument.spreadsheet',
                           'ext'        => '.ods',
                           'write_type' => 'OpenDocument',
                ],
            ];

            header('Content-Type: ' . $version_opt[$version]['mime']);
            header('Content-Disposition: attachment;filename="' . $name . $version_opt[$version]['ext'] . '"');
            header('Cache-Control: max-age=0');
            // If you're serving to IE 9, then the following may be needed
            header('Cache-Control: max-age=1');

            // If you're serving to IE over SSL, then the following may be needed
            header('Expires: Mon, 26 Jul 1997 05:00:00 GMT'); // Date in the past
            header('Last-Modified: ' . gmdate('D, d M Y H:i:s') . ' GMT'); // always modified
            header('Cache-Control: cache, must-revalidate'); // HTTP/1.1
            header('Pragma: public'); // HTTP/1.0

            $objWriter = PHPExcel_IOFactory::createWriter($objPHPExcel, $version_opt[$version]['write_type']);
            $objWriter->save('php://output');
        } catch (Exception $e) {
            return $e->getMessage();
        }
    }

    /**
     * 解析 Excel 数据并写入到数据库
     * @param string $file Excel 路径名文件名
     * @param array $header 表头对应字段信息 ['A'=>'field1', 'B'=>'field2', ...]
     * @param int $perLimit 每次一次性写入数据库中的行数
     * @param mixed $insertFunc 写入数据库的回调函数，可以用匿名函数
     * @param string $type Excel2007|Excel5
     * @return int
     */
    public static function parse($file, $header, $perLimit, $insertFunc, $type = '')
    {
        $type = self::getType($file, $type);
        $objReader = PHPExcel_IOFactory::createReader($type);
        $objPHPExcel = $objReader->load($file);
        // 数据数组
        $data = [];
        // 已导入数据计数
        $count = 0;
        // 跳过第一行
        foreach ($objPHPExcel->getSheet()->getRowIterator(2) as $row) {
            // 逐个单元格读取，减少内存消耗
            $cellIterator = $row->getCellIterator();
            // 不跳过空值
            $cellIterator->setIterateOnlyExistingCells();
            // 只读取显示的行、列，跳过隐藏行、列
            if ($objPHPExcel->getActiveSheet()->getRowDimension($row->getRowIndex())->getVisible()) {
                $rowData = [];
                foreach ($cellIterator as $cell) {
                    if ($objPHPExcel->getActiveSheet()->getColumnDimension($cell->getColumn())->getVisible()) {
                        if (isset($header[$cell->getColumn()])) {
                            $rowData[$header[$cell->getColumn()]] = $cell->getValue();
                        }
                    }
                }
                $data[] = $rowData;
                $count++;
                // 数据分批写入数据库，防止一条SQL太长数据库不支持
                if ($count && $count % $perLimit == 0) {
                    $insertFunc($data);
                    // 清空已有数据
                    $data = [];
                }
            }
        }
        // 写入剩余数据
        if ($data) {
            $insertFunc($data);
        }

        return $count;
    }


    /**
     * 解析 Excel 获取第一行头信息
     * @param string $file Excel 路径名文件名
     * @param string $type Excel2007|Excel5
     * @return array
     */
    public static function parseHeader($file, $type = '')
    {
        $type = self::getType($file, $type);
        $objReader = PHPExcel_IOFactory::createReader($type);
        $objPHPExcel = $objReader->load($file);
        $header = [];
        foreach ($objPHPExcel->getSheet()->getRowIterator() as $row) {
            // 逐个单元格读取，减少内存消耗
            $cellIterator = $row->getCellIterator();
            // 不跳过空值
            $cellIterator->setIterateOnlyExistingCells();
            if ($objPHPExcel->getActiveSheet()->getRowDimension($row->getRowIndex())->getVisible()) {
                foreach ($cellIterator as $cell) {
                    if ($objPHPExcel->getActiveSheet()->getColumnDimension($cell->getColumn())->getVisible()) {
                        $header[$cell->getColumn()] = $cell->getValue();
                    }
                }
                break;
            }
        }

        return $header;
    }

    /**
     * 自动获取 Excel 类型
     * @param string $file Excel 路径名文件名
     * @param string $type Excel2007|Excel5
     * @return string
     * @throws Exception
     */
    private static function getType($file, $type = '')
    {
        if (!$type) {
            $ext = pathinfo($file, PATHINFO_EXTENSION);
            switch ($ext) {
                case 'xls' :
                    $type = 'Excel5';
                    break;
                case 'xlsx' :
                    $type = 'Excel2007';
                    break;
                default:
                    throw new Exception('请指定Excel的类型');
            }
        }
        return $type;
    }

    /**
     * 将 Excel 时间转为标准的时间格式
     * @param $date
     * @param bool $time
     * @return array|int|string
     */
    public static function excelTime($date, $time = false)
    {
        if (function_exists('GregorianToJD')) {
            if (is_numeric($date)) {
                $jd = GregorianToJD(1, 1, 1970);
                $gregorian = JDToGregorian($jd + intval($date) - 25569);
                $date = explode('/', $gregorian);
                $date_str = str_pad($date [2], 4, '0', STR_PAD_LEFT)
                    . "-" . str_pad($date [0], 2, '0', STR_PAD_LEFT)
                    . "-" . str_pad($date [1], 2, '0', STR_PAD_LEFT)
                    . ($time ? " 00:00:00" : '');

                return $date_str;
            }
        } else {
            $date = $date > 25568 ? $date + 1 : 25569;
            $ofs = (70 * 365 + 17 + 3) * 86400;
            $date = date("Y-m-d", ($date * 86400) - $ofs) . ($time ? " 00:00:00" : '');
        }

        return $date;
    }
}

```

- 读取Excel文件


```php
$fileName = "url.xls";

if (!file_exists($fileName)) {

    exit("文件".$fileName."不存在");

}


require_once './PHPExcel/IOFactory.php';

$objPHPExcel = PHPExcel_IOFactory::load($fileName);

//获取sheet表格数目
$sheetCount = $objPHPExcel->getSheetCount();

//默认选中sheet0表
$sheetSelected = 0;
$objPHPExcel->setActiveSheetIndex($sheetSelected);

//获取表格行数
$rowCount = $objPHPExcel->getActiveSheet()->getHighestRow();

//获取表格列数
$columnCount = $objPHPExcel->getActiveSheet()->getHighestColumn();

echo "<div>Sheet Count : ".$sheetCount."　　行数： ".$rowCount."　　列数：".$columnCount."</div>";

$dataArr = array();

 
/* 循环读取每个单元格的数据 */
//行数循环
for ($row = 1; $row <= $rowCount; $row++){

	//列数循环 , 列数是以A列开始
	for ($column = 'A'; $column <= $columnCount; $column++) {

	    $dataArr[] = $objPHPExcel->getActiveSheet()->getCell($column.$row)->getValue();
	    echo $column.$row.":".$objPHPExcel->getActiveSheet()->getCell($column.$row)->getValue()."<br />";

	}

	echo "<br/>消耗的内存为：".(memory_get_peak_usage(true) / 1024 / 1024)."M";

	$endTime = time();

	echo "<div>解析完后，当前的时间为：".date("Y-m-d H:i:s")."　　　

	总共消耗的时间为：".(($endTime - $startTime))."秒</div>";

	var_dump($dataArr);

	$dataArr = NULL;
}
```

















