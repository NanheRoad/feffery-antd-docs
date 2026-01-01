# AntdDescriptionItem

## 简介源码：`views/AntdDescriptionItem/intro.py`
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
                {'title': '描述列表'},
                {'title': 'AntdDescriptionItem 描述列表子项'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDescriptionItem 描述列表子项', level=2),
        fac.AntdParagraph('在描述列表中构建单个描述列表子项。'),
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

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - label (dict; optional):
        标签元素css样式.

    - content (dict; optional):
        内容元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - label (string; optional):
        标签元素css类名.

    - content (string; optional):
        内容元素css类名.

- label (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- span (number; default 1):
    所占宽度份数  默认值：`1`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
