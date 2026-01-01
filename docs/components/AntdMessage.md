# AntdMessage

## 简介源码：`views/AntdMessage/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '反馈'},
                {'title': 'AntdMessage 全局提示'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdMessage 全局提示', level=2),
        fac.AntdParagraph('用于全局展示操作反馈信息。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdButton(
    '触发全局提示', id='message-basic-demo-new', type='primary'
),
html.Div(id='message-basic-demo'),

...

@app.callback(
    Output('message-basic-demo', 'children'),
    Input('message-basic-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def message_basic_demo(nClicks):
    return fac.AntdMessage(content='Hello, feffery-antd-components!', type='info')
```

### duration

- 说明：演示 duration 的用法。

#### 代码
```python
fac.AntdButton(
        '触发10s全局提示', id='message-duration-demo-new', type='primary'
    ),
    html.Div(id='message-duration-demo'),
]

...

@app.callback(
    Output('message-duration-demo', 'children'),
    Input('message-duration-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def message_duration_demo(nClicks):
    return fac.AntdMessage(
        content='这是一条成功提示消息，将在10s后自动消失',
        duration=10,
        type='success',
    )
```

### max_count

- 说明：演示 max_count 的用法。

#### 代码
```python
fac.AntdButton(
    '触发全局提示', id='message-max-count-demo-new', type='primary'
),
html.Div(id='message-max-count-demo'),

...

@app.callback(
    Output('message-max-count-demo', 'children'),
    Input('message-max-count-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def message_max_count_demo(nClicks):
    return fac.AntdMessage(content='全局提示示例', type='success', maxCount=3)
```

### top

- 说明：演示 top 的用法。

#### 代码
```python
fac.AntdButton(
    '触发距离顶端200px全局提示',
    id='message-top-demo-new',
    type='primary',
),
html.Div(id='message-top-demo'),

...

@app.callback(
    Output('message-top-demo', 'children'),
    Input('message-top-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def message_top_demo(nClicks):
    return fac.AntdMessage(content='全局提示示例', top=200, type='success')
```

### type

- 说明：演示 type 的用法。

#### 代码
```python
fac.AntdFlex(
[
    fac.AntdButton(
        'Default',
        id={'type': 'trigger-message', 'index': 'default'},
        type='default',
    ),
    fac.AntdButton(
        'Info',
        id={'type': 'trigger-message', 'index': 'info'},
        type='default',
    ),
    fac.AntdButton(
        'Success',
        id={'type': 'trigger-message', 'index': 'success'},
        type='default',
    ),
    fac.AntdButton(
        'Warning',
        id={'type': 'trigger-message', 'index': 'warning'},
        type='default',
    ),
    fac.AntdButton(
        'Error',
        id={'type': 'trigger-message', 'index': 'error'},
        type='default',
    ),
    html.Div(id='message-type-demo'),
],
gap='small',
align='flex-start',
)

...

@app.callback(
    Output('message-type-demo', 'children'),
    Input({'type': 'trigger-message', 'index': ALL}, 'nClicks'),
    prevent_initial_call=True,
)
def message_type_demo(nClicks):
    triggered_index = ctx.triggered_id.index
    if nClicks:
        return fac.AntdMessage(
            content=f'{triggered_index.capitalize()} message',
            type=triggered_index,
        )

    return no_update
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string; optional):
    当前组件css类名.

- content (string; optional):
    提示信息内容.

- type (a value equal to: 'default', 'success', 'error', 'info', 'warning'; default 'default'):
    提示信息类型，可选项有`'default'`、`'success'`、`'error'`、`'info'`、`'warning'`
    默认值：'default'.

- duration (number; default 3):
    提示信息自动消失对应的延时，单位：秒，设置为`0`时不会自动消失  默认值：`3`.

- top (number; default 8):
    提示信息距离顶端的像素距离  默认值：`8`.

- maxCount (number; optional):
    最多允许同时出现的提示信息数量.

- icon (string; optional):
    自定义前缀图标，同`AntdIcon`的`icon`参数.

- iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; default 'AntdIcon'):
    自定义前缀图标渲染方式，可选项有`'AntdIcon'`、`'fontawesome'`.
