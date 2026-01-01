# AntdAffix

## 简介源码：`views/AntdAffix/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '其他'},
                {'title': 'AntdAffix 固钉'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdAffix 固钉', level=2),
        fac.AntdParagraph(
            '确保内部元素原有位置在被用户滚动出视口后，仍然可以在视口范围内保持可见状态。'
        ),
    ]

```

## 示例源码（demos）

### `views/AntdAffix/demos/local_container.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        [
            html.Div(style={'height': '100px'}),
            fac.AntdAffix(
                fac.AntdButton('请在当前局部容器内下滑', danger=True),
                offsetTop=50,
                target='affix-container-demo',
            ),
            html.Div(style={'height': '1000px'}),
        ],
        id='affix-container-demo',
        style={
            'border': '1px solid #f0f0f0',
            'maxHeight': '300px',
            'padding': '10px',
            'overflowY': 'auto',
            'background': '#f8f9fa',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    [
        html.Div(style={'height': '100px'}),
        fac.AntdAffix(
            fac.AntdButton('请在当前局部容器内下滑', danger=True),
            offsetTop=50,
            target='affix-container-demo',
        ),
        html.Div(style={'height': '1000px'}),
    ],
    id='affix-container-demo',
    style={
        'border': '1px solid #f0f0f0',
        'maxHeight': '300px',
        'padding': '10px',
        'overflowY': 'auto',
        'background': '#f8f9fa',
    },
)
"""
    }
]

```

### `views/AntdAffix/demos/offset_bottom.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        fac.AntdAffix(
            fac.AntdButton('向上滑动页面体验固钉效果', type='dashed'),
            offsetBottom=100,
            style={'float': 'right'},
        ),
        style={'marginTop': '1000px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    fac.AntdAffix(
        fac.AntdButton('向上滑动页面体验固钉效果', type='dashed'),
        offsetBottom=100,
        style={'float': 'right'},
    ),
    style={'marginTop': '1000px'},
)
"""
    }
]

```

### `views/AntdAffix/demos/offset_top.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        fac.AntdAffix(
            fac.AntdButton('向下滑动页面体验固钉锚定效果', type='primary'),
            offsetTop=100,
        ),
        style={'marginBottom': '1000px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    fac.AntdAffix(
        fac.AntdButton('向下滑动页面体验固钉锚定效果', type='primary'),
        offsetTop=100,
    ),
    style={'marginBottom': '1000px'},
)
"""
    }
]

```
