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

## 示例代码片段（仅保留演示内容）

### local_container

- 说明：演示 local_container 的用法。

#### 代码
```python
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
```

### offset_bottom

- 说明：演示 offset_bottom 的用法。

#### 代码
```python
html.Div(
    fac.AntdAffix(
        fac.AntdButton('向上滑动页面体验固钉效果', type='dashed'),
        offsetBottom=100,
        style={'float': 'right'},
    ),
    style={'marginTop': '1000px'},
)
```

### offset_top

- 说明：演示 offset_top 的用法。

#### 代码
```python
html.Div(
    fac.AntdAffix(
        fac.AntdButton('向下滑动页面体验固钉锚定效果', type='primary'),
        offsetTop=100,
    ),
    style={'marginBottom': '1000px'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- offsetBottom (number; optional):
    触发固钉效果的视窗底部距离像素阈值.

- offsetTop (number; default 0):
    触发固钉效果的视窗顶部距离像素阈值  默认值：`0`.

- target (string; optional):
    滚动事件监听的特定目标容器id.

- affixed (boolean; optional):
    监听当前目标是否已触发固定.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
