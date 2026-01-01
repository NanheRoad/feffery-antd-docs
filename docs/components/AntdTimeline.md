# AntdTimeline

## 简介源码：`views/AntdTimeline/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '通用'},
                {'title': 'AntdTimeline 时间轴'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTimeline 时间轴', level=2),
        fac.AntdParagraph('用于渲染美观的时间轴内容。'),
    ]

```

## 示例源码（demos）

### `views/AntdTimeline/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeline(
                items=[
                    {'content': '训练数据导入'},
                    {'content': '模型训练'},
                    {'content': '模型持久化'},
                    {'content': '模型发布'},
                ]
            )
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdTimeline(
            items=[
                {
                    'content': '训练数据导入'
                },
                {
                    'content': '模型训练'
                },
                {
                    'content': '模型持久化'
                },
                {
                    'content': '模型发布'
                }
            ]
        )
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/circle_color.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeline(
                items=[
                    {'content': '训练数据导入', 'color': 'blue'},
                    {'content': '模型训练', 'color': 'green'},
                    {'content': '模型持久化', 'color': 'grey'},
                    {'content': '模型发布', 'color': 'red'},
                ]
            )
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [        
        fac.AntdTimeline(
            items=[
                {
                    'content': '训练数据导入',
                    'color': 'blue'
                },
                {
                    'content': '模型训练',
                    'color': 'green'
                },
                {
                    'content': '模型持久化',
                    'color': 'grey'
                },
                {
                    'content': '模型发布',
                    'color': 'red'
                }
            ]
        )
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/custom_circle_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeline(
                items=[
                    {
                        'content': '负责人：张三',
                        'icon': fac.AntdAvatar(
                            mode='image',
                            src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                        ),
                    },
                    {
                        'content': '训练数据导入',
                        'icon': fac.AntdIcon(
                            icon='md-cloud-upload', style={'fontSize': '18px'}
                        ),
                    },
                    {
                        'content': '模型训练',
                        'icon': fac.AntdIcon(
                            icon='antd-clock-circle', style={'fontSize': '18px'}
                        ),
                    },
                    {
                        'content': '模型持久化',
                        'icon': fac.AntdIcon(
                            icon='fc-accept-database',
                            style={'fontSize': '18px'},
                        ),
                    },
                    {
                        'content': '模型发布',
                        'icon': fac.AntdIcon(
                            icon='md-cloud-done', style={'fontSize': '18px'}
                        ),
                    },
                ]
            )
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [        
        fac.AntdTimeline(
            items=[
                {
                    'content': '负责人：张三',
                    'icon': fac.AntdAvatar(
                        mode='image',
                        src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                    ),
                },
                {
                    'content': '训练数据导入',
                    'icon': fac.AntdIcon(
                        icon='md-cloud-upload',
                        style={
                            'fontSize': '18px'
                        }
                    )
                },
                {
                    'content': '模型训练',
                    'icon': fac.AntdIcon(
                        icon='antd-clock-circle',
                        style={
                            'fontSize': '18px'
                        }
                    )
                },
                {
                    'content': '模型持久化',
                    'icon': fac.AntdIcon(
                        icon='fc-accept-database',
                        style={
                            'fontSize': '18px'
                        }
                    )
                },
                {
                    'content': '模型发布',
                    'icon': fac.AntdIcon(
                        icon='md-cloud-done',
                        style={
                            'fontSize': '18px'
                        }
                    )
                }
            ]
        )
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/label.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeline(
                items=[
                    {'label': '1小时前', 'content': '训练数据导入'},
                    {'label': '58分钟前', 'content': '模型训练'},
                    {
                        'label': fac.AntdTag(content='9分钟前'),
                        'content': '模型持久化',
                    },
                    {
                        'label': fac.AntdTag(content='1分钟前'),
                        'content': '模型发布',
                    },
                ],
                pending='处理中',
            )
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdTimeline(
            items=[
                {
                    'label': '1小时前',
                    'content': '训练数据导入'
                },
                {
                    'label': '58分钟前',
                    'content': '模型训练'
                },
                {
                    'label': fac.AntdTag(content='9分钟前'),
                    'content': '模型持久化',
                },
                {
                    'label': fac.AntdTag(content='1分钟前'),
                    'content': '模型发布',
                },
            ],
            pending='处理中'
        )
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider(
                'mode="right"（默认）', innerTextOrientation='left'
            ),
            fac.AntdTimeline(
                items=[
                    {'label': '1小时前', 'content': '训练数据导入'},
                    {'label': '58分钟前', 'content': '模型训练'},
                    {'label': '9分钟前', 'content': '模型持久化'},
                    {'label': '1分钟前', 'content': '模型发布'},
                ],
                pending='处理中',
            ),
            fac.AntdDivider('mode="alternate"', innerTextOrientation='left'),
            fac.AntdTimeline(
                items=[
                    {'label': '1小时前', 'content': '训练数据导入'},
                    {'label': '58分钟前', 'content': '模型训练'},
                    {'label': '9分钟前', 'content': '模型持久化'},
                    {'label': '1分钟前', 'content': '模型发布'},
                ],
                pending='处理中',
                mode='alternate',
            ),
            fac.AntdDivider('mode="right"', innerTextOrientation='left'),
            fac.AntdTimeline(
                items=[
                    {'label': '1小时前', 'content': '训练数据导入'},
                    {'label': '58分钟前', 'content': '模型训练'},
                    {'label': '9分钟前', 'content': '模型持久化'},
                    {'label': '1分钟前', 'content': '模型发布'},
                ],
                pending='处理中',
                mode='right',
            ),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider(
            'mode="right"（默认）',
            innerTextOrientation='left'
        ),
        fac.AntdTimeline(
            items=[
                {
                    'label': '1小时前',
                    'content': '训练数据导入'
                },
                {
                    'label': '58分钟前',
                    'content': '模型训练'
                },
                {
                    'label': '9分钟前',
                    'content': '模型持久化'
                },
                {
                    'label': '1分钟前',
                    'content': '模型发布'
                }
            ],
            pending='处理中'
        ),

        fac.AntdDivider(
            'mode="alternate"',
            innerTextOrientation='left'
        ),
        fac.AntdTimeline(
            items=[
                {
                    'label': '1小时前',
                    'content': '训练数据导入'
                },
                {
                    'label': '58分钟前',
                    'content': '模型训练'
                },
                {
                    'label': '9分钟前',
                    'content': '模型持久化'
                },
                {
                    'label': '1分钟前',
                    'content': '模型发布'
                }
            ],
            pending='处理中',
            mode='alternate'
        ),

        fac.AntdDivider(
            'mode="right"',
            innerTextOrientation='left'
        ),
        fac.AntdTimeline(
            items=[
                {
                    'label': '1小时前',
                    'content': '训练数据导入'
                },
                {
                    'label': '58分钟前',
                    'content': '模型训练'
                },
                {
                    'label': '9分钟前',
                    'content': '模型持久化'
                },
                {
                    'label': '1分钟前',
                    'content': '模型发布'
                }
            ],
            pending='处理中',
            mode='right'
        )
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/pending.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('添加末尾幽灵节点', innerTextOrientation='left'),
            fac.AntdTimeline(
                items=[
                    {'content': '训练数据导入'},
                    {'content': '模型训练'},
                    {'content': '模型持久化'},
                    {'content': '模型发布'},
                ],
                pending='处理中',
            ),
            fac.AntdDivider('自定义幽灵节点图标', innerTextOrientation='left'),
            fac.AntdTimeline(
                items=[
                    {'content': '训练数据导入'},
                    {'content': '模型训练'},
                    {'content': '模型持久化'},
                    {'content': '模型发布'},
                ],
                pending='处理中',
                # 使用fuc.FefferyMotion组件为fac.AntdIcon组件添加动画效果
                pendingDot=fuc.FefferyMotion(
                    fac.AntdIcon(
                        icon='antd-hourglass',
                    ),
                    animate={
                        'transform': 'rotate(180deg)',
                    },
                    transition={
                        'repeat': 'infinity',
                        'duration': 1,
                        'type': 'spring',
                    },
                ),
            ),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider('添加末尾幽灵节点', innerTextOrientation='left'),
        fac.AntdTimeline(
            items=[
                {'content': '训练数据导入'},
                {'content': '模型训练'},
                {'content': '模型持久化'},
                {'content': '模型发布'},
            ],
            pending='处理中',
        ),
        fac.AntdDivider('自定义幽灵节点图标', innerTextOrientation='left'),
        fac.AntdTimeline(
            items=[
                {'content': '训练数据导入'},
                {'content': '模型训练'},
                {'content': '模型持久化'},
                {'content': '模型发布'},
            ],
            pending='处理中',
            # 使用fuc.FefferyMotion组件为fac.AntdIcon组件添加动画效果
            pendingDot=fuc.FefferyMotion(
                fac.AntdIcon(
                    icon='antd-hourglass',
                ),
                animate={
                    'transform': 'rotate(180deg)',
                },
                transition={
                    'repeat': 'infinity',
                    'duration': 1,
                    'type': 'spring',
                },
            ),
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdTimeline/demos/reverse.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTimeline(
                items=[
                    {'content': '训练数据导入'},
                    {'content': '模型训练'},
                    {'content': '模型持久化'},
                    {'content': '模型发布'},
                ],
                pending='处理中',
                reverse=True,
            ),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdTimeline(
            items=[
                {'content': '训练数据导入'},
                {'content': '模型训练'},
                {'content': '模型持久化'},
                {'content': '模型发布'},
            ],
            pending='处理中',
            reverse=True,
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```
