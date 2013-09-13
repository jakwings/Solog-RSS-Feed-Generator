Solog RSS Feed Generator
========================

一个简单的 RSS Feed 生成工具。

> A simple RSS 2.0 feed generator.


## 说明文档（Documentation）

不妨直接看源代码及注释。;)

> Please see the source code and comments. ;)

### 支持的 channel 子元素（sub-elements of channel）

子元素的名称是大小写敏感的。

> Names of sub-elements are case-sensitive.

```
title, link, description, pubDate, lastBuildDate,
language, copyright, managingEditor, webMaster,
category, cloud, ttl, image, rating, textInput,
skipHours, skipDays
```

`docs` 和 `generator` 被保留，无法设置。

> `docs` and `generator` are preserved and can not be set.

### 支持的 item 子元素（sub-elements of item）

子元素的名称是大小写敏感的。

> Names of sub-elements are case-sensitive.

```
title, link, description, category, pubDate,
comments, author, enclosure, guid, source
```


## 示例（Examples）

### 创建实例（Create an instance）

```
require 'rss.class.php';
$rss = new RssFeed('"Title \'oh\'"', 'http://example.com', 'Just for test.');
```

### 修改 channel 配置（Configure channel element）

```
$rss->Config('pubDate', date(DATE_RSS, strtotime('2013-12-25')));
$rss->Config('language', 'zh-cn');
$rss->Config('cloud', array(
  'attrs' => array(
    'domain' => 'rpc.sys.com',
    'port' => '80',
    'path' => '/RPC2',
    'registerProcedure' => 'myCloud.rssPleaseNotify',
    'protocol' => 'xml-rpc',
  ),
  'value' => '',  // 可选（optional）
));
$rss->Config('image', array(
  'value' => array(  // 子元素（sub-elements）
    'url' => 'http://example.com/favicon.png',
    'title' => '"Title \'oh\'"',
    'link' => 'http://example.com',
    'example' => array(
      'attrs' => array(
        'a' => 1,
        'b' => 2,
      ),
      'value' => array(
        'url' => 'http://example.com/favicon.png',
        'title' => '"Title \'oh\'"',
        'link' => 'http://example.com',
      ),
    ),
  ),
));
```

### 添加文章信息（Add an "item" element）

```
$rss->AddItem(array(
  'title' => 'Hello, world!',
  'description' => 'Foo came into the bar and said to Baz, "Hello, world!"',
  'source' => array(
    'attrs' => array('url' => 'http://example2.com/feed.xml'),
    'value' => 'Foo Example'
  ),
));
```

### 输出 Feed 到网页（Display the feed）

```
$rss->Publish();
```

### 获取 Feed 的内容（Get feed content）

```
$content = $rss->Fetch();
```
