# AntdTransfer

## 简介源码：`views/AntdTransfer/intro.py`
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
                {'title': 'AntdTransfer 穿梭框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTransfer 穿梭框', level=2),
        fac.AntdParagraph(
            '用于以直观的方式在两栏中移动选项，帮助用户完成选择行为。'
        ),
    ]

```

## 示例源码（demos）

### `views/AntdTransfer/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdTransfer(
            id='transfer-demo',
            dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
            targetKeys=[2, 3, 4],
        ),
        fac.AntdSpace(id='transfer-demo-output', direction='vertical'),
    ]

    return demo_contents


@app.callback(
    Output('transfer-demo-output', 'children'),
    [
        Input('transfer-demo', 'targetKeys'),
        Input('transfer-demo', 'moveDirection'),
        Input('transfer-demo', 'moveKeys'),
    ],
)
def transfer_demo(targetKeys, moveDirection, moveKeys):
    return [
        fac.AntdText(f'targetKeys: {targetKeys}'),
        fac.AntdText(f'moveDirection: {moveDirection}'),
        fac.AntdText(f'moveKeys: {moveKeys}'),
    ]


code_string = [
    {
        'code': """
[
    fac.AntdTransfer(
        id='transfer-demo',
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
    ),
    fac.AntdSpace(id='transfer-demo-output', direction='vertical'),
]

...

@app.callback(
    Output('transfer-demo-output', 'children'),
    [Input('transfer-demo', 'targetKeys'),
     Input('transfer-demo', 'moveDirection'),
     Input('transfer-demo', 'moveKeys')]
)
def transfer_demo(targetKeys, moveDirection, moveKeys):

    return [
        fac.AntdText(f'targetKeys: {targetKeys}'),
        fac.AntdText(f'moveDirection: {moveDirection}'),
        fac.AntdText(f'moveKeys: {moveKeys}')
    ]
"""
    }
]

```

### `views/AntdTransfer/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
)
"""
    }
]

```

### `views/AntdTransfer/demos/custom_height.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdDivider(
                        f'height="{height}"', innerTextOrientation='left'
                    ),
                    fac.AntdTransfer(
                        dataSource=[
                            {'key': i, 'title': f'选项{i}'}
                            for i in range(1, 10)
                        ],
                        targetKeys=[2, 3, 4],
                        height=height,
                    ),
                ],
                direction='vertical',
                style={'width': '100%'},
            )
            for height in ['300px', '10rem', '30vh']
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
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    f'height="{height}"', innerTextOrientation='left'
                ),
                fac.AntdTransfer(
                    dataSource=[
                        {'key': i, 'title': f'选项{i}'}
                        for i in range(1, 10)
                    ],
                    targetKeys=[2, 3, 4],
                    height=height,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for height in ['300px', '10rem', '30vh']
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdTransfer/demos/custom_move_button_content.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
        operations=['放入', '移出'],
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    operations=['放入', '移出'],
)
"""
    }
]

```

### `views/AntdTransfer/demos/custom_titles.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
        titles=['左侧区域', '右侧区域'],
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    titles=['左侧区域', '右侧区域'],
)
"""
    }
]

```

### `views/AntdTransfer/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
        disabled=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    disabled=True,
)
"""
    }
]

```

### `views/AntdTransfer/demos/multiple_mode_search.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                id='transfer-multiple-mode-search-demo-switch-mode',
                options=[
                    {'label': mode, 'value': mode}
                    for mode in ['case-insensitive', 'case-sensitive', 'regex']
                ],
                defaultValue='case-insensitive',
                optionType='button',
            ),
            fac.AntdTransfer(
                id='transfer-multiple-mode-search-demo',
                dataSource=[
                    {'key': i, 'title': f'选项{i}'} for i in list('AbCdEf')
                ],
                targetKeys=[],
                showSearch=True,
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    Output('transfer-multiple-mode-search-demo', 'optionFilterMode'),
    Input('transfer-multiple-mode-search-demo-switch-mode', 'value'),
)
def transfer_multiple_mode_search_demo(value):
    return value


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='transfer-multiple-mode-search-demo-switch-mode',
            options=[
                {'label': mode, 'value': mode}
                for mode in ['case-insensitive', 'case-sensitive', 'regex']
            ],
            defaultValue='case-insensitive',
            optionType='button',
        ),
        fac.AntdTransfer(
            id='transfer-multiple-mode-search-demo',
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in list('AbCdEf')
            ],
            targetKeys=[],
            showSearch=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('transfer-multiple-mode-search-demo', 'optionFilterMode'),
    Input('transfer-multiple-mode-search-demo-switch-mode', 'value'),
)
def transfer_multiple_mode_search_demo(value):
    return value
"""
    }
]

```

### `views/AntdTransfer/demos/pagination.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 50)],
        targetKeys=[2, 3, 4],
        pagination={'pageSize': 5},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 50)],
    targetKeys=[2, 3, 4],
    pagination={'pageSize': 5},
)
"""
    }
]

```

### `views/AntdTransfer/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
        readOnly=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    readOnly=True,
)
"""
    }
]

```

### `views/AntdTransfer/demos/search.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTransfer(
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
        showSearch=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    showSearch=True,
)
"""
    }
]

```

### `views/AntdTransfer/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTransfer(
                dataSource=[
                    {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
                ],
                targetKeys=[2, 3, 4],
                status='warning',
            ),
            fac.AntdTransfer(
                dataSource=[
                    {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
                ],
                targetKeys=[2, 3, 4],
                status='error',
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
        fac.AntdTransfer(
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
            ],
            targetKeys=[2, 3, 4],
            status='warning',
        ),
        fac.AntdTransfer(
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
            ],
            targetKeys=[2, 3, 4],
            status='error',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```
