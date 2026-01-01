# AntdNotification

## 简介源码：`views/AntdNotification/intro.py`
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
                {'title': 'AntdNotification 通知提醒框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdNotification 通知提醒框', level=2),
        fac.AntdParagraph('用于全局展示通知提醒信息。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdButton(
    '触发通知提醒框', id='notification-basic-demo-new', type='primary'
),
html.Div(id='notification-basic-demo'),

...

@app.callback(
    Output('notification-basic-demo', 'children'),
    Input('notification-basic-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def notification_basic_demo(nClicks):
    return fac.AntdNotification(
        message='Notification Title',
        description='Hello, feffery-antd-components!',
    )
```

### duration

- 说明：演示 duration 的用法。

#### 代码
```python
fac.AntdButton(
    '触发10s全局通知提醒',
    id='notification-duration-demo-new',
    type='primary',
),
html.Div(id='notification-duration-demo'),

...

@app.callback(
    Output('notification-duration-demo', 'children'),
    Input('notification-duration-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def notification_duration_demo(nClicks):
    return fac.AntdNotification(
        message='通知延时',
        description='这是一条成功通知消息，将在10s后自动消失',
        duration=10,
        type='success',
    )
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            'top',
            id={
                'type': 'placement-trigger-notification',
                'index': 'top',
            },
            type='primary',
        ),
        fac.AntdButton(
            'bottom',
            id={
                'type': 'placement-trigger-notification',
                'index': 'bottom',
            },
            type='primary',
        ),
    ],
),
fac.AntdDivider(),
fac.AntdSpace(
    [
        fac.AntdButton(
            'topLeft',
            id={
                'type': 'placement-trigger-notification',
                'index': 'topLeft',
            },
            type='primary',
        ),
        fac.AntdButton(
            'topRight',
            id={
                'type': 'placement-trigger-notification',
                'index': 'topRight',
            },
            type='primary',
        ),
    ],
),
fac.AntdDivider(),
fac.AntdSpace(
    [
        fac.AntdButton(
            'bottomLeft',
            id={
                'type': 'placement-trigger-notification',
                'index': 'bottomLeft',
            },
            type='primary',
        ),
        fac.AntdButton(
            'bottomRight',
            id={
                'type': 'placement-trigger-notification',
                'index': 'bottomRight',
            },
            type='primary',
        ),
    ],
),
html.Div(id='notification-placement-demo'),

...

@app.callback(
    Output('notification-placement-demo', 'children'),
    Input({'type': 'placement-trigger-notification', 'index': ALL}, 'nClicks'),
    prevent_initial_call=True,
)
def notification_placement_demo(nClicks):
    triggered_index = ctx.triggered_id.index
    if nClicks:
        return fac.AntdNotification(
            message=f'{triggered_index.capitalize()} notification',
            description=f'This is the content of the {triggered_index} notification. '
            * 3,
            placement=triggered_index,
            type='info',
        )

    return no_update
```

### show_progress

- 说明：演示 show_progress 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发通知提醒框',
        id='notification-show-progress-demo-new',
        type='primary',
    ),
    html.Div(id='notification-show-progress-demo'),
]

...

@app.callback(
    Output('notification-show-progress-demo', 'children'),
    Input('notification-show-progress-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def notification_show_progress_demo(nClicks):
    return fac.AntdNotification(
        message='Notification Title',
        description='Hello, feffery-antd-components!',
        showProgress=True,
    )
```

### stack

- 说明：演示 stack 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发通知提醒框', id='notification-stack-demo-new', type='primary'
    ),
    html.Div(id='notification-stack-demo'),
]

...

@app.callback(
    Output('notification-stack-demo', 'children'),
    Input('notification-stack-demo-new', 'nClicks'),
    prevent_initial_call=True,
)
def notification_stack_demo(nClicks):
    return fac.AntdNotification(
        message='Notification Title',
        description='Hello, feffery-antd-components!',
        stack=True,
    )
```

### type

- 说明：演示 type 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdButton(
            'Default',
            id={'type': 'trigger-notification', 'index': 'default'},
            type='default',
        ),
        fac.AntdButton(
            'Info',
            id={'type': 'trigger-notification', 'index': 'info'},
            type='default',
        ),
        fac.AntdButton(
            'Success',
            id={'type': 'trigger-notification', 'index': 'success'},
            type='default',
        ),
        fac.AntdButton(
            'Warning',
            id={'type': 'trigger-notification', 'index': 'warning'},
            type='default',
        ),
        fac.AntdButton(
            'Error',
            id={'type': 'trigger-notification', 'index': 'error'},
            type='default',
        ),
        html.Div(id='notification-type-demo'),
    ],
    gap='small',
    align='flex-start',
)

...

@app.callback(
    Output('notification-type-demo', 'children'),
    Input({'type': 'trigger-notification', 'index': ALL}, 'nClicks'),
    prevent_initial_call=True,
)
def notification_type_demo(nClicks):
    triggered_index = ctx.triggered_id.index
    if nClicks:
        return fac.AntdNotification(
            message=f'{triggered_index.capitalize()} notification',
            description=f'This is the content of the {triggered_index} notification. '
            * 3,
            type=triggered_index,
        )

    return no_update
```
