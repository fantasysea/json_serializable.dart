
使用dart解析json的时候,如果类型不对,解析会直接失败,没法强转.后台经常会在改返回*null*的时候返回"",返回对象{}的时候返回[]数组,返回int的时候,返回String.由于后台很多代码是现成的,很难修改,只能兼容,所以我把使用int的地方,还有遇到{} [] 这种类型不对的都做了判断,返回了null,牺牲了一些性能,但是能保证运行的时候能正常.
例如:
解析map的时候判断如果是""或者[]或者是null都返回null,解析int的时候判断""或者null的时候返回"0",最后都通过int.parse("0")强转得到int.这样判断之后,错误率直线下降,开发效率大大提升.


```dart
//解析map的判断
(json['data'] == null ||
            json['data'].toString() == '' ||
            json['data'].toString() == '[]')
        ? null
        : Data.fromJson(json['data'] as Map<String, dynamic>),

//解析int
int.parse((json['status'] == null) || json['status'] == ""
        ? "0"
        : json['status'].toString()),


````

[![Build Status](https://travis-ci.org/google/json_serializable.dart.svg?branch=master)](https://travis-ci.org/google/json_serializable.dart)

Provides [source_gen] `Generator`s to create code for JSON serialization and
deserialization.

## json_serializable

* Package: https://pub.dev/packages/json_serializable
* [Source code](json_serializable)

The core package providing Generators for JSON-specific tasks.

Import it into your pubspec `dev_dependencies:` section.

## json_annotation

* Package: https://pub.dev/packages/json_annotation
* [Source code](json_annotation)

The annotation package which has no dependencies.

Import it into your pubspec `dependencies:` section.

## checked_yaml

* Package: https://pub.dev/packages/checked_yaml
* [Source code](checked_yaml)

Generate more helpful exceptions when decoding YAML documents using
`package:json_serializable` and `package:yaml`.

Import it into your pubspec `dependencies:` section.

## example

* [Source code](example)

An example showing how to setup and use `json_serializable` and
`json_annotation`.

[source_gen]: https://pub.dev/packages/source_gen
