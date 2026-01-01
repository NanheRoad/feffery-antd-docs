# AntdCollapse

## 简介源码：`views/AntdCollapse/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdCollapse 折叠面板'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCollapse 折叠面板', level=2),
        fac.AntdParagraph('可折叠展开的特殊容器。'),
    ]

```

## 示例源码（demos）

### `views/AntdCollapse/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdParagraph('内容示例' * 20),
                id='collapse-demo',
                isOpen=True,
                title='回调示例',
                style={'width': 300},
            ),
            fac.AntdText(id='collapse-demo-output'),
        ],
        direction='vertical',
    )

    return demo_contents


@app.callback(
    Output('collapse-demo-output', 'children'), Input('collapse-demo', 'isOpen')
)
def collapse_demo(isOpen):
    return f'isOpen={isOpen}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            id='collapse-demo',
            isOpen=True,
            title='回调示例',
            style={'width': 300},
        ),
        fac.AntdText(id='collapse-demo-output'),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('collapse-demo-output', 'children'), Input('collapse-demo', 'isOpen')
)
def collapse_demo(isOpen):
    return f'isOpen={isOpen}'
"""
    }
]

```

### `views/AntdCollapse/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCollapse(
        fac.AntdParagraph('内容示例' * 20),
        title='折叠面板示例',
        style={'width': 300},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    title='折叠面板示例',
    style={'width': 300},
)
"""
    }
]

```

### `views/AntdCollapse/demos/collapsible.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdParagraph('内容示例' * 20),
                title='collapsible="header"',
                collapsible='header',
                isOpen=False,
                style={'width': 300},
            ),
            fac.AntdCollapse(
                fac.AntdParagraph('内容示例' * 20),
                title='collapsible="disabled"',
                collapsible='disabled',
                isOpen=False,
                style={'width': 300},
            ),
            fac.AntdCollapse(
                fac.AntdParagraph('内容示例' * 20),
                title='collapsible="icon"',
                collapsible='icon',
                isOpen=False,
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
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="header"',
            collapsible='header',
            isOpen=False,
            style={'width': 300},
        ),
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="disabled"',
            collapsible='disabled',
            isOpen=False,
            style={'width': 300},
        ),
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="icon"',
            collapsible='icon',
            isOpen=False,
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdCollapse/demos/force_render.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider(
            'forceRender=False（默认）', innerTextOrientation='left'
        ),
        fac.AntdSpace(
            [
                fac.AntdCollapse(
                    fac.AntdInput(
                        id='collapse-child-demo1',
                        defaultValue='内容测试',
                        style={'width': '100%'},
                    ),
                    isOpen=False,
                    style={'width': 300},
                ),
                fac.AntdText(id='collapse-child-demo1-output'),
            ]
        ),
        fac.AntdDivider('forceRender=True', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdCollapse(
                    fac.AntdInput(
                        id='collapse-child-demo2',
                        defaultValue='内容测试',
                        style={'width': '100%'},
                    ),
                    isOpen=False,
                    forceRender=True,
                    style={'width': 300},
                ),
                fac.AntdText(id='collapse-child-demo2-output'),
            ]
        ),
    ]

    return demo_contents


@app.callback(
    Output('collapse-child-demo1-output', 'children'),
    Input('collapse-child-demo1', 'value'),
)
def collapse_child_demo1(value):
    return value


@app.callback(
    Output('collapse-child-demo2-output', 'children'),
    Input('collapse-child-demo2', 'value'),
)
def collapse_child_demo2(value):
    return value


code_string = [
    {
        'code': """
[
    fac.AntdDivider(
        'forceRender=False（默认）', innerTextOrientation='left'
    ),
    fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdInput(
                    id='collapse-child-demo1',
                    defaultValue='内容测试',
                    style={'width': '100%'},
                ),
                isOpen=False,
                style={'width': 300},
            ),
            fac.AntdText(id='collapse-child-demo1-output'),
        ]
    ),
    fac.AntdDivider('forceRender=True', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdInput(
                    id='collapse-child-demo2',
                    defaultValue='内容测试',
                    style={'width': '100%'},
                ),
                isOpen=False,
                forceRender=True,
                style={'width': 300},
            ),
            fac.AntdText(id='collapse-child-demo2-output'),
        ]
    ),
]

...

@app.callback(
    Output('collapse-child-demo1-output', 'children'),
    Input('collapse-child-demo1', 'value'),
)
def collapse_child_demo1(value):
    return value


@app.callback(
    Output('collapse-child-demo2-output', 'children'),
    Input('collapse-child-demo2', 'value'),
)
def collapse_child_demo2(value):
    return value
"""
    }
]

```

### `views/AntdCollapse/demos/ghost.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20), ghost=True, title='折叠面板示例'
        ),
        style={'background': '#e7f5ff', 'width': 300},
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    fac.AntdCollapse(
        fac.AntdParagraph('内容示例' * 20), ghost=True, title='折叠面板示例'
    ),
    style={'background': '#e7f5ff', 'width': 300},
)
"""
    }
]

```

### `views/AntdCollapse/demos/is_open.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCollapse(
        fac.AntdParagraph('内容示例' * 20),
        isOpen=False,
        title='折叠面板示例',
        style={'width': 300},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    isOpen=False,
    title='折叠面板示例',
    style={'width': 300},
)
"""
    }
]

```

### `views/AntdCollapse/demos/non_bordered.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCollapse(
        fac.AntdParagraph('内容示例' * 20),
        bordered=False,
        title='折叠面板示例',
        style={'width': 300},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    bordered=False,
    title='折叠面板示例',
    style={'width': 300},
)
"""
    }
]

```

### `views/AntdCollapse/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdParagraph('内容示例' * 20),
                title=f'size="{size}"',
                size=size,
                isOpen=False,
                style={'width': 300},
            )
            for size in ['small', 'middle', 'large']
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
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title=f'size="{size}"',
            style={'width': 300},
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```
