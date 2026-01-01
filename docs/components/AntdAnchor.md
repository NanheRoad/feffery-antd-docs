# AntdAnchor

## 简介源码：`views/AntdAnchor/intro.py`
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
                {'title': translator.t('导航')},
                {'title': translator.t('AntdAnchor 锚点')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdAnchor 锚点'), level=2),
        fac.AntdParagraph(translator.t('用于渲染页面内导航目录。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：最基础的锚点。

#### 代码
```python
[
    fac.AntdAnchor(
        linkDict=[
            {
                'title': '章节1',
                'href': '#章节1',
                'children': [
                    {'title': '章节1-1', 'href': '#章节1-1'},
                    {'title': '章节1-2', 'href': '#章节1-2'},
                ],
            },
            {
                'title': '章节2',
                'href': '#章节2',
                'children': [
                    {'title': '章节2-1', 'href': '#章节2-1'},
                    {'title': '章节2-2', 'href': '#章节2-2'},
                ],
            },
        ],
        align='left',
    ),
    fac.AntdDivider('章节1', id='章节1', innerTextOrientation='right'),
    html.Div(style={'height': 300}),
    fac.AntdDivider(
        '章节1-1', id='章节1-1', innerTextOrientation='right'
    ),
    html.Div(style={'height': 300}),
    fac.AntdDivider(
        '章节1-2', id='章节1-2', innerTextOrientation='right'
    ),
    html.Div(style={'height': 300}),
    fac.AntdDivider('章节2', id='章节2', innerTextOrientation='right'),
    html.Div(style={'height': 300}),
    fac.AntdDivider(
        '章节2-1', id='章节2-1', innerTextOrientation='right'
    ),
    html.Div(style={'height': 300}),
    fac.AntdDivider(
        '章节2-2', id='章节2-2', innerTextOrientation='right'
    ),
    html.Div(style={'height': 300}),
]
```

### 水平锚点

- 说明：设置参数`direction='horizontal'`启用水平方向锚点，注意此模式下锚点不支持嵌套。

#### 代码
```python
[
    fac.AntdAnchor(
        direction='horizontal',
        linkDict=[
            {
                'key': f'章节{i}',
                'title': f'章节{i}',
                'href': f'#章节{i}',
            }
            for i in range(1, 6)
        ],
        align='left',
    ),
    *[
        html.Div(
            fac.AntdDivider(
                f'章节{i}',
                id=f'章节{i}',
                innerTextOrientation='right',
            ),
            style={'paddingBottom': 800},
        )
        for i in range(1, 6)
    ],
    html.Div(style={'height': 300}),
]
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- affix (boolean; default True):
    Whether to enable the affix mode. Default value: `True`.

- align (a value equal to: 'left', 'right'; default 'right'):
    The position of the anchor point, with options `left` or `right`. Default value: `right`.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- bounds (number; default 5):
    The pixel margin for the anchor point. Default value: `5`.

- className (string | dict; optional):
    The CSS class name for the current component, supporting [dynamic CSS class names](/advanced-classname).

- clickedLink (dict; optional):
    Listens for click events on the anchor point node.

- containerId (string; optional):
    The ID of the target container for the anchor point.

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- key (string; optional):
    Updates the `key` value for the current component, which can force a redraw of the component.

- linkDict (optional):
    Hierarchical data structure for the directory.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is currently loading.

    - prop_name (string; optional):
        Holds which property is currently loading.

- offsetTop (number; optional):
    Sets the specified pixel offset from the top of the window to trigger the anchoring effect.

- style (dict; optional):
    The CSS styles for the current component.

- targetOffset (number; optional):
    The offset for the anchor point. Default is the same as the parameter offsetTop.
