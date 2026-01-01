# AntdDateRangePicker

## 简介源码：`views/AntdDateRangePicker/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdDateRangePicker 日期范围选择'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDateRangePicker 日期范围选择', level=2),
        fac.AntdParagraph('提供常见的日期范围选择相关功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo1',
                    style={'width': 300},
                ),
                fac.AntdText(id='date-range-picker-demo1-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo2',
                    placeholder=['开始日期时间', '结束日期时间'],
                    style={'width': 350},
                    showTime=True,
                    needConfirm=True,
                ),
                fac.AntdText(id='date-range-picker-demo2-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo3',
                    placeholder=['配合自定义format', ''],
                    format='YYYY年MM月DD日',
                    style={'width': 300},
                ),
                fac.AntdText(id='date-range-picker-demo3-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('date-range-picker-demo1-output', 'children'),
    Input('date-range-picker-demo1', 'value'),
)
def date_range_picker_demo1(value):
    return f'value: {value}'


@app.callback(
    Output('date-range-picker-demo2-output', 'children'),
    Input('date-range-picker-demo2', 'value'),
)
def date_range_picker_demo2(value):
    return f'value: {value}'


@app.callback(
    Output('date-range-picker-demo3-output', 'children'),
    Input('date-range-picker-demo3', 'value'),
)
def date_range_picker_demo3(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(),
        fac.AntdDateRangePicker(
            placeholder=['开始日期时间', '结束日期时间'],
            showTime=True,
            needConfirm=True,
        ),
    ],
    wrap=True,
)
```

### custom_cells

- 说明：演示 custom_cells 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        '精确日期匹配：明天',
        fac.AntdDateRangePicker(
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
        fac.AntdDateRangePicker(
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
        fac.AntdDateRangePicker(
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

### custom_format

- 说明：演示 custom_format 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placeholder=['picker="date"', ''],
            format='YYYY年MM月DD日',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="week"', ''],
            picker='week',
            format='YYYY年第w周',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="month"', ''],
            picker='month',
            format='YYYY-MM',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="year"', ''],
            picker='year',
            format='YYYY年',
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### different_picker

- 说明：演示 different_picker 的用法。

#### 代码
```python
fac.AntdSpace(
        [
            fac.AntdDateRangePicker(
                picker=picker, placeholder=['picker:', picker]
            )
            for picker in ['date', 'week', 'month', 'quarter', 'year']
        ],
        direction='vertical',
    )
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placement=placement, placeholder=['placement:', placement]
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

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(disabled=[True, True]),
        fac.AntdDateRangePicker(disabled=[True, False]),
        fac.AntdDateRangePicker(disabled=[False, True]),
    ],
    direction='vertical',
)
```

### disabled_dates

- 说明：演示 disabled_dates 的用法。

#### 代码
```python
[
    fac.AntdDivider("mode='eq'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'eq', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ne'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月非6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'ne', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='le'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月小于等于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'le', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='lt'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月小于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'lt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ge'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月大于等于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'ge', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='gt'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月大于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'gt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='in'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月的5号到25号', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='not-in'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用非每月的5号到25号', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'not-in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider(
        "mode='in-enumerate-dates'", innerTextOrientation='left'
    ),
    fac.AntdDateRangePicker(
        placeholder=['禁用枚举列表中的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {
                'mode': 'in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider(
        "mode='not-in-enumerate-dates'", innerTextOrientation='left'
    ),
    fac.AntdDateRangePicker(
        placeholder=['禁用非枚举列表中的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {
                'mode': 'not-in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("target='specific-date'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用指定日期之前的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'lt', 'target': 'specific-date', 'value': '2023-01-15'}
        ],
        pickerValue='2023-01-01',
    ),
]
```

### extra_footer

- 说明：演示 extra_footer 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            extraFooter=fac.AntdText('底部额外内容示例')
        ),
        fac.AntdDateRangePicker(
            placeholder=['开始日期时间', '结束日期时间'],
            showTime=True,
            extraFooter=fac.AntdText('底部额外内容示例'),
        ),
    ],
    wrap=True,
)
```

### listen_picker_value

- 说明：演示 listen_picker_value 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            id='date-range-picker-listen-picker-value-demo',
            style={'width': 250},
        ),
        fac.AntdText(
            id='date-range-picker-listen-picker-value-demo-output'
        ),
    ]
)

...

@app.callback(
    Output('date-range-picker-listen-picker-value-demo-output', 'children'),
    Input('date-range-picker-listen-picker-value-demo', 'pickerValue'),
)
def show_picker_value(pickerValue):
    return f'pickerValue: {pickerValue}'
```

### picker_value

- 说明：演示 picker_value 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            pickerValue='1999-12-31', style={'width': 300}
        ),
        fac.AntdDateRangePicker(
            placeholder=['配合自定义format', ''],
            pickerValue='1999年12月31日',
            format='YYYY年MM月DD日',
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'],
    prefix=fac.AntdIcon(icon='antd-user'),
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'], readOnly=True
)
```

### render_status

- 说明：演示 render_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placeholder=[f'status="{status}"', ''],
            status=status,
            style={'width': 300},
        )
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
```

### suffix_icon

- 说明：演示 suffix_icon 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
```

### time_default_value

- 说明：演示 time_default_value 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    placeholder=['开始日期时间', '结束日期时间'],
    showTime={'defaultValue': ['08:30:00', '17:30:00']},
    needConfirm=True,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- popupClassName (string; optional):
    展开菜单css类名.

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- format (string; optional):
    日期时间显示格式，[参考资料](https://day.js.org/docs/en/display/format)
    默认值：`'YYYY-MM-DD'`.

- picker (a value equal to: 'date', 'week', 'month', 'quarter', 'year'; default 'date'):
    日期选择粒度，可选项有`'date'`、`'week'`、`'month'`、`'quarter'`、`'year'`
    默认值：`'date'`.

- firstDayOfWeek (number; optional):
    自定义每周起始日下标.

- disabled (list of booleans; default [False, False]):
    是否禁用当前组件  默认值：`False`.

- showTime (dict; default False):
    配置时间选择面板相关参数  默认值：`False`.

    `showTime` is a boolean | dict with keys:

    - defaultValue (list of strings; optional):
        时间选择面板初始化选中时间字符串.

    - format (string; optional):
        与`defaultValue`对应的时间格式，[参考资料](https://day.js.org/docs/en/display/format)
        默认值：`'HH:mm:ss'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- placeholder (list of strings; optional):
    输入框占位文字内容.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):
    选择面板展开方向，可选项有`'bottomLeft'`、`'bottomRight'`、`'topLeft'`、`'topRight'`
    默认值：`'bottomLeft'`.

- value (list of strings; optional):
    监听或设置已选值，与`format`格式对应.

- defaultValue (list of strings; optional):
    初始化已选值，与`format`格式对应.

- pickerValue (string | list of strings; optional):
    监听或设置面板展开对应日期，与`format`格式对应.

- disabledDatesStrategy (list of dicts; optional):
    配置日期禁用项策略数组，满足策略中至少一项规则的日期将会被禁止选中.

    `disabledDatesStrategy` is a list of dicts with keys:

    - mode (a value equal to: 'eq', 'ne', 'le', 'lt', 'ge', 'gt', 'in', 'not-in', 'in-enumerate-dates', 'not-in-enumerate-dates'; optional):
        当前策略类型，可选项有`'eq'`（等于）、`'ne'`（不等于）、`'le'`（小于等于）、`'lt'`（小于）、`'ge'`（大于等于）
        、`'gt'`（大于）、`'in'`（属于）、`'not-in'`（不属于）、`'in-enumerate-dates'`（属于日期字符串枚举数组），`'not-in-enumerate-dates'`（不属于日期字符串枚举数组）.

    - target (a value equal to: 'day', 'month', 'quarter', 'year', 'dayOfYear', 'dayOfWeek', 'specific-date'; optional):
        当前策略约束目标，可选项有`'dayOfYear'`（按年份天数）、`'dayOfWeek'`（按周天数）、`'day'`（按日）
        、`'month'`（按月份）、`'quarter'`（按季度）、`'year'`（按年份）、`'specific-date'`（具体日期）
        ，其中在`'specific-date'`目标下，`value`值将严格按照`'YYYY-MM-DD'`格式进行解析.

    - value (number | string | list of numbers | list of strings; optional):
        与策略类型、策略约束目标相对应的实际约束值.

- open (boolean; optional):
    监听或设置当前日期范围选择面板是否展开.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- allowClear (boolean; default True):
    是否允许一键清空已选值  默认值：`True`.

- autoFocus (boolean; default False):
    是否自动获取焦点  默认值：`False`.

- readOnly (boolean; optional):
    是否渲染为只读状态  默认值：`False`.

- extraFooter (a list of or a singular dash component, string or number; optional):
    组件型，底部额外区域内容.

- presets (list of dicts; optional):
    配置预设项列表.

    `presets` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，当前预设项标题.

    - value (list of strings; optional):
        当前预设项对应值，与`format`格式对应.

- clickedPreset (dict; optional):
    配合`presets`参数，监听最近一次预设项点击事件相关信息.

    `clickedPreset` is a dict with keys:

    - value (string | number; optional):
        对应预设项值.

    - timestamp (number; optional):
        事件对应时间戳信息.

- needConfirm (boolean; default False):
    是否需要点击按钮确认选值，传入`False`时失去焦点即代表选择  默认值：`False`.

- customCells (list of dicts; optional):
    自定义对应日期的单元格样式.

    `customCells` is a list of dicts with keys:

    - year (number; optional):
        当前项匹配的年份值.

    - month (number; optional):
        当前项匹配的月份值.

    - date (number; optional):
        当前项匹配的日期值.

    - style (dict; optional):
        自定义css样式.

    - className (string; optional):
        自定义css类名.

- prefix (a list of or a singular dash component, string or number; optional):
    组件型，前缀内嵌内容.

- suffixIcon (a list of or a singular dash component, string or number; optional):
    自定义选择框后缀图标内容.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
