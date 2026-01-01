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
