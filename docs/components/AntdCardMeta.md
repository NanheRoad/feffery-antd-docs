# AntdCardMeta

## 简介源码：`views/AntdCardMeta/intro.py`
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
                {'title': 'AntdCardMeta 结构化卡片'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCardMeta 结构化卡片', level=2),
        fac.AntdParagraph('用于为卡片添加结构化展示信息。'),
    ]

```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- avatar (a list of or a singular dash component, string or number; optional):
    组件型，头像元素.

- description (a list of or a singular dash component, string or number; optional):
    组件型，描述内容.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
