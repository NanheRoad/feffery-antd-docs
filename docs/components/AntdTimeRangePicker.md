# AntdTimeRangePicker

## 简介源码：`views/AntdTimeRangePicker/intro.py`
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
                {'title': 'AntdTimeRangePicker 时间范围选择'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTimeRangePicker 时间范围选择', level=2),
        fac.AntdParagraph('提供常用的时间范围选择功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### _12_hours

- 说明：演示 _12_hours 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(use12Hours=True)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdTimeRangePicker(
                    id='time-range-picker-demo',
                    defaultValue=['12:00:00', '13:00:00'],
                ),
                fac.AntdText(id='time-range-picker-demo-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdTimeRangePicker(
                    id='time-range-picker-format-demo',
                    defaultValue=['12时00分00秒', '13时00分00秒'],
                    format='HH时mm分ss秒',
                ),
                fac.AntdText(id='time-range-picker-format-demo-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('time-range-picker-demo-output', 'children'),
    Input('time-range-picker-demo', 'value'),
)
def time_range_picker_demo(value):
    return f'value: {value}'


@app.callback(
    Output('time-range-picker-format-demo-output', 'children'),
    Input('time-range-picker-format-demo', 'value'),
)
def time_range_picker_format_demo(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    placeholder=['开始时间', '结束时间']
)
```

### custom_format

- 说明：演示 custom_format 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(format='HH时mm分ss秒')
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTimeRangePicker(
            placeholder=['placement=', f'"{placement}"'],
            placement=placement,
            style={'width': 300},
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
        fac.AntdTimeRangePicker(
            placeholder=['开始时间', '结束时间'], disabled=[True, True]
        ),
        fac.AntdTimeRangePicker(
            placeholder=['开始时间', '结束时间'],
            disabled=[True, False],
            defaultValue=['12:00:00', ''],
        ),
        fac.AntdTimeRangePicker(
            placeholder=['开始时间', '结束时间'],
            disabled=[False, True],
            defaultValue=['', '12:00:00'],
        ),
    ],
    direction='vertical',
)
```

### extra_footer

- 说明：演示 extra_footer 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    placeholder=['开始时间', '结束时间'],
    extraFooter=fac.AntdText('底部额外内容示例'),
)
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    defaultValue=['11:00:00', '12:00:00'],
    prefix=fac.AntdIcon(icon='antd-user'),
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    readOnly=True, defaultValue=['11:00:00', '12:00:00']
)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTimeRangePicker(status='warning'),
        fac.AntdTimeRangePicker(status='error'),
    ],
    direction='vertical',
)
```

### suffix_icon

- 说明：演示 suffix_icon 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    defaultValue=['11:00:00', '12:00:00'],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
```

### time_step

- 说明：演示 time_step 的用法。

#### 代码
```python
fac.AntdTimeRangePicker(
    hourStep=3, minuteStep=10, secondStep=20
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

- format (string; default 'HH:mm:ss'):
    时间显示格式，[参考资料](https://day.js.org/docs/en/display/format)
    默认值：`'HH:mm:ss'`.

- hourStep (number; default 1):
    小时选项间隔  默认值：`1`.

- minuteStep (number; default 1):
    分钟选项间隔  默认值：`1`.

- secondStep (number; default 1):
    秒选项间隔  默认值：`1`.

- use12Hours (boolean; default False):
    是否使用12小时制，当设置为`True`时，`format`参数默认值变更为`'h:mm:ss a'`  默认值：`False`.

- allowClear (boolean; default True):
    是否允许一键清空已选值  默认值：`True`.

- autoFocus (boolean; default False):
    是否自动获取焦点  默认值：`False`.

- placeholder (list of strings; optional):
    输入框占位文字内容.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):
    选择面板展开方向，可选项有`'bottomLeft'`、`'bottomRight'`、`'topLeft'`、`'topRight'`
    默认值：`'bottomLeft'`.

- disabled (list of booleans; default [False, False]):
    是否禁用当前组件  默认值：`False`.

- value (list of strings; optional):
    监听或设置已选值，与`format`格式对应.

- defaultValue (list of strings; optional):
    初始化已选值，与`format`格式对应.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- open (boolean; optional):
    监听或设置当前选择面板是否展开.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- readOnly (boolean; optional):
    是否渲染为只读状态  默认值：`False`.

- extraFooter (a list of or a singular dash component, string or number; optional):
    组件型，底部额外区域内容.

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

- needConfirm (boolean; default False):
    是否需要确认按钮，为`False`时失去焦点即代表选择  默认值：`False`.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
