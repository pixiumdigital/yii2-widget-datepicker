# Pixium DatePicker

### This widget is a slighlty different version of Kartik's DatePicker.
### You can check it on Kartik's github [here](/kartik-v/yii2-widget-datepicker).

## What is different  ?
### PluginOptions
The `pluginOptions` parameter can have the following fields:
- `eventCls`: _string_, the class associated to a cell when `beforeShowDay`, `beforeShowMonth` etc. are called and return `event` 
- `selectable`: _boolean_, wether the month and years are selected with a `<select>` tag or not

### BeforeShowDay
returning `boolean` can now also mean if the day has an event or not. Therefore, in order to use `event`, an object should always be returned.
The returned object can contains the following:
```js
    return {
        enabled: boolean,
        classes: string,
        tooltip: tooltip,
        content: string,
        event: boolean
    }
```

## Usage

### -Selecatble is __not set__  or set on __`false`__

<img src="README.assets/image-20191226144512075.png" width="300px">

```php
echo $form->field($model, 'field')->widget(kartik\datecontrol\DateControl::classname(), [
					'type' => 'date',
          'options' => [
						'id' => 'myDate',
					],
					'autoWidget' => true,
					'widgetOptions' => [
						'options' => [
              //Options here...
						],
						'pluginOptions' => [
							'selectable' => false,
						],
						'pluginEvents' => [
              //Events here...
						]
					]
]);
```



### -Selecatble is set on __`true`__

<img src="README.assets/image-20191226145144051.png" width="300px">

```php
echo $form->field($model, 'field')->widget(kartik\datecontrol\DateControl::classname(), [
					'type' => 'date',
          'options' => [
						'id' => 'myDate',
					],
					'autoWidget' => true,
					'widgetOptions' => [
						'options' => [
              //Options here...
						],
						'pluginOptions' => [
							'selectable' => true,
						],
						'pluginEvents' => [
              //Events here...
						]
					]
]);
```



### - eventCls is set and beforeShowDay returns `event`

<img src="README.assets/image-20191226145554846.png" width="300px">

```js
function magic(date) {
		if (/*Condition*/) {
			return {
				event: true
			};
		}
}
```



```php
$myExpression = new JsExpression('function(date) { return magic(date); }');

echo $form->field($model, 'from')->widget(kartik\datecontrol\DateControl::classname(), [
					'type' => 'date',
  				'options' => [
						'id' => 'fromDate',
					],
					'autoWidget' => true,
					'widgetOptions' => [
						'options' => [
              //Options here...
						],
						'pluginOptions' => [
							'beforeShowDay' => $myExpression,
							'eventCls' => 'green-circle',
              'selectable' => true,
						],
						'pluginEvents' => [
              //Plugin events here...
						]
					]
]);
```

