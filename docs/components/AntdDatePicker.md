# AntdDatePicker

## 简介源码：`views/AntdDatePicker/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {"title": translator.t("组件介绍")},
                {"title": translator.t("数据录入")},
                {"title": translator.t("AntdDatePicker 日期选择")},
            ],
            style={"marginBottom": 8},
        ),
        fac.AntdTitle(translator.t("AntdDatePicker 日期选择"), level=2),
        fac.AntdParagraph(translator.t("提供常见的日期选择相关功能。")),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo1',
                    style={'width': 175},
                ),
                fac.AntdText(id='date-picker-demo1-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo2',
                    placeholder='请选择日期时间',
                    style={'width': 175},
                    showTime=True,
                ),
                fac.AntdText(id='date-picker-demo2-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo3',
                    placeholder='配合自定义format',
                    format='YYYY年MM月DD日',
                    style={'width': 175},
                ),
                fac.AntdText(id='date-picker-demo3-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('date-picker-demo1-output', 'children'),
    Input('date-picker-demo1', 'value'),
)
def date_picker_demo1(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo2-output', 'children'),
    Input('date-picker-demo2', 'value'),
)
def date_picker_demo2(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo3-output', 'children'),
    Input('date-picker-demo3', 'value'),
)
def date_picker_demo3(value):
    return f'value: {value}'
```

### 基础使用

- 说明：最基础的日期选择、日期时间选择。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(),
        fac.AntdDatePicker(placeholder='请选择日期时间', showTime=True),
    ],
    wrap=True,
)
```

### 控制指定日期单元格样式

- 说明：通过参数`customCells`对指定规则对应的日期单元格添加额外样式，未填写条件的部分将视作通配规则。

#### 代码
```python
fac.AntdSpace(
    [
        '精确日期匹配：明天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'year': datetime.now().year,
                    'month': datetime.now().month,
                    'date': (datetime.now() + timedelta(days=1)).day,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
        '年份通配：每年的本月第10天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'month': datetime.now().month,
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
        '年份+月份通配：每月的第10天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 自定义format

- 说明：设置参数`format`以实现不同粒度设置下适合的已选内容回填格式化。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placeholder='picker="date"',
            format='YYYY年MM月DD日',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="week"',
            picker='week',
            format='YYYY年第w周',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="month"',
            picker='month',
            format='YYYY-MM',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="year"',
            picker='year',
            format='YYYY年',
            style={'width': 175},
        ),
    ],
    direction='vertical',
)
```

### 不同的日期选择粒度

- 说明：设置参数`picker`选择不同的日期选择粒度。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(picker=picker, placeholder=f'picker="{picker}"')
        for picker in ['date', 'week', 'month', 'quarter', 'year']
    ],
    direction='vertical',
)
```

### 悬浮层展开方位

- 说明：设置参数`placement`控制悬浮层展开方位。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placement=placement, placeholder=f'placement="{placement}"'
        )
        for placement in [
            'bottomLeft',
            'bottomRight',
            'topLeft',
            'topRight',
        ]
    ],
    direction='vertical',
)
```

### 禁用状态

- 说明：设置参数`disabled=True`开启禁用状态。

#### 代码
```python
fac.AntdDatePicker(disabled=True)
```

### 自定义日期禁用策略

- 说明：设置参数`disabledDatesStrategy`控制需要禁止用户选中的日期。

#### 代码
```python
[
    fac.AntdDivider("mode='eq'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'eq', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ne'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月非6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ne', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='le'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月小于等于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'le', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='lt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月小于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'lt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ge'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月大于等于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ge', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='gt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月大于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'gt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月的5号到25号',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='not-in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用非每月的5号到25号',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'not-in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用枚举列表中的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("mode='not-in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用非枚举列表中的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'not-in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("target='specific-date'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用指定日期之前的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'lt', 'target': 'specific-date', 'value': '2023-01-15'}
        ],
        pickerValue='2023-01-01',
    ),
]
```

### 基于回调的动态日期禁用

- 说明：通过回调函数实现基于当前日期时间的动态禁用策略，以“只允许选择未来7天内日期”为例。

#### 代码
```python
from datetime import datetime, timedelta

...

fac.AntdDatePicker(id='date-picker-dynamic-forbidden-demo')

...

@app.callback(
    Output('date-picker-dynamic-forbidden-demo', 'disabledDatesStrategy'),
    Input('date-picker-dynamic-forbidden-demo', 'id'),
)
def date_picker_dynamic_forbidden_demo(_):

    return [
        {
            'mode': 'lt',
            'target': 'specific-date',
            'value': datetime.now().strftime('%Y-%m-%d'),
        },
        {
            'mode': 'gt',
            'target': 'specific-date',
            'value': (datetime.now() + timedelta(days=7)).strftime('%Y-%m-%d'),
        },
    ]
```

### 底部添加额外内容

- 说明：通过参数`extraFooter`自定义选择面板底部额外的内容。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(extraFooter=fac.AntdText('底部额外内容示例')),
        fac.AntdDatePicker(
            placeholder='请选择日期时间',
            showTime=True,
            extraFooter=fac.AntdText('底部额外内容示例'),
        ),
    ],
    wrap=True,
)
```

### 隐藏今天按钮

- 说明：隐藏“今天”快捷选择按钮。

#### 代码
```python
fac.AntdDatePicker(showToday=False)
```

### 监听面板停留位置

- 说明：通过回调函数监听`pickerValue`的变化，获取当前面板停留位置。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            id='date-picker-listen-picker-value-demo',
            style={'width': 175},
        ),
        fac.AntdText(id='date-picker-listen-picker-value-demo-output'),
    ]
)

...

@app.callback(
    Output('date-picker-listen-picker-value-demo-output', 'children'),
    Input('date-picker-listen-picker-value-demo', 'pickerValue'),
)
def show_picker_value(pickerValue):
    return f'pickerValue: {pickerValue}'
```

### 控制面板停留位置

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            pickerValue='1999-12-31', style={'width': 175}
        ),
        fac.AntdDatePicker(
            placeholder='配合自定义format',
            pickerValue='1999年12月31日',
            format='YYYY年MM月DD日',
            style={'width': 175},
        ),
    ],
    direction='vertical',
)
```

### 内嵌前缀内容

- 说明：通过参数`prefix`设置选择框内嵌前缀内容。

#### 代码
```python
fac.AntdDatePicker(
    value='2024-01-01', prefix=fac.AntdIcon(icon='antd-user')
)
```

### 只读状态

- 说明：设置参数`readOnly=True`开启只读状态。

#### 代码
```python
fac.AntdDatePicker(value='2024-01-01', readOnly=True)
```

### 强制状态渲染

- 说明：设置参数`status`强制状态渲染。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDatePicker(placeholder=f'status="{status}"', status=status)
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
```

### 内嵌后缀图标

- 说明：通过参数`suffixIcon`设置选择框内嵌后缀图标。

#### 代码
```python
fac.AntdDatePicker(
    value='2024-01-01', suffixIcon=fac.AntdIcon(icon='antd-user')
)
```

### 设置自动选定的时间值

- 说明：由参数`showTime.defaultValue`设定的默认值，将会在用户初次选中日期后，在时间选择面板中被自动选中。

#### 代码
```python
fac.AntdDatePicker(
    placeholder='请选择日期时间', showTime={'defaultValue': '18:33:33'}
)
```

## API 参数说明

- id (string; optional):  
   Unique component id.

- key (string; optional):  
   Update the `key` value of the current component to force re-rendering of the component.

- className (string | dict; optional):  
   CSS class name of the current component, supports [dynamic css](/advanced-classname).

- popupClassName (string; optional):  
   CSS class name of the dropdown menu.

- name (string; optional):  
   Used with the `AntdForm` batch value collection/control function, serving as the field name of the current form item. Defaults to `id`.

- enableBatchControl (boolean; default True):  
   Controls whether the current component participates in the effective `AntdForm` batch value collection/control function. Default: `True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):  
   Language of the component text. Options: `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German), `'ru-ru'` (Russian).  
   Default: `'zh-cn'`.

- format (string; optional):  
   Date/time display format, [reference](https://day.js.org/docs/en/display/format).  
   Default: `'YYYY-MM-DD'`.

- picker (a value equal to: 'date', 'week', 'month', 'quarter', 'year'; default 'date'):  
   Date selection granularity. Options: `'date'`, `'week'`, `'month'`, `'quarter'`, `'year'`.  
   Default: `'date'`.

- firstDayOfWeek (number; optional):  
   Custom index of the first day of the week.

- disabled (boolean; default False):  
   Whether to disable the component. Default: `False`.

- showTime (dict; default False):  
   Configure parameters related to the time selection panel. Default: `False`.

  `showTime` is a boolean | dict with keys:

  - defaultValue (string; optional):  
     Initial selected time string for the time selection panel.

  - format (string; optional):  
     Time format corresponding to `defaultValue`, [reference](https://day.js.org/docs/en/display/format).  
     Default: `'HH:mm:ss'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):  
   Size specification of the component. Options: `'small'`, `'middle'`, `'large'`.  
   Default: `'middle'`.

- bordered (boolean; default True):  
   Whether to show a border. Equivalent to `variant='outlined'` when set to `True`. Default: `True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):  
   Variant type. Options: `'outlined'`, `'borderless'`, `'filled'`, `'underlined'`. `'outlined'` is equivalent to `bordered=True`, but takes higher priority.

- placeholder (string; optional):  
   Placeholder text in the input box.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):  
   Direction in which the panel expands. Options: `'bottomLeft'`, `'bottomRight'`, `'topLeft'`, `'topRight'`.  
   Default: `'bottomLeft'`.

- value (string; optional):  
   Listen to or set the selected value, corresponding to `format`.

- defaultValue (string; optional):  
   Initial selected value, corresponding to `format`.

- pickerValue (string; optional):  
   Listen to or set the panel’s displayed date, corresponding to `format`.

- disabledDatesStrategy (list of dicts; optional):  
   Configure an array of disabled date strategies. Dates matching at least one rule will be disabled.

  `disabledDatesStrategy` is a list of dicts with keys:

  - mode (a value equal to: 'eq', 'ne', 'le', 'lt', 'ge', 'gt', 'in', 'not-in', 'in-enumerate-dates', 'not-in-enumerate-dates'; optional):  
     Current strategy type. Options: `'eq'` (equal), `'ne'` (not equal), `'le'` (less than or equal), `'lt'` (less than), `'ge'` (greater than or equal),  
     `'gt'` (greater than), `'in'` (in), `'not-in'` (not in), `'in-enumerate-dates'` (in list of date strings), `'not-in-enumerate-dates'` (not in list of date strings).

  - target (a value equal to: 'day', 'month', 'quarter', 'year', 'dayOfYear', 'dayOfWeek', 'specific-date'; optional):  
     Strategy target. Options: `'dayOfYear'` (by day of year), `'dayOfWeek'` (by day of week), `'day'` (by day), `'month'` (by month), `'quarter'` (by quarter), `'year'` (by year), `'specific-date'` (specific date).  
     For `'specific-date'`, the `value` must strictly follow the `'YYYY-MM-DD'` format.

  - value (number | string | list of numbers | list of strings; optional):  
     The actual constraint value corresponding to the strategy type and target.

- status (a value equal to: 'error', 'warning'; optional):  
   Validation status. Options: `'error'`, `'warning'`.

- allowClear (boolean; default True):  
   Whether to allow clearing the selected value with one click. Default: `True`.

- autoFocus (boolean; default False):  
   Whether to automatically focus. Default: `False`.

- readOnly (boolean; optional):  
   Whether to render as read-only. Default: `False`.

- extraFooter (a list of or a singular dash component, string or number; optional):  
   Component type, extra footer content.

- showToday (boolean; default True):  
   Whether to show the “Today” quick selection button. Default: `True`.

- presets (list of dicts; optional):  
   Configure a list of presets.

  `presets` is a list of dicts with keys:

  - label (a list of or a singular dash component, string or number; optional):  
     Component type, label for the preset item.

  - value (string; optional):  
     Value of the preset item, corresponding to `format`.

- clickedPreset (dict; optional):  
   Works with the `presets` parameter, listens for the most recent preset item click event information.

  `clickedPreset` is a dict with keys:

  - value (string | number; optional):  
     Value of the preset item.

  - timestamp (number; optional):  
     Timestamp of the event.

- needConfirm (boolean; default False):  
   Whether clicking a button is required to confirm selection. If `False`, losing focus means selection is made. Default: `False`.

- customCells (list of dicts; optional):  
   Customize cell styles for specific dates.

  `customCells` is a list of dicts with keys:

  - year (number; optional):  
     Year value for matching.

  - month (number; optional):  
     Month value for matching.

  - date (number; optional):  
     Day value for matching.

  - style (dict; optional):  
     Custom CSS style.

  - className (string; optional):  
     Custom CSS class name.

- prefix (a list of or a singular dash component, string or number; optional):  
   Component type, embedded prefix content.

- suffixIcon (a list of or a singular dash component, string or number; optional):  
   Custom suffix icon content for the selection box.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):  
   Anchoring strategy for the dropdown layer. Options: `'parent'`, `'body'`. Default: `'body'`.

- batchPropsNames (list of strings; optional):  
   List of property names to include in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):  
   Listen to the values of properties specified in `batchPropsNames`.

- data-_ (string; optional):  
   Wildcard attribute in `data-_` format.

- aria-_ (string; optional):  
   Wildcard attribute in `aria-_` format.

- persistence (boolean | string | number; optional):  
   Whether to enable [property persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):  
   Properties enabled for persistence. Options: `'value'`.  
   Default: `['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):  
   Type of persistence storage. Options: `'local'` (local storage), `'session'` (session storage), `'memory'` (in-memory).  
   Default: `'local'`.
