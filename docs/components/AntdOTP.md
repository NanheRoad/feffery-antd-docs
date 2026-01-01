# AntdOTP

## 简介源码：`views/AntdOTP/intro.py`
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
                {'title': 'AntdOTP 一次性密码框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdOTP 一次性密码框', level=2),
        fac.AntdParagraph('用于提供验证码等一次性固定位数密码输入功能。'),
    ]

```

## 示例源码（demos）

### `views/AntdOTP/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdOTP(id='otp-demo'),
            fac.AntdText(id='otp-demo-output'),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


@app.callback(
    Output('otp-demo-output', 'children'),
    Input('otp-demo', 'value'),
    prevent_initial_call=True,
)
def show_otp_value(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdOTP(id='otp-demo'),
        fac.AntdText(id='otp-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('otp-demo-output', 'children'),
    Input('otp-demo', 'value'),
    prevent_initial_call=True,
)
def show_otp_value(value):
    return f'value: {value}'
"""
    }
]

```

### `views/AntdOTP/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdOTP()

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdOTP()
"""
    }
]

```

### `views/AntdOTP/demos/custom_display_character.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdOTP(mask='🔒')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdOTP(mask='🔒')
"""
    }
]

```

### `views/AntdOTP/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdOTP(disabled=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdOTP(disabled=True)
"""
    }
]

```

### `views/AntdOTP/demos/length.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdOTP(length=i) for i in range(3, 10)], direction='vertical'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdOTP(length=i) for i in range(3, 10)], direction='vertical'
)
"""
    }
]

```

### `views/AntdOTP/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('size="small"', innerTextOrientation='left'),
            fac.AntdOTP(size='small'),
            fac.AntdDivider(
                'size="middle"（默认）', innerTextOrientation='left'
            ),
            fac.AntdOTP(),
            fac.AntdDivider('size="large"', innerTextOrientation='left'),
            fac.AntdOTP(size='large'),
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
        fac.AntdDivider('size="small"', innerTextOrientation='left'),
        fac.AntdOTP(size='small'),
        fac.AntdDivider(
            'size="middle"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(),
        fac.AntdDivider('size="large"', innerTextOrientation='left'),
        fac.AntdOTP(size='large'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdOTP/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdOTP(status=status) for status in ['warning', 'error']],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdOTP(status=status) for status in ['warning', 'error']],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdOTP/demos/variant.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider(
                'variant="outlined"（默认）', innerTextOrientation='left'
            ),
            fac.AntdOTP(variant='outlined'),
            fac.AntdDivider(
                'variant="borderless"', innerTextOrientation='left'
            ),
            fac.AntdOTP(variant='borderless'),
            fac.AntdDivider('variant="filled"', innerTextOrientation='left'),
            fac.AntdOTP(variant='filled'),
            fac.AntdDivider(
                'variant="underlined"', innerTextOrientation='left'
            ),
            fac.AntdOTP(variant='underlined'),
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
        fac.AntdDivider(
            'variant="outlined"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='outlined'),
        fac.AntdDivider(
            'variant="borderless"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='borderless'),
        fac.AntdDivider('variant="filled"', innerTextOrientation='left'),
        fac.AntdOTP(variant='filled'),
        fac.AntdDivider(
            'variant="underlined"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='underlined'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```
