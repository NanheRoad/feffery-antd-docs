# AntdResult

## 简介源码：`views/AntdResult/intro.py`
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
                {'title': 'AntdResult 结果'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdResult 结果', level=2),
        fac.AntdParagraph('用于为用户提供不同场景下的状态提示。'),
    ]

```

## 示例源码（demos）

### `views/AntdResult/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdResult(title='标题示例', subTitle='副标题示例')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdResult(title='标题示例', subTitle='副标题示例')
"""
    }
]

```

### `views/AntdResult/demos/complex_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdResult(
        status='success',
        title='任务创建成功',
        subTitle=fac.AntdSpace(
            [
                fac.AntdText('创建时间：2023-01-01 12:00:00', type='secondary'),
                fac.AntdSpace(
                    [
                        fac.AntdButton('查看详情', type='primary'),
                        fac.AntdButton('回到首页'),
                    ]
                ),
            ],
            direction='vertical',
            align='center',
        ),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdResult(
    status='success',
    title='任务创建成功',
    subTitle=fac.AntdSpace(
        [
            fac.AntdText('创建时间：2023-01-01 12:00:00', type='secondary'),
            fac.AntdSpace(
                [
                    fac.AntdButton('查看详情', type='primary'),
                    fac.AntdButton('回到首页'),
                ]
            ),
        ],
        direction='vertical',
        align='center',
    ),
)
"""
    }
]

```

### `views/AntdResult/demos/custom_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdResult(
        title='标题示例',
        subTitle='副标题示例',
        icon=fac.AntdIcon(
            icon='antd-bulb', style={'fontSize': 60, 'color': '#fcd53f'}
        ),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdResult(
    title='标题示例',
    subTitle='副标题示例',
    icon=fac.AntdIcon(
        icon='antd-bulb', style={'fontSize': 60, 'color': '#fcd53f'}
    ),
)
"""
    }
]

```

### `views/AntdResult/demos/extra.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdResult(
        title='标题示例',
        subTitle='副标题示例',
        extra=fac.AntdButton('额外内容', type='primary'),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdResult(
    title='标题示例',
    subTitle='副标题示例',
    extra=fac.AntdButton('额外内容', type='primary'),
)
"""
    }
]

```

### `views/AntdResult/demos/status_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdResult(
                title='标题示例', subTitle=f'status="{status}"', status=status
            )
            for status in [
                'info',
                'success',
                'warning',
                'error',
                '404',
                '403',
                '500',
                'loading',
            ]
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
        fac.AntdResult(
            title='标题示例', subTitle=f'status="{status}"', status=status
        )
        for status in [
            'info',
            'success',
            'warning',
            'error',
            '404',
            '403',
            '500',
            'loading',
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```
