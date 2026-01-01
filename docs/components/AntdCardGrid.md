# AntdCardGrid

## 简介源码：`views/AntdCardGrid/intro.py`
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
                {'title': '卡片'},
                {'title': 'AntdCardGrid 卡片网格'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCardGrid 卡片网格', level=2),
        fac.AntdParagraph('用于构建内嵌的网格布局卡片。'),
    ]

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

- hoverable (boolean; default True):
    鼠标悬停时是否显示特殊样式  默认值：`True`.

- nClicks (number; default 0):
    监听当前卡片网格累计点击次数  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
