# AntdAlert

## 简介源码：`views/AntdAlert/intro.py`
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
                {'title': 'AntdAlert 警告提示'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdAlert 警告提示', level=2),
        fac.AntdParagraph('用于渲染不同状态类型的警告提示信息。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### action

- 说明：演示 action 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(
            message='Success Tips',
            type='success',
            showIcon=True,
            closable=True,
            action=fac.AntdButton('UNDO', size='small', type='text'),
        ),
        fac.AntdAlert(
            message='Error Text',
            description='Error Description Error Description Error Description Error Description',
            type='error',
            showIcon=True,
            action=fac.AntdButton('Detail', size='small', danger=True),
        ),
        fac.AntdAlert(
            message='Warning Text',
            type='warning',
            closable=True,
            action=fac.AntdButton(
                'Done', size='small', type='text', ghost=True
            ),
        ),
        fac.AntdAlert(
            message='Info Text',
            description='Info Description Info Description Info Description Info Description',
            type='info',
            closable=True,
            action=fac.AntdSpace(
                [
                    fac.AntdButton('Accept', size='small', type='primary'),
                    fac.AntdButton(
                        'Decline', size='small', danger=True, ghost=True
                    ),
                ],
                direction='vertical',
            ),
        ),
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdAlert(
    showIcon=True,
    message=fac.AntdSpace(
        [
            fac.AntdText('这是组件型message参数示例，'),
            fac.AntdButton(
                '点我试试',
                id='alert-message-button-input',
                type='primary',
                size='small',
            ),
        ],
        size=0,
    ),
    description=fac.AntdText(
        '这是组件型description参数示例，上面的按钮被点了0次',
        id='alert-description-output',
    ),
)

...

@app.callback(
    Output('alert-description-output', 'children'),
    Input('alert-message-button-input', 'nClicks'),
    prevent_initial_call=True,
)
def alert_message_description_callback_demo(nClicks):
    return f'这是组件型description参数示例，上面的按钮被点了{nClicks}次'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdAlert(message='Success Text', type='success')
```

### closable

- 说明：演示 closable 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(
            message='Warning Text Warning Text Warning TextW arning Text Warning Text Warning TextWarning Text',
            type='warning',
            closable=True,
        ),
        fac.AntdAlert(
            message='Error Text',
            description='Error Description Error Description Error Description Error Description Error Description Error Description',
            type='error',
            closable=True,
        ),
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

### custom_icon

- 说明：演示 custom_icon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(message='Demo Text', showIcon=True, icon='😎'),
        fac.AntdAlert(
            message='Demo Text',
            showIcon=True,
            icon=fac.AntdIcon(icon='antd-user'),
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### description

- 说明：演示 description 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(
            message=f'{type.capitalize()} Text',
            description=f'{type.capitalize()} Description {type.capitalize()} Description {type.capitalize()} Description',
            type=type,
        )
        for type in ['success', 'info', 'warning', 'error']
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

### icon

- 说明：演示 icon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(
            message='Success Tips',
            type='success',
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Informational Notes',
            type='info',
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Warning', type='warning', showIcon=True, closable=True
        ),
        fac.AntdAlert(
            message='Error',
            type='error',
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Success Tips',
            description='Detailed description and advice about successful copywriting.',
            type='success',
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Informational Notes',
            description='Additional description and information about copywriting.',
            type='info',
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Warning',
            description='This is a warning notice about copywriting.',
            type='warning',
            showIcon=True,
            closable=True,
        ),
        fac.AntdAlert(
            message='Error',
            description='This is an error message about copywriting.',
            type='error',
            showIcon=True,
        ),
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

### loop

- 说明：演示 loop 的用法。

#### 代码
```python
fac.AntdAlert(
    message=[
        '君不见黄河之水天上来',
        '奔流到海不复回',
        '君不见高堂明镜悲白发',
        '朝如青丝暮成雪',
        '人生得意须尽欢',
        '莫使金樽空对月',
        '天生我材必有用',
        '千金散尽还复来',
    ],
    description='轮播模式示例',
    showIcon=True,
    messageRenderMode='loop-text',
)
```

### marquee

- 说明：演示 marquee 的用法。

#### 代码
```python
fac.AntdAlert(
    message='，'.join(
        [
            '君不见黄河之水天上来',
            '奔流到海不复回',
            '君不见高堂明镜悲白发',
            '朝如青丝暮成雪',
            '人生得意须尽欢',
            '莫使金樽空对月',
            '天生我材必有用',
            '千金散尽还复来。',
        ]
    ),
    description='这是走马灯模式示例',
    showIcon=True,
    messageRenderMode='marquee',
)
```

### top_notice

- 说明：演示 top_notice 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(
            message='Warning text',
            type='warning',
            banner=True,
            showIcon=True,
        ),
        fac.AntdAlert(
            message='Very long warning text warning text text text text text text text',
            type='warning',
            banner=True,
            showIcon=True,
            closable=True,
        ),
        fac.AntdAlert(
            message='Warning text without icon',
            type='warning',
            banner=True,
            showIcon=False,
        ),
        fac.AntdAlert(
            message='Error text',
            type='error',
            banner=True,
            showIcon=True,
        ),
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

### type

- 说明：演示 type 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAlert(message=f'{type.capitalize()} Text', type=type)
        for type in ['success', 'info', 'warning', 'error']
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- message (a list of or a singular dash component, string or number; optional):
    主要提示信息内容.

- description (a list of or a singular dash component, string or number; optional):
    额外提示信息内容.

- type (a value equal to: 'success', 'info', 'warning', 'error'; default 'info'):
    提示信息类型，可选项有`'success'`、`'info'`、`'warning'`、`'error'`
    默认值：`'info'`.

- showIcon (boolean; default False):
    是否显示额外图标  默认值：`False`.

- icon (a list of or a singular dash component, string or number; optional):
    组件型，当`showIcon=True`时，用于自定义图标元素.

- closable (boolean; default False):
    是否可关闭  默认值：`False`.

- messageRenderMode (a value equal to: 'default', 'loop-text', 'marquee'; default 'default'):
    渲染模式，可选项有`'default'`、`'loop-text'`、`'marquee'`  默认值：`'default'`.

- action (a list of or a singular dash component, string or number; optional):
    组件型，定义右上角额外操作区元素.

- banner (boolean; default False):
    是否用作顶部公告  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
