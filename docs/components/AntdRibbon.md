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
