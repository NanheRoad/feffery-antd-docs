# AntdRibbon

## 简介源码：`views/AntdRibbon/intro.py`
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
                {'title': 'AntdRibbon 缎带'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRibbon 缎带', level=2),
        fac.AntdParagraph('用于为容器类元素添加点缀作用的缎带。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRibbon(
            fuc.FefferyDiv(
                shadow='always-shadow',
                style={
                    'height': '200px',
                    'width': '300px',
                    'borderRadius': '10px',
                },
            ),
            text='缎带示例',
        ),
        fac.AntdRibbon(
            fuc.FefferyDiv(
                shadow='always-shadow',
                style={
                    'height': '200px',
                    'width': '300px',
                    'borderRadius': '10px',
                },
            ),
            text='缎带示例',
            placement='start',
            color='#ff4d4f',
        ),
    ],
    direction='vertical',
    size='large',
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，添加徽标的目标元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- color (string; optional):
    缎带颜色.

- placement (a value equal to: 'start', 'end'; default 'end'):
    缎带显示位置，可选项有`'start'`、`'end'`  默认值：`'end'`.

- text (a list of or a singular dash component, string or number; optional):
    组件型，缎带内容.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
