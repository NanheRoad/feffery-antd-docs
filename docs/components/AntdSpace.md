# AntdSpace

## 简介源码：`views/AntdSpace/intro.py`
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
                {'title': translator.t('AntdSpace 排列')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdSpace 排列'), level=2),
        fac.AntdParagraph(
            translator.t('用于快捷对一组元素进行水平或竖直方向上的规整排列。')
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 对齐方式

- 说明：不同的子元素对齐方式。

#### 代码
```python
[
    fac.AntdRadioGroup(
        id='space-align-demo-align',
        options=['start', 'end', 'center', 'baseline'],
        value='start',
    ),
    fac.AntdParagraph('水平方向：'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '25px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '10px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-horizontal',
        align='start',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
    fac.AntdParagraph('竖直方向：'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '50px',
                    'width': '25px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-vertical',
        align='start',
        direction='vertical',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
]

...

@app.callback(
    Output('space-align-demo-horizontal', 'align'),
    Output('space-align-demo-vertical', 'align'),
    Input('space-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value, value
```

### 基础使用

- 说明：**AntdSpace**可以视作页面元素排列的快捷方式，用于解决基础的多个组件水平方向或竖直方向上单一的等间距排列需求，更复杂的网格排列布局需求请前往**AntdRow/AntdCol**进行进一步学习。

#### 代码
```python
[
    fac.AntdDivider('水平方向（默认）', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3
    ),
    fac.AntdDivider('竖直方向', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3,
        direction='vertical',
    ),
]
```

### 自定义分割线

- 说明：分割线可设置为任意的内容。

#### 代码
```python
fac.AntdSpace(
    [
        html.Div(
            style={
                'backgroundColor': 'rgba(64, 173, 255, 1)',
                'height': '50px',
                'width': '50px',
            }
        )
    ]
    * 3,
    customSplit=html.Div(
        style={'height': 30, 'borderRight': '1px dashed #8c8c8c'}
    ),
)
```

### 间距大小

- 说明：控制子元素间的间距大小。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='space-size-demo-size',
            options=['small', 'middle', 'large', '66'],
            value='small',
        ),
        fac.AntdSpace(
            [fac.AntdButton('child', type='primary')] * 4,
            id='space-size-demo',
        ),
    ],
    direction='vertical',
    size='large',
    style={'width': '100%'},
)

...

@app.callback(
    Output('space-size-demo', 'size'),
    Input('space-size-demo-size', 'value'),
)
def update_demo_size(value):
    if value == '66':
        return 66

    return value
```

### 添加分割线

- 说明：水平排列下可在子元素之间添加分割线。

#### 代码
```python
fac.AntdSpace(
    [
        html.Div(
            style={
                'backgroundColor': 'rgba(64, 173, 255, 1)',
                'height': '50px',
                'width': '50px',
            }
        )
    ]
    * 3,
    addSplitLine=True,
)
```

### 自动换行

- 说明：控制子元素超宽后是否自动换行。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdButton('child', type='primary')] * 25, wrap=True
)
```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
    Component type, embedded elements.

- id (string; optional):
    Unique ID for the component.

- addSplitLine (boolean; default False):
    Whether to add a separator line. Default value: `False`.

- align (a value equal to: 'start', 'end', 'center', 'baseline'; optional):
    Alignment method, with options `start`, `end`, `center`, `baseline`.

- aria-* (string; optional):
    Wildcard for `aria-*` attribute format.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- classNames (dict; optional):
    Fine-grained control over the CSS classes of child elements.

    `classNames` is a dict with keys:

    - item (string; optional):
        CSS class for the child item container element.

- customSplit (a list of or a singular dash component, string or number; optional):
    Custom separator line element.

- data-* (string; optional):
    Wildcard for `data-*` attribute format.

- direction (a value equal to: 'vertical', 'horizontal'; default 'horizontal'):
    Layout direction, with options `vertical`, `horizontal`. Default value: `horizontal`.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- loading_state (dict; optional):

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is currently loading.

    - prop_name (string; optional):
        Holds which property is currently loading.

- size (a value equal to: 'small', 'middle', 'large' | number; default 'small'):
    Spacing between child elements, with options `small`, `middle`, `large`, or a numeric value representing pixel spacing.
    Default value: `small`.

- style (dict; optional):
    The CSS style for the current component.

- styles (dict; optional):
    Fine-grained control over the CSS styles of child elements.

    `styles` is a dict with keys:

    - item (dict; optional):
        CSS style for the child item container element.

- wrap (boolean; default False):
    Whether child elements automatically wrap to the next line, only effective when `direction='horizontal'`. Default value: `False`.
