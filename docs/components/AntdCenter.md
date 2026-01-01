# AntdCenter

## 简介源码：`views/AntdCenter/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('布局')},
                {'title': translator.t('AntdCenter 居中')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCenter 居中'), level=2),
        fac.AntdParagraph(translator.t('快捷实现内容在水平垂直方向上居中。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 样式自动联动参数配置组件

- 说明：设置`inheritStyleToken=True`后，背景色、字体尺寸、文字颜色默认值自动联动上层的[参数配置组件](/AntdConfigProvider)相关设定。

#### 代码
```python
fac.AntdConfigProvider(
    [
        fac.AntdCenter(
            'demo1', inheritStyleToken=True, style={'height': 200}
        ),
        fac.AntdCenter(
            'demo2',
            inheritStyleToken=True,
            style={'height': 200, 'fontSize': 24, 'color': '#ffffb8'},
        ),
    ],
    algorithm='dark',
    token={'colorTextBase': '#d3adf7', 'fontSize': 56},
)
```

### 基础使用

- 说明：常规居中与行内居中。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCenter(
            '常规居中',
            style={'width': 300, 'height': 150, 'background': '#f0f0f0'},
        ),
        fac.AntdParagraph(
            [
                '测试内容',
                fac.AntdCenter(
                    '行内居中',
                    style={
                        'width': 100,
                        'height': 100,
                        'background': '#f0f0f0',
                    },
                    inline=True,
                ),
                '测试内容',
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
    Component type, nested elements.

- id (string; optional):
    Unique ID for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- inline (boolean; default False):
    Whether to render as an inline element. Default value: `False`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- style (dict; optional):
    CSS styles for the current component.
