# AntdRow

## 简介源码：`views/AntdRow/intro.py`
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
                {'title': translator.t('网格系统')},
                {'title': translator.t('AntdRow 行')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdRow 行'), level=2),
        fac.AntdParagraph(translator.t('在网格系统中构建单个行元素。')),
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
            id='row-align-demo-justify',
            options=[
                'start',
                'end',
                'center',
                'space-between',
                'space-around',
            ],
            value='start',
        ),
        fac.AntdText('align:'),
        fac.AntdRadioGroup(
            id='row-align-demo-align',
            options=['top', 'middle', 'bottom'],
            value='top',
        ),
        fac.AntdRow(
            [
                fac.AntdCol(
                    fac.AntdButton('child', type='primary'),
                    flex='none',
                    style={'height': 'fit-content'},
                )
            ]
            * 4,
            id='row-align-demo',
            gutter=10,
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
    Output('row-align-demo', 'justify'),
    Input('row-align-demo-justify', 'value'),
)
def update_demo_justify(value):
    return value


@app.callback(
    Output('row-align-demo', 'align'),
    Input('row-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value
```

### 基础使用

- 说明：常规居中与行内居中。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCenter(
                f'col{i}',
                style={
                    'backgroundColor': '#1677ff'
                    if i % 2 == 0
                    else '#1677ffbf',
                    'color': 'white',
                    'height': 100,
                },
            ),
            span=6,
        )
        for i in range(1, 5)
    ],
    gutter=10,
)
```

### 基于flex灵活控制列宽

- 说明：基于参数`flex`实现更灵活的列宽分配。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCenter(
                f'{flex} / 7',
                style={
                    'backgroundColor': '#1677ff',
                    'color': 'white',
                    'height': 100,
                },
            ),
            flex=flex,
        )
        for i, flex in enumerate(['1', '2', '4'])
    ],
    gutter=10,
)
```

### 响应式布局

- 说明：设置不同屏幕宽度断点下的列宽分配值。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCenter(
                f'col{i}',
                style={
                    'backgroundColor': '#1677ff'
                    if i % 2 == 0
                    else '#1677ffbf',
                    'color': 'white',
                    'height': 100,
                },
            ),
            xs=12,
            sm=12,
            md=8,
            lg=8,
            xl=6,
            xxl=6,
        )
        for i in range(1, 5)
    ],
    gutter=[10, 10],
)
```

### 响应式gutter

- 说明：设置不同屏幕宽度断点下的`gutter`值。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            html.Div(
                style={
                    'backgroundColor': '#1677ff',
                    'height': 100,
                }
            ),
            span=6,
        )
    ]
    * 4,
    gutter={'xs': 5, 'sm': 8, 'md': 10, 'lg': 12, 'xl': 15, 'xxl': 25},
)
```

### 尺寸可调整

- 说明：配合[fuc.FefferyResizable](https://fuc.feffery.tech/FefferyResizable)实现两侧宽度可调整。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            [
                fuc.FefferyStyle(
                    rawStyle="""
.custom-right-resize-handle:hover, .custom-right-resize-handle:active {
    background: #007fd4;
    transition: 0.3s background;
}

.custom-right-resize-handle {
    background: #f0f0f0;
    transition: 0.3s background;
    width: 4px !important;
    right: -2px !important;
}
"""
                ),
                fuc.FefferyResizable(
                    fac.AntdCenter('left', style={'height': '100%'}),
                    defaultSize={'width': 100, 'height': '100%'},
                    direction=['right'],
                    handleClassNames={
                        'right': 'custom-right-resize-handle'
                    },
                    maxWidth=500,
                    minWidth=50,
                ),
            ],
            flex='none',
        ),
        fac.AntdCol(
            fac.AntdCenter('right', style={'height': '100%'}), flex='auto'
        ),
    ],
    style={'height': 400, 'border': '1px dashed #8c8c8c'},
)
```

### 自动换行

- 说明：控制子元素宽度溢出时自动换行。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            'span之和溢出24单位时', innerTextOrientation='left'
        ),
        fac.AntdRow(
            [
                fac.AntdCol(
                    fac.AntdCenter(
                        f'col{i}',
                        style={
                            'backgroundColor': '#1677ff'
                            if i % 2 == 0
                            else '#1677ffbf',
                            'color': 'white',
                            'height': 100,
                        },
                    ),
                    span=6,
                )
                for i in range(1, 10)
            ],
            gutter=[10, 10],
        ),
        fac.AntdDivider(
            '像素宽度之和溢出父容器100%时', innerTextOrientation='left'
        ),
        fac.AntdRow(
            [
                fac.AntdCol(
                    fac.AntdCenter(
                        'width: 200',
                        style={
                            'backgroundColor': '#1677ff'
                            if i % 2 == 0
                            else '#1677ffbf',
                            'color': 'white',
                            'height': 100,
                            'width': 200,
                        },
                    ),
                    flex='none',
                )
                for i in range(1, 10)
            ],
            gutter=[10, 10],
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

- align (a value equal to: 'top', 'middle', 'bottom'; default 'top'):
    Vertical alignment method, options include `'top'`, `'middle'`, `'bottom'`. Default value: `'top'`.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- gutter (dict; default 0):
    Grid spacing, when passing a numeric value, it represents the horizontal pixel spacing. When passing an array, it sets the horizontal and vertical pixel spacing respectively. When passing a dictionary, you can set the horizontal pixel spacing for responsive breakpoints.

    `gutter` is a number | list of numbers | dict with keys:

    - lg (number; optional):
        Horizontal pixel spacing when the page width is greater than or equal to 992px.

    - md (number; optional):
        Horizontal pixel spacing when the page width is greater than or equal to 768px.

    - sm (number; optional):
        Horizontal pixel spacing when the page width is greater than or equal to 567px.

    - xl (number; optional):
        Horizontal pixel spacing when the page width is greater than or equal to 1200px.

    - xs (number; optional):
        Horizontal pixel spacing when the page width is less than 567px.

    - xxl (number; optional):
        Horizontal pixel spacing when the page width is greater than or equal to 1600px.

- justify (a value equal to: 'start', 'end', 'center', 'space-around', 'space-between'; default 'start'):
    Horizontal arrangement method, options include `'start'`, `'end'`, `'center'`, `'space-around'`, `'space-between'`.
    Default value: `'start'`.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- loading_state (dict; optional):

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- style (dict; optional):
    CSS styles for the current component.

- wrap (boolean; default True):
    Whether to allow automatic line wrapping. Default value: `True`.
