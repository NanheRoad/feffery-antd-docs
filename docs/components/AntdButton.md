# AntdButton

## 简介源码：`views/AntdButton/intro.py`
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
                {'title': translator.t('通用')},
                {'title': translator.t('AntdButton 按钮')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdButton 按钮'), level=2),
        fac.AntdParagraph(translator.t('按钮用于触发一个即时操作。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 链接跳转功能

- 说明：设置参数`href`添加链接跳转功能。

#### 代码
```python
fac.AntdButton(
    'fac文档首页', type='primary', href='/', target='_blank'
)
```

### 汉字自动插入空格

- 说明：设置参数`autoInsertSpace`控制是否在按钮内容为两个汉字时，自动插入空格。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdButton('汉字'), fac.AntdButton('汉字', autoInsertSpace=False)],
    wrap=True,
)
```

### 点击自动进入加载中状态

- 说明：设置参数`autoSpin`控制按钮是否在每次被点击后自动进入加载中状态。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, autoSpin=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True,
)
```

### 配合autoSpin的回调

- 说明：配合`autoSpin`、`loadingChildren`等参数优化点击按钮触发耗时计算任务执行的场景。

#### 代码
```python
fac.AntdButton(
    '按钮示例',
    id='button-auto-spin-demo',
    loadingChildren='计算中',
    autoSpin=True,
)

...

@app.callback(
    Output('button-auto-spin-demo', 'loading'),
    Input('button-auto-spin-demo', 'nClicks'),
    prevent_initial_call=True,
)
def button_auto_spin_demo(nClicks):
    # 模拟计算任务耗时
    time.sleep(2)

    return False
```

### 回调监听

- 说明：通过`nClicks`进行按钮点击事件的监听，特别地，在有效设置参数`debounceWait`后，将针对点击事件进行防抖监听，避免过于频繁的触发。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdButton('常规点击监听', id='button-basic-event'),
                fac.AntdText(id='button-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdButton(
                    '防抖点击监听', id='button-debounce-event', debounceWait=300
                ),
                fac.AntdText(id='button-debounce-event-output'),
            ]
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('button-basic-event-output', 'children'),
    Input('button-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('button-debounce-event-output', 'children'),
    Input('button-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_debounce_event(nClicks):
    return f'nClicks: {nClicks}'
```

### 基础使用

- 说明：最基础的按钮。

#### 代码
```python
fac.AntdButton('按钮示例')
```

### 撑满父元素

- 说明：设置参数`block=True`撑满父元素。

#### 代码
```python
fac.AntdButton('按钮示例', type='primary', block=True)
```

### 额外图标

- 说明：设置参数`icon`添加自定义图标元素。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            'fac文档首页', icon=fac.AntdIcon(icon='antd-search')
        ),
        fac.AntdButton(
            'fac文档首页',
            icon=fac.AntdIcon(icon='antd-search'),
            iconPosition='end',
        ),
    ],
    wrap=True
)
```

### 加载中状态

- 说明：设置参数`loading`控制是否将按钮渲染为加载中状态。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, loading=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True,
)
```

### 按钮形状

- 说明：设置参数`shape`控制按钮形状。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(shape, type='primary', shape=shape)
        for shape in ['default', 'circle', 'round']
    ],
    wrap=True
)
```

### 按钮类型

- 说明：不同类型的按钮。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
```

### 点击直接执行js

- 说明：通过参数`clickExecuteJsString`为按钮设置每次点击后直接触发的**javascript**代码，从而在简单场景下省略编写回调函数。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdButton(
                '执行js', clickExecuteJsString='alert("执行js示例")'
            ),
            fac.AntdButton(
                '打开模态框',
                clickExecuteJsString='dash_clientside.set_props("button-click-execute-js-modal", {"visible": true})',
            ),
        ],
        wrap=True,
    ),
    # 示例模态框
    fac.AntdModal(
        '这是一个示例模态框',
        id='button-click-execute-js-modal',
        title='示例模态框',
    ),
]
```

### 颜色与变体

- 说明：通过参数`color`和`variant`实现不同预设颜色主题与形态变体的组合。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                f'color: {color}',
                *[
                    fac.AntdButton(variant, color=color, variant=variant)
                    for variant in [
                        'outlined',
                        'dashed',
                        'solid',
                        'filled',
                        'text',
                        'link',
                    ]
                ],
            ],
            wrap=True,
        )
        for color in [
            'default',
            'primary',
            'danger',
            'blue',
            'purple',
            'cyan',
            'green',
            'magenta',
            'pink',
            'red',
            'orange',
            'yellow',
            'volcano',
            'geekblue',
            'lime',
            'gold',
        ]
    ],
    direction='vertical',
)
```

### 危险状态

- 说明：设置参数`danger=True`开启危险状态。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, danger=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
```

### 禁用状态

- 说明：设置参数`disabled=True`开启禁用状态。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, disabled=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
```

### 透明背景

- 说明：设置参数`ghost=True`开启透明背景。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, ghost=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],,
    wrap=True,
    style={'background': '#d9d9d9', 'padding': 8},
)
```

### 特殊交互动效

- 说明：设置参数`motionType='happy-work'`为按钮点击交互行为开启特殊交互动效。

#### 代码
```python
fac.AntdButton(
    '点我试试', type='primary', motionType='happy-work'
)
```

### 尺寸规格

- 说明：不同尺寸的按钮。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(size, size=size)
        for size in ['small', 'middle', 'large']
    ],
    wrap=True,
)
```

## API 参数说明


- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- children (a list of or a singular dash component, string or number; optional):
    Component type, the embedded element inside the button.

- style (dict; optional):
    The CSS style of the current component.

- className (string | dict; optional):
    The CSS class name of the current component, supports [dynamic CSS class names](/advanced-classname).

- styles (dict; optional):
    Fine-grained control over the CSS styles of child elements.

    `styles` is a dict with keys:

    - icon (dict; optional):
        The CSS style for the button icon element.

- classNames (dict; optional):
    Fine-grained control over the CSS class names of child elements.

    `classNames` is a dict with keys:

    - icon (string; optional):
        The CSS class name for the button icon element.

- loadingChildren (a list of or a singular dash component, string or number; optional):
    Component type, the embedded element displayed when the button is in a loading state.

- type (a value equal to: 'default', 'primary', 'dashed', 'link', 'text'; default 'default'):
    The type of button, with options `'default'`, `'primary'`, `'dashed'`, `'link'`, `'text'`.
    Default value: `'default'`.

- href (string; optional):
    The link address for the button to jump to when clicked.

- target (string; default '_blank'):
    The method of the link to jump when the button is clicked. Default value: `'_blank'`.

- autoInsertSpace (boolean; default True):
    Whether to insert a space between two Chinese characters in the button. Default value: `True`.

- block (boolean; default False):
    Whether the button is rendered as a block-level element (width fills the parent container). Default value: `False`.

- danger (boolean; default False):
    Whether the button presents a danger style. Default value: `False`.

- disabled (boolean; default False):
    Whether the button presents a disabled state. Default value: `False`.

- ghost (boolean; default False):
    Whether the button presents a transparent background state. Default value: `False`.

- shape (a value equal to: 'default', 'circle', 'round'; default 'default'):
    The shape of the button, with options `'default'`, `'circle'`, `'round'`. Default value: `'default'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    The size specification of the button, with options `'small'`, `'middle'`, `'large'`. Default value: `'middle'`.

- nClicks (number; default 0):
    The cumulative number of button clicks, used to monitor button click behavior. Default value: `0`.

- clickExecuteJsString (string; optional):
    The string of JavaScript code to be executed when the button is clicked.

- debounceWait (number; default 0):
    The debounce delay for the button click event listener, in milliseconds. Default value: `0`.

- icon (a list of or a singular dash component, string or number; optional):
    Component type, the prefix icon element embedded before the button.

- iconPosition (a value equal to: 'start', 'end'; default 'start'):
    The position of the button icon component, with options `'start'`, `'end'`. Default value: `'start'`.

- loading (boolean; optional):
    Whether the button presents a loading state. Default value: `False`.

- autoSpin (boolean; default False):
    Whether the current button automatically enters a loading state after each click. Default value: `False`.

- motionType (a value equal to: 'happy-work'; optional):
    The additional special interaction type of the button, with options `'happy-work'`.

- color (a value equal to: 'default', 'primary', 'danger'; optional):
    The color style of the button, with options `'default'`, `'primary'`, `'danger'`.

- variant (a value equal to: 'outlined', 'dashed', 'solid', 'filled', 'text', 'link'; optional):
    The variant type, with options `'outlined'`, `'dashed'`, `'solid'`, `'filled'`, `'text'`, `'link'`.

- title (string; optional):
    The native button title attribute.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
