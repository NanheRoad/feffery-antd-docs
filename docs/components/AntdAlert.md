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

## 示例源码（demos）

### `views/AntdAlert/demos/action.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAlert(
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

    return demo_contents


@app.callback(
    Output('alert-description-output', 'children'),
    Input('alert-message-button-input', 'nClicks'),
    prevent_initial_call=True,
)
def alert_message_description_callback_demo(nClicks):
    return f'这是组件型description参数示例，上面的按钮被点了{nClicks}次'


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAlert(message='Success Text', type='success')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdAlert(message='Success Text', type='success')
"""
    }
]

```

### `views/AntdAlert/demos/closable.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/custom_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/description.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/loop.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAlert(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/marquee.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAlert(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/top_notice.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAlert/demos/type.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdAlert(message=f'{type.capitalize()} Text', type=type)
            for type in ['success', 'info', 'warning', 'error']
        ],
        direction='vertical',
        size='middle',
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdAlert(message=f'{type.capitalize()} Text', type=type)
        for type in ['success', 'info', 'warning', 'error']
    ],
    direction='vertical',
    size='middle',
    style={'width': '100%'},
)
"""
    }
]

```
