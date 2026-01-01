# AntdFlex

## 简介源码：`views/AntdFlex/intro.py`
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
                {'title': translator.t('AntdFlex 弹性布局')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdFlex 弹性布局'), level=2),
        fac.AntdParagraph(
            translator.t(
                '基于css中的flex布局原理，对一组元素进行水平或垂直方向上的排列。'
            )
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 对齐方式

- 说明：通过参数`justify`与`align`控制不同方向上的对齐方式。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdText('justify:'),
        fac.AntdRadioGroup(
            id='flex-align-demo-justify',
            options=[
                'flex-start',
                'center',
                'flex-end',
                'space-between',
                'space-around',
                'space-evenly',
            ],
            value='flex-start',
        ),
        fac.AntdText('align:'),
        fac.AntdRadioGroup(
            id='flex-align-demo-align',
            options=['flex-start', 'center', 'flex-end'],
            value='flex-start',
        ),
        fac.AntdFlex(
            [fac.AntdButton('子元素', type='primary')] * 4,
            id='flex-align-demo',
            style={
                'width': '100%',
                'height': 200,
                'borderRadius': 6,
                'border': '1px solid #40a9ff',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('flex-align-demo', 'justify'),
    Input('flex-align-demo-justify', 'value'),
)
def update_demo_justify(value):
    return value


@app.callback(
    Output('flex-align-demo', 'align'),
    Input('flex-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value
```

### 基础使用

- 说明：基础的水平排布与垂直排布。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdText('水平排布（默认）'),
        fac.AntdFlex(
            [
                html.Div(
                    style={
                        'width': '25%',
                        'height': 48,
                        'background': '#1677ff'
                        if i % 2 == 0
                        else '#1677ffbf',
                    }
                )
                for i in range(4)
            ]
        ),
        fac.AntdText('垂直排布'),
        fac.AntdFlex(
            [
                html.Div(
                    style={
                        'width': '25%',
                        'height': 48,
                        'background': '#1677ff'
                        if i % 2 == 0
                        else '#1677ffbf',
                    }
                )
                for i in range(4)
            ],
            vertical=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 间距

- 说明：灵活控制子元素之间的间距。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='flex-gap-demo-gap',
            options=['small', 'middle', 'large', '66'],
            value='small',
        ),
        fac.AntdFlex(
            [fac.AntdButton('子元素', type='primary')] * 4,
            id='flex-gap-demo',
        ),
    ],
    direction='vertical',
    size='large',
    style={'width': '100%'},
)

...

@app.callback(
    Output('flex-gap-demo', 'gap'),
    Input('flex-gap-demo-gap', 'value'),
)
def update_demo_gap(value):
    if value == '66':
        return 66

    return value
```

### 自动换行

- 说明：控制子元素超宽后是否自动换行。

#### 代码
```python
fac.AntdFlex(
    [fac.AntdButton('子元素', type='primary')] * 25,
    gap='small',
    wrap='wrap',
)
```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
    Component type, child elements.

- id (string; optional):
    Unique identifier for the component.

- align (string; default 'normal'):
    Alignment of child elements in the cross axis, equivalent to the CSS `align-items` property. Default value: `'normal'`.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- className (string | dict; optional):
    Current component CSS class name, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- flex (string; default 'normal'):
    Equivalent to the CSS `flex` property. Default value: `'normal'`.

- gap (string | number | a value equal to: 'small', 'middle', 'large'; optional):
    Spacing between child elements, options include `'small'`, `'middle'`, `'large'`, or a string CSS width, or a numeric pixel width.

- justify (string; default 'normal'):
    Alignment of child elements in the main axis, equivalent to the CSS `justify-content` property. Default value: `'normal'`.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

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

- vertical (boolean; default False):
    Whether to use a vertical main axis. Default value: `False`.

- wrap (string | boolean; default 'nowrap'):
    Behavior of child element wrapping, equivalent to the CSS `flex-wrap` property, or can directly pass a boolean value to set whether to wrap automatically. Default value: `'nowrap'`.
