# 第三方扩展库



使用composer进行安装，卸载，升级





1. ## 加解密组件

- ### hashids(https://github.com/vinkla/hashids)

Hashids是一个能利用整数生成出短小、唯一、非连续标识符的类库，它支持包含php在内的好多好多（真的好多）种语言。

Hashids支持通过生成出来的标识符进行解码为原数字，还支持加盐加密，不会因为大家都用这个类库就被猜到真实ID。

官网地址：https://hashids.org

该库支持多种库[JavaScript](https://hashids.org/javascript), [Ruby](https://hashids.org/ruby), [Python](https://hashids.org/python), [Java](https://hashids.org/java), [Scala](https://hashids.org/scala), [PHP](https://hashids.org/php), [Perl](https://hashids.org/perl), [Perl 6](https://hashids.org/perl6), [Swift](https://hashids.org/swift), [Clojure](https://hashids.org/clojure), [Objective-C](https://hashids.org/objective-c), [C](https://hashids.org/c), [C++11](https://hashids.org/cpp), [D](https://hashids.org/d), [F#](https://hashids.org/f-sharp), [Go](https://hashids.org/go), [Erlang](https://hashids.org/erlang), [Lua](https://hashids.org/lua), [Haskell](https://hashids.org/haskell), [OCaml](https://hashids.org/ocaml), [Elixir](https://hashids.org/elixir), [Rust](https://hashids.org/rust), [Smalltalk](https://hashids.org/smalltalk), [ColdFusion](https://hashids.org/coldfusion), [Kotlin](https://hashids.org/kotlin), [Nim](https://hashids.org/nim), [VBA](https://hashids.org/vba), [Haxe](https://hashids.org/haxe), [Crystal](https://hashids.org/crystal), [Elm](https://hashids.org/elm), [ActionScript](https://hashids.org/actionscript), [Bash](https://hashids.org/bash), [R](https://hashids.org/r), [TSQL](https://hashids.org/tsql), [PostgreSQL](https://hashids.org/postgresql), [PLpgSQL](https://hashids.org/plpgsql), [Dart](https://hashids.org/dart), [Io](https://hashids.org/io), [Julia](https://hashids.org/julia) and for [.NET](https://hashids.org/net)



安装：

```php
composer require hashids/hashids
```

使用：

```php
use Hashids\Hashids;

$hashids = new Hashids();

$hashids->encode(1);

===================================

use Hashids\Hashids;

$hashids = new Hashids();

$id = $hashids->encode(1, 2, 3); // o2fXhV
$numbers = $hashids->decode($id); // [1, 2, 3]
```



---



2. ## 数据操作工具

- ### php-dot-notation(https://github.com/adbario/php-dot-notation)

可以使用点符号操作数组的类库



安装：

```php
composer require adbario/php-dot-notation
```



示例：

```php
// 之前数据
$array['info']['home']['address'] = 'Kings Square';

echo $array['info']['home']['address'];

// Kings Square


//使用该类库
$dot->set('info.home.address', 'Kings Square');

echo $dot->get('info.home.address');

or

$dot['info.home.address'] = 'Kings Square';

echo $dot['info.home.address'];

```



---



- ### weblibs-configmanager(https://github.com/clagiordano/weblibs-configmanager/)

weblib-configmanager是一个简单而轻量的工具库，用于管理PHP分层配置文件，可以实现对于数组文件的读取与修改操作



支持的格式：

![image-20210610215739946](C:\Users\lixing02\AppData\Roaming\Typora\typora-user-images\image-20210610215739946.png)



安装：

```
composer require clagiordano/weblibs-configmanager
```



基本使用：



基础数据

```php
<?php

return array (
  'app' => 'app_name',
  'db' => 
  array (
    'host' => 'localhost',
    'user' => 'sample_user',
    'pass' => 'sample_pass',
    'port' => 3306,
  ),
  'other' => 
  array (
    'multi' => 
    array (
      'deep' => 
      array (
        'nested' => 'config_value',
      ),
    ),
  ),
);

```


操作：

```php
1）
use clagiordano\weblibs\configmanager\ConfigManager;

/**
 * Instance object to read argument file
 */
$config = new ConfigManager("configfile.php");

2）
/**
 * Check if a value exists into config file
 */
$value = $config->existValue('app');

3）
/**
 * Read a simple element from config file
 */
$value = $config->getValue('app');

4）
/**
 * Access to a nested element from config
 */
$nestedValue = $config->getValue('other.multi.deep.nested');

5）
/**
 * Change config value at runtime
 */
$this->config->setValue('other.multi.deep.nested', "SUPERNESTED");

6）
/**
 * Save config file with original name (OVERWRITE) 
 */
$this->config->saveConfigFile('/new/file/name/or/path/test.php');


```



---



- ### danielstjules/stringy（https://github.com/danielstjules/Stringy）


一个支持多字节的PHP字符串操作库。兼容PHP 5.4+， PHP 7+和HHVM



  安装

```php
composer：
require 'vendor/autoload.php';

包导入：
require_once 'path/to/Stringy/src/Stringy.php';

use Stringy\Stringy as S;
```



示例

```php
// Standard library
strtoupper('fòôbàř');       // 'FòôBàř'
strlen('fòôbàř');           // 10

// mbstring
mb_strtoupper('fòôbàř');    // 'FÒÔBÀŘ'
mb_strlen('fòôbàř');        // '6'

// Stringy
s('fòôbàř')->toUpperCase(); // 'FÒÔBÀŘ'
s('fòôbàř')->length();      // '6'


方便处理包含特殊多字符的字符串，支持多种操作
```



- jmespath/jmespath.py(https://github.com/jmespath/jmespath.php) 有PHP，Python，js，lua等语言支持

JMESPath是JSON的查询语言



安装

```php
composer require "mtdowling/jmespath.php"
```



使用

```php
    require 'vendor/autoload.php';

    $expression = 'foo.*.baz';

    $data = [
        'foo' => [
            'bar' => ['baz' => 1],
            'bam' => ['baz' => 2],
            'boo' => ['baz' => 3]
        ]
    ];

     ($expression, $data);
    // Returns: [1, 2, 3]

```



- PHPOffice/PHPExcel(https://github.com/PHPOffice/PHPExcel)



安装

```
composer require phpoffice/phpexcel
```

使用

```php
/** Include PHPExcel */
require_once dirname(__FILE__) . '/../Classes/PHPExcel.php';


// Create new PHPExcel object
echo date('H:i:s') , " Create new PHPExcel object" , EOL;
$objPHPExcel = new PHPExcel();

// Set document properties
echo date('H:i:s') , " Set document properties" , EOL;
$objPHPExcel->getProperties()->setCreator("Maarten Balliauw")
							 ->setLastModifiedBy("Maarten Balliauw")
							 ->setTitle("PHPExcel Test Document")
							 ->setSubject("PHPExcel Test Document")
							 ->setDescription("Test document for PHPExcel, generated using PHP classes.")
							 ->setKeywords("office PHPExcel php")
							 ->setCategory("Test result file");


// Add some data
echo date('H:i:s') , " Add some data" , EOL;
$objPHPExcel->setActiveSheetIndex(0)
            ->setCellValue('A1', 'Hello')
            ->setCellValue('B2', 'world!')
            ->setCellValue('C1', 'Hello')
            ->setCellValue('D2', 'world!');

// Miscellaneous glyphs, UTF-8
$objPHPExcel->setActiveSheetIndex(0)
            ->setCellValue('A4', 'Miscellaneous glyphs')
            ->setCellValue('A5', 'éàèùâêîôûëïüÿäöüç');


$objPHPExcel->getActiveSheet()->setCellValue('A8',"Hello\nWorld");
$objPHPExcel->getActiveSheet()->getRowDimension(8)->setRowHeight(-1);
$objPHPExcel->getActiveSheet()->getStyle('A8')->getAlignment()->setWrapText(true);


// Rename worksheet
echo date('H:i:s') , " Rename worksheet" , EOL;
$objPHPExcel->getActiveSheet()->setTitle('Simple');


// Set active sheet index to the first sheet, so Excel opens this as the first sheet
$objPHPExcel->setActiveSheetIndex(0);

```



---



3. ### 日志处理

- monolog/monolog(https://github.com/Seldaek/monolog)

  将日志发送到文件、套接字、收件箱、数据库和各种web服务， 最新版本2.0只支持PHP7.2  如果是以下版本，可以使用^1.25版本 它支持PHP5



安装

```php
composer require monolog/monolog
```



使用

```php
<?php

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

// create a log channel
$log = new Logger('name');
$log->pushHandler(new StreamHandler('path/to/your.log', Logger::WARNING));

// add records to the log
$log->warning('Foo');
$log->error('Bar');

```



---



4. ### 第三方开发工具包

- overtrue/wechat(https://easywechat.com/)（https://github.com/w7corp/easywechat）

非官网的微信SDK，方便快捷的接入微信相关功能,还支持laravel框架的集成（https://github.com/overtrue/laravel-wechat）





安装

```php
composer require "overtrue/wechat:~3.1" -vvv
```



使用

```php
use EasyWeChat\Factory;

$options = [
    'app_id'    => 'wx3cf0f39249eb0exxx',
    'secret'    => 'f1c242f4f28f735d4687abb469072xxx',
    'token'     => 'easywechat',
    'log' => [
        'level' => 'debug',
        'file'  => '/tmp/easywechat.log',
    ],
    // ...
];

$app = Factory::officialAccount($options);

$server = $app->server;
$user = $app->user;

$server->push(function($message) use ($user) {
    $fromUser = $user->get($message['FromUserName']);

    return "{$fromUser->nickname} 您好！欢迎关注 overtrue!";
});

$server->serve()->send();

```



---



- overtrue/socialite(https://github.com/overtrue/socialite)

Socialite 是一个 [OAuth2](https://oauth.net/2/) 认证工具。 它的灵感来源于 [laravel/socialite](https://github.com/laravel/socialite)， 你可以很轻易的在任何 PHP 项目中使用它。

该工具现已支持平台有：Facebook，Github，Google，Linkedin，Outlook，QQ，TAPD，支付宝，淘宝，百度，钉钉，微博，微信，抖音，飞书，豆瓣，企业微信，腾讯云。



安装

```php
$ composer require "overtrue/socialite" -vvv
```



- [Alipay - 用户信息授权](https://opendocs.alipay.com/open/289/105656)
- [DingTalk - 扫码登录第三方网站](https://ding-doc.dingtalk.com/doc#/serverapi3/mrugr3)
- [Google - OpenID Connect](https://developers.google.com/identity/protocols/OpenIDConnect)
- [Github - Authorizing OAuth Apps](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/)
- [Facebook - Graph API](https://developers.facebook.com/docs/graph-api)
- [Linkedin - Authenticating with OAuth 2.0](https://developer.linkedin.com/docs/oauth2)
- [微博 - OAuth 2.0 授权机制说明](http://open.weibo.com/wiki/授权机制说明)
- [QQ - OAuth 2.0 登录QQ](http://wiki.connect.qq.com/oauth2-0简介)
- [腾讯云 - OAuth2.0](https://cloud.tencent.com/document/product/306/37730#.E6.8E.A5.E5.85.A5.E8.85.BE.E8.AE.AF.E4.BA.91-oauth)
- [微信公众平台 - OAuth文档](http://mp.weixin.qq.com/wiki/9/01f711493b5a02f24b04365ac5d8fd95.html)
- [微信开放平台 - 网站应用微信登录开发指南](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419316505&token=&lang=zh_CN)
- [微信开放平台 - 代公众号发起网页授权](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419318590&token=&lang=zh_CN)
- [豆瓣 - OAuth 2.0 授权机制说明](http://developers.douban.com/wiki/?title=oauth2)
- [抖音 - 网站应用开发指南](http://open.douyin.com/platform/doc)
- [飞书 - 授权说明](https://open.feishu.cn/document/ukTMukTMukTM/uMTNz4yM1MjLzUzM)
- [Tapd - 用户授权说明](https://www.tapd.cn/help/show#1120003271001000093)

使用参考：[socialite/README_CN.md at master · overtrue/socialite (github.com)](https://github.com/overtrue/socialite/blob/master/README_CN.md)



---



- overtrue/pinyin(https://github.com/overtrue/pinyin)

🇨🇳 基于 [CC-CEDICT](http://cc-cedict.org/wiki/) 词典的中文转拼音工具，更准确的支持多音字的汉字转拼音解决方案。



![image-20210618101556632](C:\Users\lixing02\AppData\Roaming\Typora\typora-user-images\image-20210618101556632.png)

安装

```php
composer require "overtrue/pinyin:~4.0"
```



使用

```php
use Overtrue\Pinyin\Pinyin;

// 小内存型
$pinyin = new Pinyin(); // 默认
// 内存型
// $pinyin = new Pinyin('\\Overtrue\\Pinyin\\MemoryFileDictLoader');
// I/O型
// $pinyin = new Pinyin('\\Overtrue\\Pinyin\\GeneratorFileDictLoader');

$pinyin->convert('带着希望去旅行，比到达终点更美好');
// ["dai", "zhe", "xi", "wang", "qu", "lyu", "xing", "bi", "dao", "da", "zhong", "dian", "geng", "mei", "hao"]

$pinyin->convert('带着希望去旅行，比到达终点更美好', PINYIN_TONE);
// ["dài","zhe","xī","wàng","qù","lǚ","xíng","bǐ","dào","dá","zhōng","diǎn","gèng","měi","hǎo"]

$pinyin->convert('带着希望去旅行，比到达终点更美好', PINYIN_ASCII_TONE);
//["dai4","zhe","xi1","wang4","qu4","lyu3","xing2","bi3","dao4","da2","zhong1","dian3","geng4","mei3","hao3"]

```





- overtrue/easy-sms(https://github.com/overtrue/easy-sms)

 一款满足你的多种发送需求的短信发送组件

![image-20210618101851897](C:\Users\lixing02\AppData\Roaming\Typora\typora-user-images\image-20210618101851897.png)





安装

```php
$ composer require "overtrue/easy-sms"
```

使用

```php
use Overtrue\EasySms\EasySms;

$config = [
    // HTTP 请求的超时时间（秒）
    'timeout' => 5.0,

    // 默认发送配置
    'default' => [
        // 网关调用策略，默认：顺序调用
        'strategy' => \Overtrue\EasySms\Strategies\OrderStrategy::class,

        // 默认可用的发送网关
        'gateways' => [
            'yunpian', 'aliyun',
        ],
    ],
    // 可用的网关配置
    'gateways' => [
        'errorlog' => [
            'file' => '/tmp/easy-sms.log',
        ],
        'yunpian' => [
            'api_key' => '824f0ff2f71cab52936axxxxxxxxxx',
        ],
        'aliyun' => [
            'access_key_id' => '',
            'access_key_secret' => '',
            'sign_name' => '',
        ],
        //...
    ],
];

$easySms = new EasySms($config);

$easySms->send(13188888888, [
    'content'  => '您的验证码为: 6379',
    'template' => 'SMS_001',
    'data' => [
        'code' => 6379
    ],
]);

```

---



- phpqrcode/phpqrcode(http://phpqrcode.sourceforge.net) ([PHP生成二维码图片 phpqrcode库php-qrcode包 中文手册文档](http://www.phpqrcode.com/))

生成二维码工具

其他：php-qrcode([chillerlan/php-qrcode: A QR Code generator for PHP7.4+ (github.com)](https://github.com/chillerlan/php-qrcode))



安装

```
原生phpqrcode 不支持composer

//thinkphp6 放入 extend 目录
require_once \think\facade\App::getRootPath().'extend/phpqrcode/phpqrcode.php';

//其它框架自行引入  require_once ./phpqrcode/phpqrcode.php
```



使用

```
function create_qrcode($str,$path){
    vendor("phpqrcode.phpqrcode");
    // 纠错级别：L、M、Q、H
    $level = 'Q';
    // 点的大小：1到10,用于手机端4就可以了
    $size = 8;
    $QRcode = new \QRcode();

    try{
        ob_clean();
    }catch (\Exception $e){
        trace($e);
    } 
    $QRcode::png($str, $path, $level, $size);
}
```





### 其他

- 七牛-图片存储服务



安装

```
composer require qiniu/php-sdk
```





5. 邮件相关

- tp-mailer(https://github.com/yuan1994/tp-mailer)

**一款支持所有PHP框架的优美的邮件发送类**，ThinkPHP系列框架开箱即用，其他框架初始化配置即可使用

基于 SwiftMailer 二次开发, 为 ThinkPHP系列框架量身定制, 使 ThinkPHP 支持邮件模板、纯文本、附件邮件发送以及更多邮件功能, 邮件发送简单到只需一行代码

同时了方便其他框架或者非框架使用, Tp Mailer也非常容易拓展融合到其他框架中, 欢迎大家 `Fork` 和 `Star`, 提交代码让Tp Mailer支持更多框架



安装：

```php
composer require yuan1994/tp-mailer
    或者
//下载源码，引入使用
require_once '/path/to/tp-mailer/src/autoload.php;
```







