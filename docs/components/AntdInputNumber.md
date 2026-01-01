# AntdInputNumber

## 简介源码：`views/AntdInputNumber/intro.py`
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
                {'title': 'AntdInputNumber 数值输入框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdInputNumber 数值输入框', level=2),
        fac.AntdParagraph('专门提供数值输入功能的输入框。'),
    ]

```

## 示例源码（demos）

### `views/AntdInputNumber/demos/addon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(
                addonBefore='前缀元素',
                addonAfter='后缀元素',
                style={'width': 300},
            ),
            fac.AntdInputNumber(
                addonBefore=fac.AntdSelect(
                    defaultValue='a',
                    options=[
                        {'label': option, 'value': option}
                        for option in ['a', 'b']
                    ],
                    allowClear=False,
                ),
                addonAfter=fac.AntdSelect(
                    defaultValue='m',
                    options=[
                        {'label': option, 'value': option}
                        for option in ['mm', 'cm', 'dm', 'm']
                    ],
                    allowClear=False,
                ),
                style={'width': 300},
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
        fac.AntdInputNumber(
            addonBefore='前缀元素',
            addonAfter='后缀元素',
            style={'width': 300},
        ),
        fac.AntdInputNumber(
            addonBefore=fac.AntdSelect(
                defaultValue='a',
                options=[
                    {'label': option, 'value': option}
                    for option in ['a', 'b']
                ],
                allowClear=False,
            ),
            addonAfter=fac.AntdSelect(
                defaultValue='m',
                options=[
                    {'label': option, 'value': option}
                    for option in ['mm', 'cm', 'dm', 'm']
                ],
                allowClear=False,
            ),
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdInputNumber/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(id='input-number-demo', style={'width': 200}),
            fac.AntdText(id='input-number-demo-output'),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


@app.callback(
    Output('input-number-demo-output', 'children'),
    Input('input-number-demo', 'value'),
    prevent_initial_call=True,
)
def show_input_number_value(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInputNumber(id='input-number-demo', style={'width': 200}),
        fac.AntdText(id='input-number-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('input-number-demo-output', 'children'),
    Input('input-number-demo', 'value'),
    prevent_initial_call=True,
)
def show_input_number_value(value):
    return f'value: {value}'
"""
    }
]

```

### `views/AntdInputNumber/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        placeholder='请输入数值', style={'width': 100}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    placeholder='请输入数值', style={'width': 100}
)
"""
    }
]

```

### `views/AntdInputNumber/demos/debounce_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(
                id='input-number-debounce-demo',
                debounceWait=500,
                style={'width': 200},
            ),
            fac.AntdText(id='input-number-debounce-demo-output'),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


@app.callback(
    Output('input-number-debounce-demo-output', 'children'),
    Input('input-number-debounce-demo', 'debounceValue'),
    prevent_initial_call=True,
)
def show_input_number_debounce_value(debounceValue):
    return f'debounceValue: {debounceValue}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            id='input-number-debounce-demo',
            debounceWait=500,
            style={'width': 200},
        ),
        fac.AntdText(id='input-number-debounce-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('input-number-debounce-demo-output', 'children'),
    Input('input-number-debounce-demo', 'debounceValue'),
    prevent_initial_call=True,
)
def show_input_number_debounce_value(debounceValue):
    return f'debounceValue: {debounceValue}'
"""
    }
]

```

### `views/AntdInputNumber/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(disabled=True, style={'width': 100})

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(disabled=True, style={'width': 100})
"""
    }
]

```

### `views/AntdInputNumber/demos/limit_min_max.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        min=0,
        max=100,
        placeholder='请尝试输入0~100以外的数值查看效果',
        style={'width': 275},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    min=0,
    max=100,
    placeholder='请尝试输入0~100以外的数值查看效果',
    style={'width': 275},
)
"""
    }
]

```

### `views/AntdInputNumber/demos/precision.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        precision=5, placeholder='precision=5', style={'width': 150}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    precision=5, placeholder='precision=5', style={'width': 150}
)
"""
    }
]

```

### `views/AntdInputNumber/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        prefix=fac.AntdIcon(icon='antd-control'), style={'width': 200}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    prefix=fac.AntdIcon(icon='antd-control'), style={'width': 200}
)
"""
    }
]

```

### `views/AntdInputNumber/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        value=3.1415, readOnly=True, style={'width': 100}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    value=3.1415, readOnly=True, style={'width': 100}
)
"""
    }
]

```

### `views/AntdInputNumber/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(
                placeholder=f'size="{size}"', size=size, style={'width': 150}
            )
            for size in ['small', 'middle', 'large']
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            placeholder=f'size="{size}"', size=size, style={'width': 150}
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdInputNumber/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdInputNumber(status=status) for status in ['warning', 'error']],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdInputNumber(status=status) for status in ['warning', 'error']],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdInputNumber/demos/step.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(
                step=0.1, defaultValue=0, placeholder='step=0.1'
            ),
            fac.AntdInputNumber(
                step=0.001, defaultValue=0, placeholder='step=0.001'
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
        fac.AntdInputNumber(
            step=0.1, defaultValue=0, placeholder='step=0.1'
        ),
        fac.AntdInputNumber(
            step=0.001, defaultValue=0, placeholder='step=0.001'
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdInputNumber/demos/string_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        stringMode=True,
        defaultValue='0.1312312314124123124124123123123312312321312312312312',
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    stringMode=True,
    defaultValue='0.1312312314124123124124123123123312312321312312312312',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdInputNumber/demos/suffix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdInputNumber(
        suffix=fac.AntdIcon(icon='antd-account-book'), style={'width': 200}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdInputNumber(
    suffix=fac.AntdIcon(icon='antd-account-book'), style={'width': 200}
)
"""
    }
]

```

### `views/AntdInputNumber/demos/variant.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInputNumber(
                variant=variant,
                placeholder=f'variant="{variant}"',
                style={'width': 200},
            )
            for variant in ['outlined', 'borderless', 'filled', 'underlined']
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            variant=variant,
            placeholder=f'variant="{variant}"',
            style={'width': 200},
        )
        for variant in ['outlined', 'borderless', 'filled', 'underlined']
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```
