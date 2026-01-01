# AntdCarousel

## 简介源码：`views/AntdCarousel/intro.py`
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
                {'title': 'AntdCarousel 走马灯'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCarousel 走马灯', level=2),
        fac.AntdParagraph('轮播一组同级内容。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### auto_play

- 说明：演示 auto_play 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ],
    autoplay=True,
)
```

### auto_play_speed

- 说明：演示 auto_play_speed 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ],
    autoplay=True,
    autoplaySpeed=500,  # 500毫秒切换一次
)
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ]
)
```

### dot_duration

- 说明：演示 dot_duration 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ],
    autoplay={'dotDuration': True},
)
```

### dot_position

- 说明：演示 dot_position 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='carousel-dot-position',
            options=['bottom', 'top', 'left', 'right'],
            value='bottom',
        ),
        fac.AntdCarousel(
            [
                fac.AntdCenter(
                    i,
                    style={
                        'color': 'white',
                        'fontSize': 36,
                        'height': 160,
                        'backgroundColor': '#364d79',
                    },
                )
                for i in range(1, 6)
            ],
            id='carousel-dot-position-demo',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

app.clientside_callback(
    """(value) => value""",
    Output('carousel-dot-position-demo', 'dotPosition'),
    Input('carousel-dot-position', 'value'),
)
```

### fade_effect

- 说明：演示 fade_effect 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ],
    effect='fade',
)
```

### show_arrows

- 说明：演示 show_arrows 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCarousel(
            [
                fac.AntdCenter(
                    i,
                    style={
                        'color': 'white',
                        'fontSize': 36,
                        'height': 160,
                        'backgroundColor': '#364d79',
                    },
                )
                for i in range(1, 6)
            ],
            arrows=True,
        ),
        fac.AntdCarousel(
            [
                fac.AntdCenter(
                    i,
                    style={
                        'color': 'white',
                        'fontSize': 36,
                        'height': 160,
                        'backgroundColor': '#364d79',
                    },
                )
                for i in range(1, 6)
            ],
            dotPosition='left',
            arrows=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### slides_to_scroll

- 说明：演示 slides_to_scroll 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        html.Div(
            fac.AntdCenter(
                i,
                style={
                    'color': 'white',
                    'fontSize': 36,
                    'backgroundColor': '#364d79',
                    'height': '100%',
                },
            ),
            style={'height': 160, 'padding': '0 5px'},
        )
        for i in range(1, 10)
    ],
    slidesToShow=3,
    slidesToScroll=3,
)
```

### slides_to_show

- 说明：演示 slides_to_show 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        html.Div(
            fac.AntdCenter(
                i,
                style={
                    'color': 'white',
                    'fontSize': 36,
                    'backgroundColor': '#364d79',
                    'height': '100%',
                },
            ),
            style={'height': 160, 'padding': '0 5px'},
        )
        for i in range(1, 10)
    ],
    slidesToShow=3,
)
```

### transition_speed

- 说明：演示 transition_speed 的用法。

#### 代码
```python
fac.AntdCarousel(
    [
        fac.AntdCenter(
            i,
            style={
                'color': 'white',
                'fontSize': 36,
                'height': 160,
                'backgroundColor': '#364d79',
            },
        )
        for i in range(1, 6)
    ],
    speed=2000,
    autoplay=True,
)
```
