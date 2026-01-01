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

## 示例源码（demos）

### `views/AntdTimePicker/demos/_12_hours.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(use12Hours=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(use12Hours=True)
"""
    }
]

```

### `views/AntdTimePicker/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimePicker/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(placeholder='请选择时间')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(placeholder='请选择时间')
"""
    }
]

```

### `views/AntdTimePicker/demos/custom_format.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(
        format='HH点mm分ss秒', defaultValue='12点18分17秒'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(
    format='HH点mm分ss秒', defaultValue='12点18分17秒'
)
"""
    }
]

```

### `views/AntdTimePicker/demos/different_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimePicker/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(defaultValue='12:00:19', disabled=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(defaultValue='12:00:19', disabled=True)
"""
    }
]

```

### `views/AntdTimePicker/demos/extra_footer.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(
        extraFooter=fac.AntdText('底部额外内容示例')
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(
    extraFooter=fac.AntdText('底部额外内容示例')
)
"""
    }
]

```

### `views/AntdTimePicker/demos/hide_now.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(placeholder='请选择时间', showNow=False)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(placeholder='请选择时间', showNow=False)
"""
    }
]

```

### `views/AntdTimePicker/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(
        defaultValue='12:00:19', prefix=fac.AntdIcon(icon='antd-user')
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(
    defaultValue='12:00:19', prefix=fac.AntdIcon(icon='antd-user')
)
"""
    }
]

```

### `views/AntdTimePicker/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(defaultValue='12:00:19', readOnly=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(defaultValue='12:00:19', readOnly=True)
"""
    }
]

```

### `views/AntdTimePicker/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimePicker/demos/suffix_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(
        defaultValue='12:00:19', suffixIcon=fac.AntdIcon(icon='antd-user')
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(
    defaultValue='12:00:19', suffixIcon=fac.AntdIcon(icon='antd-user')
)
"""
    }
]

```

### `views/AntdTimePicker/demos/time_step.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimePicker(hourStep=3, minuteStep=10, secondStep=20)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimePicker(hourStep=3, minuteStep=10, secondStep=20)
"""
    }
]

```
