# AntdPopconfirm

## 简介源码：`views/AntdPopconfirm/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '反馈'},
                {'title': 'AntdPopconfirm 气泡确认框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdPopconfirm 气泡确认框', level=2),
        fac.AntdParagraph('用于实现二次确认功能，相较于对话框更加简便。'),
    ]

```

## 示例源码（demos）

### `views/AntdPopconfirm/demos/basic_callbacks.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdPopconfirm(
                fac.AntdButton('触发'), id='popconfirm-demo', title='确认继续'
            ),
            html.Pre(id='popconfirm-demo-output'),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    Output('popconfirm-demo-output', 'children'),
    Input('popconfirm-demo', 'confirmCounts'),
    Input('popconfirm-demo', 'cancelCounts'),
    prevent_initial_call=True,
)
def popconfirm_callback_demo(confirmCounts, cancelCounts):
    return json.dumps(
        {'confirmCounts': confirmCounts, 'cancelCounts': cancelCounts}, indent=4
    )


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdPopconfirm(
            fac.AntdButton('触发'), id='popconfirm-demo', title='确认继续'
        ),
        html.Pre(id='popconfirm-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('popconfirm-demo-output', 'children'),
    Input('popconfirm-demo', 'confirmCounts'),
    Input('popconfirm-demo', 'cancelCounts'),
    prevent_initial_call=True,
)
def popconfirm_callback_demo(confirmCounts, cancelCounts):
    return json.dumps(
        {'confirmCounts': confirmCounts, 'cancelCounts': cancelCounts}, indent=4
    )
"""
    }
]

```

### `views/AntdPopconfirm/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopconfirm(fac.AntdButton('触发'), title='确认继续')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopconfirm(fac.AntdButton('触发'), title='确认继续')
"""
    }
]

```

### `views/AntdPopconfirm/demos/color.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fuc.FefferyHexColorPicker(
                id='popover-color-demo-input', showAlpha=True, color='#f6f7f866'
            ),
            fac.AntdPopover(
                fac.AntdButton('锚点示例'),
                id='popover-color-demo',
                title='气泡卡片示例',
            ),
        ]
    )

    return demo_contents


@app.callback(
    [
        Output('popover-color-demo', 'color'),
        Output('popover-color-demo', 'content'),
    ],
    Input('popover-color-demo-input', 'color'),
)
def popover_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='popover-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdPopover(
            fac.AntdButton('锚点示例'),
            id='popover-color-demo',
            title='气泡卡片示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('popover-color-demo', 'color'),
        Output('popover-color-demo', 'content'),
    ],
    Input('popover-color-demo-input', 'color'),
)
def popover_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]
"""
    }
]

```

### `views/AntdPopconfirm/demos/control_open.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(id='popconfirm-open-switch', checked=False),
            fac.AntdPopconfirm(
                fac.AntdButton('触发'),
                id='popconfirm-open-demo',
                title='确认继续',
            ),
        ]
    )

    return demo_contents


@app.callback(
    Output('popconfirm-open-demo', 'open'),
    Input('popconfirm-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_popconfirm_open(checked):
    return checked


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(id='popconfirm-open-switch', checked=False),
        fac.AntdPopconfirm(
            fac.AntdButton('触发'),
            id='popconfirm-open-demo',
            title='确认继续',
        ),
    ]
)

...

@app.callback(
    Output('popconfirm-open-demo', 'open'),
    Input('popconfirm-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_popconfirm_open(checked):
    return checked
"""
    }
]

```

### `views/AntdPopconfirm/demos/custom_description.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopconfirm(
        fac.AntdButton('触发'), title='确认继续', description='描述信息示例'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', description='描述信息示例'
)
"""
    }
]

```

### `views/AntdPopconfirm/demos/custom_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopconfirm(
        fac.AntdButton('触发'), title='确认继续', icon='🤔'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', icon='🤔'
)
"""
    }
]

```

### `views/AntdPopconfirm/demos/custom_style.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopconfirm(
        fac.AntdButton('触发'),
        title='确认继续',
        description='内容示例' * 10,
        styles={'root': {'width': 400}},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopconfirm(
    fac.AntdButton('触发'),
    title='确认继续',
    description='内容示例' * 10,
    styles={'root': {'width': 400}},
)
"""
    }
]

```

### `views/AntdPopconfirm/demos/hide_arrow.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopconfirm(
        fac.AntdButton('触发'), title='确认继续', arrow='hide'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', arrow='hide'
)
"""
    }
]

```

### `views/AntdPopconfirm/demos/placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdPopconfirm(
                fac.AntdButton(placement),
                title='确认继续',
                description=f'placement="{placement}"',
                placement=placement,
            )
            for placement in [
                'top',
                'left',
                'right',
                'bottom',
                'topLeft',
                'topRight',
                'bottomLeft',
                'bottomRight',
                'leftTop',
                'leftBottom',
                'rightTop',
                'rightBottom',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdPopconfirm(
            fac.AntdButton(placement),
            title='确认继续',
            description=f'placement="{placement}"',
            placement=placement,
        )
        for placement in [
            'top',
            'left',
            'right',
            'bottom',
            'topLeft',
            'topRight',
            'bottomLeft',
            'bottomRight',
            'leftTop',
            'leftBottom',
            'rightTop',
            'rightBottom',
        ]
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdPopconfirm/demos/question_with_absolute_position.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        [
            html.Span(
                fac.AntdPopconfirm(
                    fac.AntdButton('示例1', type='primary'),
                    title='示例',
                ),
                style={'position': 'absolute', 'left': 15, 'bottom': 15},
            ),
            html.Span(
                fac.AntdPopconfirm(
                    fac.AntdButton('示例2', type='primary'),
                    title='示例',
                ),
                style={'position': 'absolute', 'right': 15, 'top': 15},
            ),
            html.Span(
                fac.AntdPopconfirm(
                    fac.AntdButton('示例3', type='primary'),
                    title='示例',
                ),
                style={'position': 'absolute', 'right': 15, 'bottom': 15},
            ),
        ],
        style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    [
        html.Span(
            fac.AntdPopconfirm(
                fac.AntdButton('示例1', type='primary'),
                title='示例',
            ),
            style={'position': 'absolute', 'left': 15, 'bottom': 15},
        ),
        html.Span(
            fac.AntdPopconfirm(
                fac.AntdButton('示例2', type='primary'),
                title='示例',
            ),
            style={'position': 'absolute', 'right': 15, 'top': 15},
        ),
        html.Span(
            fac.AntdPopconfirm(
                fac.AntdButton('示例3', type='primary'),
                title='示例',
            ),
            style={'position': 'absolute', 'right': 15, 'bottom': 15},
        ),
    ],
    style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
)
"""
    }
]

```
