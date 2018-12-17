# Configuring flutter-view

Flutter-view has been made to run without needing configuration. However by providing a configuration, you can use some more advanced features.

To configure flutter-view, put a file named **flutter-view.json** in the directory you run it from \(normally your project root directory\).

There are many options you can play with. Each of these options is optional. Options will merge their values with the ones you provides.

For example, to change the indentation of the generated Dart to 4 spaces:

{% code-tabs %}
{% code-tabs-item title="flutter-view.json" %}
```javascript
{
    indentation: 4
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## indentation

Changes the indentation of the generated Dart files.

Default value:

```javascript
indentation: 2
```

## imports

Lets you provide a list of imports to add in every generated Dart file. This can save you from having to add the same import statement at the top of your files.

Default value:

```javascript
imports: [
	'package:flutter/material.dart',
	'package:flutter/cupertino.dart'
]
```

For example, to add the [**flutter\_view\_tools**](../get-started/installation.md#installing-flutter-view-tools) to each file:

{% code-tabs %}
{% code-tabs-item title="flutter-view.json" %}
```javascript
{
    imports: [
        "package:flutter_view_tools/flutter_view_tools.dart"
    ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## tagClasses

Lets you map how certain tags are mapped into Dart classes. For example, by default a DIV is mapped into a Container.

Default value:

```javascript
tagClasses: {
	text: 'Text',
	div: 'Container',
	span: 'Wrap',
	button: 'RaisedButton',
	backgroundAssetImg: 'ExactAssetImage',
	backgroundUrlImg: 'NetworkImage'
}
```

For example, if you want to use FlatButton when you use the button tag:

{% code-tabs %}
{% code-tabs-item title="flutter-view.json" %}
```javascript
{
    tagClasses: {
        button: "FlatButton"
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## multiChildClasses

In Flutter, some widgets expect a child parameter, while others expect a children parameter. With multiChildClasses you can list classes that require the children parameter \(otherwise child is used\).

Default value:

```javascript
multiChildClasses: [
	'Row',
	'Column',
	'Stack',
	'IndexedStack',
	'GridView',
	'Flow',
	'Table',
	'Wrap',
	'ListBody',
	'ListView',
	'CustomMultiChildLayout'
]
```

## autowrapChildren and autoWrapChildrenClass

In HTML layouts, any element can have multiple children. However in Flutter, some widgets accept only a single child. 

If autowrapChildren is set to false, only the first child is set. 

If autowrapChildren is set to true, the children are wrapped by a widget that accepts multiple children. The widget used is set in the autowrapChildrenClass property.

The default values:

```javascript
autowrapChildren: true,
autowrapChildrenClass: 'Column'
```

## showPugLineNumbers

If set to true, flutter-view will add comments to the Dart file that link back to the original pug files. These comments are [used by the VSCode extensions](../get-started/vs-code-support.md#linking-between-pug-and-generated-dart) to provide easy navigation between the two.

The comments look like this:

`Container( // project://lib/screens/queue/queue.pug#19,6`

Default value:

```javascript
showPugLineNumbers: true
```

## showCommentsInDart

If true, flutter-view will add comments in Dart based on the classes and ids that you assign to tags in the Pug or HTML.

For example, the following Pug code:

```css
#title(as='title') Tasks
```

Will add the \#title as a comment:

```dart
//-- TITLE ----------------------------------------------------------
Container(
    child: Text( 
        'Tasks',
    ),
)
```

By setting showCommentsInDart, this feature is disabled.

Default value:

```javascript
showCommentsInDart: true
```

## reportErrorsInDart

If set to true, if there is an error processing a pug or css file, the error will not only be printed by flutter-view in the console, but also be shown as text in the Dart file.

The benefit of this is that you will get a red Dart file, so you get an active warning something got broken. A downside is that sometimes it breaks hot reloading.

Default value:

```javascript
reportErrorsInDart: true
```

## propagateDelete

If true, when you delete a pug file, the asociated Dart file also gets deleted.

Default value:

```javascript
propagateDelete: true
```


