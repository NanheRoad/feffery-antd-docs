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

## 示例源码（demos）

### `views/AntdCarousel/demos/auto_play.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/auto_play_speed.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/dot_duration.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/dot_position.py`
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

    return demo_contents


app.clientside_callback(
    """(value) => value""",
    Output('carousel-dot-position-demo', 'dotPosition'),
    Input('carousel-dot-position', 'value'),
)

code_string = [
    {
        'code': '''
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
'''
    }
]

```

### `views/AntdCarousel/demos/fade_effect.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/show_arrows.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/slides_to_scroll.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/slides_to_show.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCarousel/demos/transition_speed.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdCarousel(
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

    return demo_contents


code_string = [
    {
        'code': """

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
"""
    }
]

```
