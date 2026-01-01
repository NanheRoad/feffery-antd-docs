# AntdFloatButton

## 简介源码：`views/AntdFloatButton/intro.py`
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
                {'title': translator.t('AntdFloatButton 悬浮按钮')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdFloatButton 悬浮按钮'), level=2),
        fac.AntdParagraph(translator.t('悬浮于页面固定位置的按钮。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 链接跳转功能

- 说明：点击悬浮按钮进行链接跳转。

#### 代码
```python
fac.AntdFloatButton(href='/', target='_blank')
```

### 回调监听

- 说明：监听悬浮按钮的点击事件。

#### 代码
```python
[
    fac.AntdFloatButton(
        id='float-button-basic-event', description='点我', type='primary'
    ),
    fac.AntdText(id='float-button-basic-event-output'),
]

...

@app.callback(
    Output('float-button-basic-event-output', 'children'),
    Input('float-button-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def float_button_basic_event(nClicks):
    return f'nClicks: {nClicks}'
```

### 基础使用

- 说明：最基础的悬浮按钮。

#### 代码
```python
fac.AntdFloatButton()
```

### 描述信息

- 说明：为悬浮按钮添加额外描述信息。

#### 代码
```python
[
    fac.AntdFloatButton(description='描述信息'),
    fac.AntdFloatButton(
        description='描述信息', shape='square', style={'right': 84}
    ),
    fac.AntdFloatButton(
        description='描述信息',
        shape='square',
        type='primary',
        icon=fac.AntdIcon(icon='antd-question'),
        style={'right': 144},
    ),
]
```

### 按钮图标

- 说明：为悬浮按钮自定义图标元素。

#### 代码
```python
[
    fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
    fac.AntdFloatButton(
        type='primary',
        icon=fac.AntdIcon(icon='antd-bulb'),
        style={'right': 84},
    ),
]
```

### 按钮形状

- 说明：不同形状的悬浮按钮。

#### 代码
```python
[
    fac.AntdFloatButton(type='primary'),
    fac.AntdFloatButton(
        type='primary', shape='square', style={'right': 84}
    ),
]
```

### 气泡卡片

- 说明：为悬浮按钮添加额外气泡卡片信息。

#### 代码
```python
fac.AntdFloatButton(tooltip='气泡卡片信息示例')
```

### 按钮类型

- 说明：不同类型的悬浮按钮。

#### 代码
```python
[
    fac.AntdFloatButton(),
    fac.AntdFloatButton(type='primary', style={'right': 84}),
]
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- description (a list of or a singular dash component, string or number; optional):
    Component type, nested element within the button, available only when `shape='square'`.

- href (string; optional):
    URL to redirect to when the button is clicked.

- icon (a list of or a singular dash component, string or number; optional):
    Component type, prefix icon element nested within the button.

- key (string; optional):
    Updating the `key` value of the current component can force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:
    - component_name (string; optional):
        Holds the name of the component that is loading.
    - is_loading (boolean; optional):
        Determines if the component is loading or not.
    - prop_name (string; optional):
        Holds which property is loading.

- nClicks (number; default 0):
    Number of times the button has been clicked, used to monitor button click behavior. Default value: `0`.

- shape (a value equal to: 'circle', 'square'; default 'circle'):
    Shape of the button, options include `'circle'`, `'square'`. Default value: `'circle'`.

- style (dict; optional):
    CSS styles for the current component.

- target (string; default '_blank'):
    Method of opening the link when the button is clicked. Default value: `'_blank'`.

- tooltip (a list of or a singular dash component, string or number; optional):
    Component type, additional tooltip content for the button.

- type (a value equal to: 'default', 'primary'; default 'default'):
    Type of the button, options include `'default'`, `'primary'`. Default value: `'default'`.
