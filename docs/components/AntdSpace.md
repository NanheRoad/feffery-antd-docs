# AntdSpace

## 简介源码：`views/AntdSpace/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('布局')},
                {'title': translator.t('AntdSpace 排列')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdSpace 排列'), level=2),
        fac.AntdParagraph(
            translator.t('用于快捷对一组元素进行水平或竖直方向上的规整排列。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdSpace/demos/align.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = [
            fac.AntdRadioGroup(
                id='space-align-demo-align',
                options=['start', 'end', 'center', 'baseline'],
                value='start',
            ),
            fac.AntdParagraph('水平方向：'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(0, 146, 255, 1)',
                            'height': '25px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '10px',
                            'width': '50px',
                        }
                    ),
                ],
                id='space-align-demo-horizontal',
                align='start',
                style={
                    'backgroundColor': 'rgba(241, 241, 241, 0.6)',
                    'padding': '10px',
                },
            ),
            fac.AntdParagraph('竖直方向：'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(0, 146, 255, 1)',
                            'height': '50px',
                            'width': '25px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                ],
                id='space-align-demo-vertical',
                align='start',
                direction='vertical',
                style={
                    'backgroundColor': 'rgba(241, 241, 241, 0.6)',
                    'padding': '10px',
                },
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdRadioGroup(
                id='space-align-demo-align',
                options=['start', 'end', 'center', 'baseline'],
                value='start',
            ),
            fac.AntdParagraph('Horizontal:'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(0, 146, 255, 1)',
                            'height': '25px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '10px',
                            'width': '50px',
                        }
                    ),
                ],
                id='space-align-demo-horizontal',
                align='start',
                style={
                    'backgroundColor': 'rgba(241, 241, 241, 0.6)',
                    'padding': '10px',
                },
            ),
            fac.AntdParagraph('Vertical:'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(0, 146, 255, 1)',
                            'height': '50px',
                            'width': '25px',
                        }
                    ),
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    ),
                ],
                id='space-align-demo-vertical',
                align='start',
                direction='vertical',
                style={
                    'backgroundColor': 'rgba(241, 241, 241, 0.6)',
                    'padding': '10px',
                },
            ),
        ]

    return demo_contents


@app.callback(
    Output('space-align-demo-horizontal', 'align'),
    Output('space-align-demo-vertical', 'align'),
    Input('space-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value, value


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdRadioGroup(
        id='space-align-demo-align',
        options=['start', 'end', 'center', 'baseline'],
        value='start',
    ),
    fac.AntdParagraph('水平方向：'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '25px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '10px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-horizontal',
        align='start',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
    fac.AntdParagraph('竖直方向：'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '50px',
                    'width': '25px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-vertical',
        align='start',
        direction='vertical',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
]

...

@app.callback(
    Output('space-align-demo-horizontal', 'align'),
    Output('space-align-demo-vertical', 'align'),
    Input('space-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value, value
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdRadioGroup(
        id='space-align-demo-align',
        options=['start', 'end', 'center', 'baseline'],
        value='start',
    ),
    fac.AntdParagraph('Horizontal:'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '25px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '10px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-horizontal',
        align='start',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
    fac.AntdParagraph('Vertical:'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(0, 146, 255, 1)',
                    'height': '50px',
                    'width': '25px',
                }
            ),
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            ),
        ],
        id='space-align-demo-vertical',
        align='start',
        direction='vertical',
        style={
            'backgroundColor': 'rgba(241, 241, 241, 0.6)',
            'padding': '10px',
        },
    ),
]

...

@app.callback(
    Output('space-align-demo-horizontal', 'align'),
    Output('space-align-demo-vertical', 'align'),
    Input('space-align-demo-align', 'value'),
)
def update_demo_align(value):
    return value, value
"""
            }
        ]

```

### `views/AntdSpace/demos/basic_usage.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = [
            fac.AntdDivider('水平方向（默认）', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    )
                ]
                * 3
            ),
            fac.AntdDivider('竖直方向', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    )
                ]
                * 3,
                direction='vertical',
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider('Horizontal', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    )
                ]
                * 3
            ),
            fac.AntdDivider('Vertical', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    html.Div(
                        style={
                            'backgroundColor': 'rgba(64, 173, 255, 1)',
                            'height': '50px',
                            'width': '50px',
                        }
                    )
                ]
                * 3,
                direction='vertical',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDivider('水平方向（默认）', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3
    ),
    fac.AntdDivider('竖直方向', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3,
        direction='vertical',
    ),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider('Horizontal', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3
    ),
    fac.AntdDivider('Vertical', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3,
        direction='vertical',
    ),
]
"""
            }
        ]

```

### `views/AntdSpace/demos/custom_split_line.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3,
        customSplit=html.Div(
            style={'height': 30, 'borderRight': '1px dashed #8c8c8c'}
        ),
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        html.Div(
            style={
                'backgroundColor': 'rgba(64, 173, 255, 1)',
                'height': '50px',
                'width': '50px',
            }
        )
    ]
    * 3,
    customSplit=html.Div(
        style={'height': 30, 'borderRight': '1px dashed #8c8c8c'}
    ),
)
"""
    }
]

```

### `views/AntdSpace/demos/size.py`
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
                id='space-size-demo-size',
                options=['small', 'middle', 'large', '66'],
                value='small',
            ),
            fac.AntdSpace(
                [fac.AntdButton('child', type='primary')] * 4,
                id='space-size-demo',
            ),
        ],
        direction='vertical',
        size='large',
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    Output('space-size-demo', 'size'),
    Input('space-size-demo-size', 'value'),
)
def update_demo_size(value):
    if value == '66':
        return 66

    return value


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='space-size-demo-size',
            options=['small', 'middle', 'large', '66'],
            value='small',
        ),
        fac.AntdSpace(
            [fac.AntdButton('child', type='primary')] * 4,
            id='space-size-demo',
        ),
    ],
    direction='vertical',
    size='large',
    style={'width': '100%'},
)

...

@app.callback(
    Output('space-size-demo', 'size'),
    Input('space-size-demo-size', 'value'),
)
def update_demo_size(value):
    if value == '66':
        return 66

    return value
"""
    }
]

```

### `views/AntdSpace/demos/split_line.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            html.Div(
                style={
                    'backgroundColor': 'rgba(64, 173, 255, 1)',
                    'height': '50px',
                    'width': '50px',
                }
            )
        ]
        * 3,
        addSplitLine=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        html.Div(
            style={
                'backgroundColor': 'rgba(64, 173, 255, 1)',
                'height': '50px',
                'width': '50px',
            }
        )
    ]
    * 3,
    addSplitLine=True,
)
"""
    }
]

```

### `views/AntdSpace/demos/wrap.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdButton('child', type='primary')] * 25, wrap=True
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdButton('child', type='primary')] * 25, wrap=True
)
"""
    }
]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, embedded elements.

- id (string; optional):
    Unique ID for the component.

- addSplitLine (boolean; default False):
    Whether to add a separator line. Default value: `False`.

- align (a value equal to: 'start', 'end', 'center', 'baseline'; optional):
    Alignment method, with options `start`, `end`, `center`, `baseline`.

- aria-* (string; optional):
    Wildcard for `aria-*` attribute format.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- classNames (dict; optional):
    Fine-grained control over the CSS classes of child elements.

    `classNames` is a dict with keys:

    - item (string; optional):
        CSS class for the child item container element.

- customSplit (a list of or a singular dash component, string or number; optional):
    Custom separator line element.

- data-* (string; optional):
    Wildcard for `data-*` attribute format.

- direction (a value equal to: 'vertical', 'horizontal'; default 'horizontal'):
    Layout direction, with options `vertical`, `horizontal`. Default value: `horizontal`.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- loading_state (dict; optional):

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is currently loading.

    - prop_name (string; optional):
        Holds which property is currently loading.

- size (a value equal to: 'small', 'middle', 'large' | number; default 'small'):
    Spacing between child elements, with options `small`, `middle`, `large`, or a numeric value representing pixel spacing.
    Default value: `small`.

- style (dict; optional):
    The CSS style for the current component.

- styles (dict; optional):
    Fine-grained control over the CSS styles of child elements.

    `styles` is a dict with keys:

    - item (dict; optional):
        CSS style for the child item container element.

- wrap (boolean; default False):
    Whether child elements automatically wrap to the next line, only effective when `direction='horizontal'`. Default value: `False`.
