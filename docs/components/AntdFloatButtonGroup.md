# AntdFloatButtonGroup

## 简介源码：`views/AntdFloatButtonGroup/intro.py`
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
                {'title': translator.t('AntdFloatButtonGroup 悬浮按钮组')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdFloatButtonGroup 悬浮按钮组'), level=2),
        fac.AntdParagraph(translator.t('用于承载一组悬浮按钮。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：监听悬浮按钮组菜单模式下的展开状态。

#### 代码
```python
[
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-mail')),
        ],
        id='float-button-group-basic-event',
        trigger='click',
        icon=fac.AntdIcon(icon='antd-menu'),
        type='primary',
    ),
    fac.AntdText(id='float-button-group-basic-event-output'),
]

...

@app.callback(
    Output('float-button-group-basic-event-output', 'children'),
    Input('float-button-group-basic-event', 'open'),
    prevent_initial_call=True,
)
def float_button_group_basic_event(open):
    return f'open: {open}'
```

### 基础使用

- 说明：最基础的悬浮按钮组。

#### 代码
```python
[
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-mail')),
        ]
    ),
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-mail')),
            fac.AntdFloatButton(
                icon=fac.AntdIcon(icon='antd-notification')
            ),
        ],
        shape='square',
        style={'right': 84},
    ),
]
```

### 菜单模式

- 说明：设置参数`trigger`开启不同触发方式对应的菜单模式。

#### 代码
```python
[
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-mail')),
        ],
        trigger='hover',
        icon=fac.AntdIcon(icon='antd-menu'),
        type='primary',
    ),
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-mail')),
        ],
        trigger='click',
        style={'right': 84},
        icon=fac.AntdIcon(icon='antd-menu'),
        type='primary',
    ),
]
```

### 菜单展开方向

- 说明：设置参数`placement`控制不同的菜单展开方向。

#### 代码
```python
[
    fac.AntdSegmented(
        id='float-button-group-placement',
        options=[
            {'label': placement, 'value': placement}
            for placement in ['top', 'right', 'bottom', 'left']
        ],
        value='top',
        block=True,
    ),
    fac.AntdFloatButtonGroup(
        [
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-question')),
            fac.AntdFloatButton(icon=fac.AntdIcon(icon='antd-setting')),
        ],
        id='float-button-group-placement-demo',
        trigger='click',
        style={'right': 'calc(50vw - 20px)', 'bottom': 'calc(50vh - 20px)'},
        icon=fac.AntdIcon(icon='antd-menu'),
        type='primary',
    ),
]

...

@app.callback(
    Output('float-button-group-placement-demo', 'placement'),
    Input('float-button-group-placement', 'value'),
)
def float_button_group_placement_demo(value):
    return value
```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
  Component type, embedded element within the button.
- id (string; optional):
  Unique identifier for the component.
- className (string | dict; optional):
  CSS class name for the current component, supports [dynamic CSS](/advanced-classname).
- description (a list of or a singular dash component, string or number; optional):
  Description content
- icon (a list of or a singular dash component, string or number; optional):
  Component type, prefix icon element nested within the button.
- key (string; optional):
  Updating the `key` value of the current component can force a redraw of the component.
- loading_state (dict; optional)

  `loading_state` is a dict with keys:

  - component_name (string; optional):
    Holds the name of the component that is loading.
  - is_loading (boolean; optional):
    Determines if the component is loading or not.
  - prop_name (string; optional):
    Holds which property is loading.
- open (boolean; optional):
  Set or listen to the open state of the current component.
- shape (a value equal to: 'circle', 'square'; default 'circle'):
  Shape of the button, options include `'circle'`, `'square'`. Default value: `'circle'`.
- style (dict; optional):
  CSS styles for the current component.
- tooltip (a list of or a singular dash component, string or number; optional):
  Component type, additional tooltip content for the button.
- trigger (a value equal to: 'click', 'hover'; optional):
  The trigger method for menu expansion mode. options include `'click'` , `'hover'`.
- type (a value equal to: 'default', 'primary'; default 'default'):
  Type of the button, options include `'default'`, `'primary'`. Default value: `'default'`.
