# AntdSegmented

## 简介源码：`views/AntdSegmented/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdSegmented 分段控制器'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSegmented 分段控制器', level=2),
        fac.AntdParagraph('用于展示多个选项并允许用户选择其中单个选项。'),
    ]

```

## 示例源码（demos）

### `views/AntdSegmented/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSegmented(
                id='segmented-demo',
                options=[
                    {'label': i, 'value': i}
                    for i in [
                        'Daily',
                        'Weekly',
                        'Monthly',
                        'Quarterly',
                        'Yearly',
                    ]
                ],
                defaultValue='Daily',
            ),
            fac.AntdText(id='segmented-demo-output'),
        ],
        direction='vertical',
    )

    return demo_contents


@app.callback(
    Output('segmented-demo-output', 'children'),
    Input('segmented-demo', 'value'),
)
def segmented_demo(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='segmented-demo',
            options=[
                {'label': i, 'value': i}
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            defaultValue='Daily',
        ),
        fac.AntdText(id='segmented-demo-output'),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('segmented-demo-output', 'children'),
    Input('segmented-demo', 'value'),
)
def segmented_demo(value):
    return f'value: {value}
"""
    }
]

```

### `views/AntdSegmented/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=[
            {'label': i, 'value': i}
            for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
        ],
        defaultValue='Daily',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
)
"""
    }
]

```

### `views/AntdSegmented/demos/block.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=[
            {'label': f'{i}', 'value': i}
            for i in [123, 456, 'longtext-longtext-longtext-longtext']
        ],
        defaultValue=123,
        block=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=[
        {'label': f'{i}', 'value': i}
        for i in [123, 456, 'longtext-longtext-longtext-longtext']
    ],
    defaultValue=123,
    block=True,
)
"""
    }
]

```

### `views/AntdSegmented/demos/custom_render.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdFlex(
        [
            fac.AntdSegmented(
                options=[
                    {
                        'label': html.Div(
                            [
                                fac.AntdAvatar(
                                    mode='image',
                                    src='https://api.dicebear.com/7.x/miniavs/svg?seed=8',
                                ),
                                html.Div('User 1'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'user1',
                    },
                    {
                        'label': html.Div(
                            [
                                fac.AntdAvatar(
                                    mode='text',
                                    text='K',
                                    style={
                                        'backgroundColor': '#f56a00',
                                    },
                                ),
                                html.Div('User 2'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'user2',
                    },
                    {
                        'label': html.Div(
                            [
                                fac.AntdAvatar(
                                    mode='icon',
                                    icon='antd-user',
                                    style={
                                        'backgroundColor': '#87d068',
                                    },
                                ),
                                html.Div('User 3'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'user3',
                    },
                ]
            ),
            fac.AntdSegmented(
                options=[
                    {
                        'label': html.Div(
                            [
                                html.Div('Spring'),
                                html.Div('Jan-Mar'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'spring',
                    },
                    {
                        'label': html.Div(
                            [
                                html.Div('Summer'),
                                html.Div('Apr-Jun'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'summer',
                    },
                    {
                        'label': html.Div(
                            [
                                html.Div('Autumn'),
                                html.Div('Jul-Sept'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'autumn',
                    },
                    {
                        'label': html.Div(
                            [
                                html.Div('Winter'),
                                html.Div('Oct-Dec'),
                            ],
                            style={'padding': 4},
                        ),
                        'value': 'winter',
                    },
                ]
            ),
        ],
        gap='small',
        align='flex-start',
        vertical=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='image',
                                src='https://api.dicebear.com/7.x/miniavs/svg?seed=8',
                            ),
                            html.Div('User 1'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user1',
                },
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='text',
                                text='K',
                                style={
                                    'backgroundColor': '#f56a00',
                                },
                            ),
                            html.Div('User 2'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user2',
                },
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='icon',
                                icon='antd-user',
                                style={
                                    'backgroundColor': '#87d068',
                                },
                            ),
                            html.Div('User 3'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user3',
                },
            ]
        ),
        fac.AntdSegmented(
            options=[
                {
                    'label': html.Div(
                        [
                            html.Div('Spring'),
                            html.Div('Jan-Mar'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'spring',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Summer'),
                            html.Div('Apr-Jun'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'summer',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Autumn'),
                            html.Div('Jul-Sept'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'autumn',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Winter'),
                            html.Div('Oct-Dec'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'winter',
                },
            ]
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
"""
    }
]

```

### `views/AntdSegmented/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdFlex(
        [
            fac.AntdSegmented(
                options=[
                    {'label': i, 'value': i}
                    for i in ['Map', 'Transit', 'Satellite']
                ],
                defaultValue='Map',
                disabled=True,
            ),
            fac.AntdSegmented(
                options=[
                    {
                        'label': i,
                        'value': i,
                        'disabled': True
                        if i in ['Weekly', 'Quarterly']
                        else False,
                    }
                    for i in [
                        'Daily',
                        'Weekly',
                        'Monthly',
                        'Quarterly',
                        'Yearly',
                    ]
                ],
                defaultValue='Daily',
            ),
        ],
        gap='small',
        align='flex-start',
        vertical=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {'label': i, 'value': i}
                for i in ['Map', 'Transit', 'Satellite']
            ],
            defaultValue='Map',
            disabled=True,
        ),
        fac.AntdSegmented(
            options=[
                {
                    'label': i,
                    'value': i,
                    'disabled': True
                    if i in ['Weekly', 'Quarterly']
                    else False,
                }
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            defaultValue='Daily',
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
"""
    }
]

```

### `views/AntdSegmented/demos/icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=[
            {'label': f'选项{i}', 'value': i, 'icon': icon}
            for i, icon in enumerate(
                [
                    'antd-carry-out',
                    'antd-branches',
                    'antd-team',
                    'antd-send',
                    'antd-setting',
                ]
            )
        ],
        defaultValue=0,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=[
        {'label': f'选项{i}', 'value': i, 'icon': icon}
        for i, icon in enumerate(
            [
                'antd-carry-out',
                'antd-branches',
                'antd-team',
                'antd-send',
                'antd-setting',
            ]
        )
    ],
    defaultValue=0,
)
"""
    }
]

```

### `views/AntdSegmented/demos/only_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSegmented(
                options=[
                    {'value': i, 'icon': icon}
                    for i, icon in enumerate(
                        [
                            'antd-carry-out',
                            'antd-branches',
                            'antd-team',
                            'antd-send',
                            'antd-setting',
                        ]
                    )
                ],
                defaultValue=0,
            ),
            fac.AntdSegmented(
                options=[
                    {'value': i, 'icon': icon}
                    for i, icon in enumerate(
                        [
                            'antd-carry-out',
                            'antd-branches',
                            'antd-team',
                            'antd-send',
                            'antd-setting',
                        ]
                    )
                ],
                defaultValue=0,
                vertical=True,
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSegmented(
            options=[
                {'value': i, 'icon': icon}
                for i, icon in enumerate(
                    [
                        'antd-carry-out',
                        'antd-branches',
                        'antd-team',
                        'antd-send',
                        'antd-setting',
                    ]
                )
            ],
            defaultValue=0,
        ),
        fac.AntdSegmented(
            options=[
                {'value': i, 'icon': icon}
                for i, icon in enumerate(
                    [
                        'antd-carry-out',
                        'antd-branches',
                        'antd-team',
                        'antd-send',
                        'antd-setting',
                    ]
                )
            ],
            defaultValue=0,
            vertical=True,
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdSegmented/demos/quickly_set_options.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly'],
        defaultValue='Daily',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly'],
    defaultValue='Daily',
)
"""
    }
]

```

### `views/AntdSegmented/demos/shape.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=[
            {'label': i, 'value': i}
            for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
        ],
        defaultValue='Daily',
        shape='round',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
    shape='round',
)
"""
    }
]

```

### `views/AntdSegmented/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdFlex(
        [
            fac.AntdSegmented(
                options=[
                    {'label': i, 'value': i}
                    for i in [
                        'Daily',
                        'Weekly',
                        'Monthly',
                        'Quarterly',
                        'Yearly',
                    ]
                ],
                size=size,
                defaultValue='Daily',
            )
            for size in ['small', 'middle', 'large']
        ],
        gap='small',
        align='flex-start',
        vertical=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {'label': i, 'value': i}
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            size=size,
            defaultValue='Daily',
        )
        for size in ['small', 'middle', 'large']
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
"""
    }
]

```

### `views/AntdSegmented/demos/vertical.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmented(
        options=[
            {'label': i, 'value': i}
            for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
        ],
        defaultValue='Daily',
        vertical=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
    vertical=True,
)
"""
    }
]

```
