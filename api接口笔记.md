# API接口笔记

## 暴露问题
---

+ 列表数据返回时，不能用 `Lesson::all()`方法，这样如果数据量大的时候，会给用户很不好的体验
+ 直接 `return Lesson` 返回的话，不能添加额外的信息，比如状态码(status_code),消息(message)等
+ 会把数据库里面的字段直接呈现出来，这样的话会暴露数据库的结构

## 解决方案
---
+ Laravel5 里面,`\Response::json`可以直接返回json格式的数据,比如		

```
retuen \Response::json([
	'status_code' => 200,
	'message' => 'success',
	'data' => $lessons
]);
```
+ 给需要返回的结果集添加处理方法 `tranForm`,比如		

```
public function transForm($lessons){
	return array_map(function($lesson){
		return [
			'title' => $lesson['title'],
			'content' => $lesson['body],
			'is_free' => $lesson['free']
		];
	}, $lessons->toArray());
}
```
+ 当对数据进行处理时，应该建立一个专门的数据处理类 `Transformer.php` 该类的作用就是把从数据库里面查出来的数据进行字段映射。一般的，我们做API接口时，会有一个数据的列表和数据的详情，[Laravel](http://laravist.com)中,分别是 `Lesson::all()`和`Lesson::findOrFail()`，前者返回的是一个Collection对象，后者返回的是一个数组,当我们对其进行处理时,可以先建立一个抽象的父类，里面建立一个处理Collection对象的方法，这样可以对所有的列表进行统一的处理，然后针对每一个不同的Model，相对应的建立子类，来继承这个`Transformer.php`,这样就可以完美解决。
