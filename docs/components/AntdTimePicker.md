# AntdTimePicker

## 简介源码：`views/AntdTimePicker/intro.py`
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
                {'title': 'AntdTimePicker 时间选择'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTimePicker 时间选择', level=2),
        fac.AntdParagraph('提供常用的时间选择功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### _12_hours

- 说明：演示 _12_hours 的用法。

#### 代码
```python
fac.AntdTimePicker(use12Hours=True)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdTimePicker(
                    id='time-picker-demo', defaultValue='06:00:00'
                ),
                fac.AntdText(id='time-picker-demo-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdTimePicker(
                    id='time-picker-format-demo',
                    defaultValue='06时00分00秒',
                    format='HH时mm分ss秒',
                ),
                fac.AntdText(id='time-picker-format-demo-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('time-picker-demo-output', 'children'),
    Input('time-picker-demo', 'value'),
)
def time_picker_demo(value):
    return f'value: {value}'


@app.callback(
    Output('time-picker-format-demo-output', 'children'),
    Input('time-picker-format-demo', 'value'),
)
def time_picker_format_demo(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTimePicker(placeholder='请选择时间')
```

### custom_format

- 说明：演示 custom_format 的用法。

#### 代码
```python
fac.AntdTimePicker(
    format='HH点mm分ss秒', defaultValue='12点18分17秒'
)
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTimePicker(
            placement=placement,
            placeholder=f'placement="{placement}"',
            style={'width': 220},
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
fac.AntdTimePicker(defaultValue='12:00:19', disabled=True)
```

### extra_footer

- 说明：演示 extra_footer 的用法。

#### 代码
```python
fac.AntdTimePicker(
    extraFooter=fac.AntdText('底部额外内容示例')
)
```

### hide_now

- 说明：演示 hide_now 的用法。

#### 代码
```python
fac.AntdTimePicker(placeholder='请选择时间', showNow=False)
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdTimePicker(
    defaultValue='12:00:19', prefix=fac.AntdIcon(icon='antd-user')
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdTimePicker(defaultValue='12:00:19', readOnly=True)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTimePicker(
            placeholder='status="warning"',
            status='warning',
            style={'width': 200},
        ),
        fac.AntdTimePicker(
            placeholder='status="error"',
            status='error',
            style={'width': 200},
        ),
    ],
    direction='vertical',
)
```

### suffix_icon

- 说明：演示 suffix_icon 的用法。

#### 代码
```python
fac.AntdTimePicker(
    defaultValue='12:00:19', suffixIcon=fac.AntdIcon(icon='antd-user')
)
```

### time_step

- 说明：演示 time_step 的用法。

#### 代码
```python
fac.AntdTimePicker(hourStep=3, minuteStep=10, secondStep=20)
```
