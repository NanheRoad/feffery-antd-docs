# AntdSkeletonInput

## 简介源码：`views/AntdSkeletonInput/intro.py`
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
                {'title': '骨架屏'},
                {'title': 'AntdSkeletonInput 输入框占位图'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSkeletonInput 输入框占位图', level=2),
        fac.AntdParagraph('用于在自定义骨架屏中构建输入框占位相关内容。'),
    ]

```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- active (boolean; default False):
    是否显示动画  默认值：`False`.

- size (a value equal to: 'large', 'small', 'default'; default 'default'):
    输入框占位图尺寸，可选项有`'large'`、`'small'`、`'default'`  默认值：`'default'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
