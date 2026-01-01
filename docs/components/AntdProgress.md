# AntdProgress

## 简介源码：`views/AntdProgress/intro.py`
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
                {'title': 'AntdProgress 进度条'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdProgress 进度条', level=2),
        fac.AntdParagraph('用于渲染常用形式的进度条。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            'type="line"（默认）', innerTextOrientation='left'
        ),
        fac.AntdProgress(percent=80, style={'width': 200}),
        fac.AntdDivider('type="circle"', innerTextOrientation='left'),
        fac.AntdProgress(percent=80, type='circle'),
        fac.AntdDivider(
            'type="dashboard"', innerTextOrientation='left'
        ),
        fac.AntdProgress(percent=80, type='dashboard'),
    ],
    direction='vertical',
)
```

### custom_percent_content

- 说明：演示 custom_percent_content 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(
            percent=80, format={'prefix': '进度'}, style={'width': 200}
        ),
        fac.AntdProgress(
            percent=80, format={'suffix': '分'}, type='circle'
        ),
        fac.AntdProgress(
            percent=80, format={'content': '🚀🚀🚀'}, type='dashboard'
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### dashboard_gap

- 说明：演示 dashboard_gap 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(
            percent=80,
            gapPosition=i,
            gapDegree=j,
            type='dashboard',
            style={'width': 200},
        )
        for i, j in [
            ('top', 0),
            ('left', 60),
            ('right', 180),
            ('bottom', 295),
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### finish_style

- 说明：演示 finish_style 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(percent=100, style={'width': 200}),
        fac.AntdProgress(percent=100, type='circle'),
        fac.AntdProgress(percent=100, type='dashboard'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### force_status

- 说明：演示 force_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdProgress(
                    percent=80, status=status, style={'width': 425}
                )
                for status in ['normal', 'success', 'exception', 'active']
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        fac.AntdSpace(
            [
                fac.AntdProgress(percent=80, status=status, type='circle')
                for status in ['normal', 'success', 'exception']
            ],
            style={'width': '100%'},
        ),
        fac.AntdSpace(
            [
                fac.AntdProgress(
                    percent=80, status=status, type='dashboard'
                )
                for status in ['normal', 'success', 'exception']
            ],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### gradient_color

- 说明：演示 gradient_color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(
            percent=80,
            strokeColor={'from': '#f067b4', 'to': '#81ffef'},
            style={'width': 200},
        ),
        fac.AntdProgress(
            percent=80,
            strokeColor={'from': '#f067b4', 'to': '#81ffef'},
            type='circle',
        ),
        fac.AntdProgress(
            percent=80,
            strokeColor={'from': '#f067b4', 'to': '#81ffef'},
            type='dashboard',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### mini

- 说明：演示 mini 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(
            percent=80,
            status=status,
            size='small',
            style={
                'width': 425
            }
        )
        for status in [
            'normal', 'success', 'exception', 'active'
        ]
    ],
    direction='vertical',
    style={
        'width': '100%'
    }
)
```

### mini_circle

- 说明：演示 mini_circle 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdProgress(percent=80, type='circle', size=14), '任务进度'],
    size='small',
)
```

### multi_step

- 说明：演示 multi_step 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTooltip(
            fac.AntdProgress(percent=60, success={'percent': 30}),
            title='3 done / 3 in progress / 4 to do',
        ),
        fac.AntdTooltip(
            fac.AntdProgress(
                percent=60, success={'percent': 30}, type='circle'
            ),
            title='3 done / 3 in progress / 4 to do',
        ),
        fac.AntdTooltip(
            fac.AntdProgress(
                percent=60, success={'percent': 30}, type='dashboard'
            ),
            title='3 done / 3 in progress / 4 to do',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### percent_position

- 说明：演示 percent_position 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    'percentPosition='
                    + json.dumps(
                        {
                            'align': align,
                            'type': _type,
                        }
                    )
                ),
                fac.AntdProgress(
                    percent=0,
                    size=['100%', 18],
                    percentPosition={
                        'align': align,
                        'type': _type,
                    },
                ),
                fac.AntdProgress(
                    percent=66.6,
                    size=['100%', 18],
                    percentPosition={
                        'align': align,
                        'type': _type,
                    },
                ),
                fac.AntdProgress(
                    percent=100,
                    size=['100%', 18],
                    percentPosition={
                        'align': align,
                        'type': _type,
                    },
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for align in ['start', 'center', 'end']
        for _type in ['inner', 'outer']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### remaining_color

- 说明：演示 remaining_color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdProgress(
            percent=80, trailColor='#a5d8ff', style={'width': 200}
        ),
        fac.AntdProgress(percent=80, trailColor='#a5d8ff', type='circle'),
        fac.AntdProgress(
            percent=80, trailColor='#a5d8ff', type='dashboard'
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### step_line

- 说明：演示 step_line 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('默认分段宽度', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdProgress(percent=40, steps=10),
                fac.AntdProgress(
                    percent=100, steps=5, strokeColor='#52c41a'
                ),
                fac.AntdProgress(percent=80, steps=10, size='small'),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        fac.AntdDivider('自定义分段宽度', innerTextOrientation='left'),
        fuc.FefferyStyle(
            rawStyle="""
#progress-custom-step-width .ant-progress-steps-item {
    width: 30px !important;
}
"""
        ),
        fac.AntdSpace(
            [
                fac.AntdProgress(percent=40, steps=10),
                fac.AntdProgress(
                    percent=100, steps=5, strokeColor='#52c41a'
                ),
            ],
            id='progress-custom-step-width',
            direction='vertical',
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
