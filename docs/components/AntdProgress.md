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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- type (a value equal to: 'line', 'circle', 'dashboard'; default 'line'):
    进度条类型，可选项有`'line'`、`'circle'`、`'dashboard'`  默认值：`'line'`.

- size (dict; default 'default'):
    进度条尺寸规格，可选项有`'small'`、`'default'`、`'large'`，传入数值型表示像素尺寸，传入字典型可分别控制宽度和高度
    默认值：`'default'`.

    `size` is a number | list of number | strings | a value equal to:
    'small', 'default' | dict with keys:

    - width (number; optional):
        像素宽度.

    - height (number; optional):
        像素高度.

- percent (number; default 0):
    进度条进度，取值应在`0`到`100`之间，当`100`时默认会渲染为完成状态  默认值：`0`.

- success (dict; optional):
    配置进度条完成状态相关参数.

    `success` is a dict with keys:

    - percent (number; optional):
        达到完成状态对应的进度，取值应在`0`到`100`之间  默认值：`100`.

    - strokeColor (dict; optional):
        完成状态进度条颜色，支持渐变色.

        `strokeColor` is a string

      Or dict with keys:

        - from (string; optional):

            渐变色开端颜色.

        - to (string; optional):

            渐变色末端颜色.

- format (dict; optional):
    配置进度提示相关参数.

    `format` is a dict with keys:

    - prefix (string; optional):
        进度提示前缀文字  默认值：`''`.

    - suffix (string; optional):
        进度提示后缀文字  默认值：`'%'`.

    - content (a list of or a singular dash component, string or number; optional):
        组件型，强制设置显示内容.

- status (a value equal to: 'success', 'exception', 'normal', 'active'; optional):
    进度条状态，可选项有`'success'`、`'exception'`、`'normal'`、`'active'`，其中`'active'`仅在`type='line'`时生效
    默认值：`'normal'`.

- showInfo (boolean; default True):
    是否显示进度数值或状态图标  默认值：`True`.

- percentPosition (dict; optional):
    适用于`'line'`型进度条，配置进度条附带进度数值信息显示位置.

    `percentPosition` is a dict with keys:

    - align (a value equal to: 'start', 'center', 'end'; optional):
        对齐方式，可选项有`'start'`、`'center'`、`'end'`.

    - type (a value equal to: 'inner', 'outer'; optional):
        内外位置，可选项有`'inner'`、`'outer'`.

- strokeColor (dict; optional):
    配置进度条颜色，支持渐变色.

    `strokeColor` is a string | list of strings | dict with keys:

    - from (string; optional):
        渐变色开端颜色.

    - to (string; optional):
        渐变色末端颜色. | dict with strings as keys and values of type string

- strokeLinecap (a value equal to: 'round', 'butt', 'square'; optional):
    进度条线型，可选项有`'round'`、`'butt'`、`'square'`  默认值：`'round'`.

- strokeWidth (number; optional):
    进度条线的宽度，单位是进度条画布宽度的百分比.

- trailColor (string; optional):
    未完成分段部分的颜色，默认无颜色.

- gapDegree (number; optional):
    进度条缺口角度，取值应在`0`到`295`之间，仅`type='dashboard'`时可用  默认值：`75`.

- gapPosition (a value equal to: 'top', 'bottom', 'left', 'right'; default 'bottom'):
    仪表盘缺口方向，可选项有`'top'`、`'bottom'`、`'left'`、`'right'`，仅`type='dashboard'`时可用
    默认值：`'bottom'`.

- steps (dict; optional):
    配置进度条分段数量，针对`'circle'`、`'dashboard'`型进度条支持传入字典型进行更详细的配置.

    `steps` is a number | dict with keys:

    - count (number; optional):
        分段数量.

    - gap (number; optional):
        分段间隔像素大小.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
