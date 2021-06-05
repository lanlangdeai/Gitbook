# 第三方扩展库



使用composer进行安装，卸载，升级





1. ## 加解密组件

- hashids(https://github.com/vinkla/hashids)

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

