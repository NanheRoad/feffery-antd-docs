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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，定义走马灯中需要轮播的若干元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- arrows (boolean; default False):
    是否显示箭头  默认值：`False`.

- autoplay (dict; default False):
    是否自动轮播，可传入字典型进行更多配置  默认值：`False`.

    `autoplay` is a boolean | dict with keys:

    - dotDuration (boolean; optional):
        是否展示指示点进度条.

- dotPosition (a value equal to: 'top', 'bottom', 'left', 'right'; default 'bottom'):
    面板指示器位置，可选项有`'top'`、`'bottom'`、`'left'`、`'right'`  默认值：`'bottom'`.

- easing (string; default 'linear'):
    调整动画效果，同css中的`animation-timing-function`  默认值：'linear'.

- effect (a value equal to: 'scrollx', 'fade'; default 'scrollx'):
    动化效果，可选项有`'scrollx'`、`'fade'`  默认值：'scrollx'.

- autoplaySpeed (number; default 3000):
    轮播间隔时长，单位：毫秒  默认值：`3000`.

- speed (number; default 500):
    轮播动画耗时，单位：毫秒  默认值：`500`.

- pauseOnHover (boolean; default False):
    是否在鼠标悬停时暂停轮播  默认值：`False`.

- infinite (boolean; default True):
    是否启用无限循环轮播  默认值：`True`.

- lazyLoad (boolean; default False):
    是否针对走马灯中的子项实施懒加载效果  默认值：`False`.

- slidesToShow (number; default 1):
    同时展示的子项数量  默认值：`1`.

- slidesToScroll (number; default 1):
    一次轮播划过的子项数量  默认值：`1`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
