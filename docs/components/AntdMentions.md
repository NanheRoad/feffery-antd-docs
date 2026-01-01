# AntdMentions

## 简介源码：`views/AntdMentions/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdMentions 提及'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdMentions 提及', level=2),
        fac.AntdParagraph(
            '用于实现在输入内容中对不同角色进行提及的功能，常用于构建论坛、协同办公等平台中的评论功能。'
        ),
    ]

```

## 示例源码（demos）

### `views/AntdMentions/demos/auto_size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider('autoSize=False（默认）', innerTextOrientation='left'),
        fac.AntdMentions(
            defaultValue='示例内容' * 20,
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            style={'width': 300},
        ),
        fac.AntdDivider('autoSize=True', innerTextOrientation='left'),
        fac.AntdMentions(
            defaultValue='示例内容' * 20,
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            autoSize=True,
            style={'width': 300},
        ),
        fac.AntdDivider(
            '配置minRows、maxRows参数', innerTextOrientation='left'
        ),
        fac.AntdMentions(
            defaultValue='示例内容' * 20,
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            autoSize={'minRows': 2, 'maxRows': 6},
            style={'width': 300},
        ),
    ]

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDivider(
    'autoSize=False（默认）',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 300
    }
),

fac.AntdDivider(
    'autoSize=True',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    autoSize=True,
    style={
        'width': 300
    }
),

fac.AntdDivider(
    '配置minRows、maxRows参数',
    innerTextOrientation='left'
),
fac.AntdMentions(
    defaultValue='示例内容'*20,
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    autoSize={
        'minRows': 2,
        'maxRows': 6
    },
    style={
        'width': 300
    }
)
"""
    }
]

```

### `views/AntdMentions/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdMentions(
            id='mentions-demo',
            autoSize={'minRows': 2, 'maxRows': 4},
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            style={'width': 300},
        ),
        html.Br(),
        fac.AntdSpace(id='mentions-demo-output', direction='vertical'),
    ]

    return demo_contents


@app.callback(
    Output('mentions-demo-output', 'children'),
    [
        Input('mentions-demo', 'value'),
        Input('mentions-demo', 'selectedOptions'),
    ],
)
def mentions_demo(value, selectedOptions):
    return [
        fac.AntdText(f'value: {value}'),
        fac.AntdText(f'selectedOptions: {selectedOptions}'),
    ]


code_string = [
    {
        'code': """
fac.AntdMentions(
    id='mentions-demo',
    autoSize={
        'minRows': 2,
        'maxRows': 4
    },
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 300
    }
),

html.Br(),

fac.AntdSpace(
    id='mentions-demo-output',
    direction='vertical'
)

...

@app.callback(
    Output('mentions-demo-output', 'children'),
    [Input('mentions-demo', 'value'),
     Input('mentions-demo', 'selectedOptions')]
)
def mentions_demo(value, selectedOptions):

    return [
        fac.AntdText(
            f'value: {value}'
        ),
        fac.AntdText(
            f'selectedOptions: {selectedOptions}'
        )
    ]
"""
    }
]

```

### `views/AntdMentions/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdMentions(
        placeholder='请输入@',
        options=[
            {'label': f'用户{c}', 'value': f'用户{c}'} for c in list('abcdef')
        ],
        style={'width': 200},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdMentions(
    placeholder='请输入@',
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    style={
        'width': 200
    }
)
"""
    }
]

```

### `views/AntdMentions/demos/different_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdMentions(
        options=[
            {'label': f'用户{c}', 'value': f'用户{c}'} for c in list('abcdef')
        ],
        placement='top',
        style={'width': 200},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    placement='top',
    style={
        'width': 200
    }
)
"""
    }
]

```

### `views/AntdMentions/demos/disabled_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdMentions(
        options=[
            {'label': f'用户{c}', 'value': f'用户{c}'} for c in list('abcdef')
        ],
        disabled=True,
        style={'width': 200},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    disabled=True,
    style={
        'width': 200
    }
)
"""
    }
]

```

### `views/AntdMentions/demos/render_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider('status="warning"', innerTextOrientation='left'),
        fac.AntdMentions(
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            status='warning',
            style={'width': 200},
        ),
        fac.AntdDivider('status="error"', innerTextOrientation='left'),
        fac.AntdMentions(
            options=[
                {'label': f'用户{c}', 'value': f'用户{c}'}
                for c in list('abcdef')
            ],
            status='error',
            style={'width': 200},
        ),
    ]

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDivider(
    'status="warning"',
    innerTextOrientation='left'
),
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    status='warning',
    style={
        'width': 200
    }
),

fac.AntdDivider(
    'status="error"',
    innerTextOrientation='left'
),
fac.AntdMentions(
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    status='error',
    style={
        'width': 200
    }
)
"""
    }
]

```

### `views/AntdMentions/demos/trigger_keyword.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdMentions(
        placeholder='请输入#',
        options=[
            {'label': f'用户{c}', 'value': f'用户{c}'} for c in list('abcdef')
        ],
        prefix='#',
        style={'width': 200},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdMentions(
    placeholder='请输入#',
    options=[
        {
            'label': f'用户{c}',
            'value': f'用户{c}'
        }
        for c in list('abcdef')
    ],
    prefix='#',
    style={
        'width': 200
    }
)
"""
    }
]

```
