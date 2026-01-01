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

## 示例源码（demos）

### `views/AntdTimeRangePicker/demos/_12_hours.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(use12Hours=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(use12Hours=True)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/basic_callbacks.py`
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        placeholder=['开始时间', '结束时间']
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    placeholder=['开始时间', '结束时间']
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/custom_format.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(format='HH时mm分ss秒')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(format='HH时mm分ss秒')
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/different_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/extra_footer.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        placeholder=['开始时间', '结束时间'],
        extraFooter=fac.AntdText('底部额外内容示例'),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    placeholder=['开始时间', '结束时间'],
    extraFooter=fac.AntdText('底部额外内容示例'),
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        defaultValue=['11:00:00', '12:00:00'],
        prefix=fac.AntdIcon(icon='antd-user'),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    defaultValue=['11:00:00', '12:00:00'],
    prefix=fac.AntdIcon(icon='antd-user'),
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        readOnly=True, defaultValue=['11:00:00', '12:00:00']
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    readOnly=True, defaultValue=['11:00:00', '12:00:00']
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeRangePicker(status='warning'),
            fac.AntdTimeRangePicker(status='error'),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdTimeRangePicker(status='warning'),
        fac.AntdTimeRangePicker(status='error'),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/suffix_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        defaultValue=['11:00:00', '12:00:00'],
        suffixIcon=fac.AntdIcon(icon='antd-user'),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    defaultValue=['11:00:00', '12:00:00'],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
"""
    }
]

```

### `views/AntdTimeRangePicker/demos/time_step.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTimeRangePicker(
        hourStep=3, minuteStep=10, secondStep=20
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTimeRangePicker(
    hourStep=3, minuteStep=10, secondStep=20
)
"""
    }
]

```
