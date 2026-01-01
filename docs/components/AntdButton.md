# AntdButton

## 简介源码：`views/AntdButton/intro.py`
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
                {'title': translator.t('通用')},
                {'title': translator.t('AntdButton 按钮')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdButton 按钮'), level=2),
        fac.AntdParagraph(translator.t('按钮用于触发一个即时操作。')),
    ]

```

## 示例源码（demos）

### `views/AntdButton/demos/as_link.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdButton(
            'fac文档首页', type='primary', href='/', target='_blank'
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdButton(
            'fac documentation', type='primary', href='/', target='_blank'
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdButton(
    'fac文档首页', type='primary', href='/', target='_blank'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdButton(
    'fac documentation', type='primary', href='/', target='_blank'
)
"""
            }
        ]

```

### `views/AntdButton/demos/auto_insert_space.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdButton('汉字'), fac.AntdButton('汉字', autoInsertSpace=False)],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdButton('汉字'), fac.AntdButton('汉字', autoInsertSpace=False)],
    wrap=True,
)
"""
    }
]

```

### `views/AntdButton/demos/auto_spin.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type, autoSpin=True)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, autoSpin=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdButton/demos/auto_spin_callback.py`
```python
import time
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app
from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdButton(
            '按钮示例',
            id='button-auto-spin-demo',
            loadingChildren='计算中',
            autoSpin=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdButton(
            'Button',
            id='button-auto-spin-demo',
            loadingChildren='Calculating',
            autoSpin=True,
        )

    return demo_contents


@app.callback(
    Output('button-auto-spin-demo', 'loading'),
    Input('button-auto-spin-demo', 'nClicks'),
    prevent_initial_call=True,
)
def button_auto_spin_demo(nClicks):
    # 模拟计算任务耗时
    # simulate calculation
    time.sleep(2)

    return False


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdButton(
    '按钮示例',
    id='button-auto-spin-demo',
    loadingChildren='计算中',
    autoSpin=True,
)

...

@app.callback(
    Output('button-auto-spin-demo', 'loading'),
    Input('button-auto-spin-demo', 'nClicks'),
    prevent_initial_call=True,
)
def button_auto_spin_demo(nClicks):
    # 模拟计算任务耗时
    time.sleep(2)

    return False
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdButton(
    'Button',
    id='button-auto-spin-demo',
    loadingChildren='Calculating',
    autoSpin=True,
)

...

@app.callback(
    Output('button-auto-spin-demo', 'loading'),
    Input('button-auto-spin-demo', 'nClicks'),
    prevent_initial_call=True,
)
def button_auto_spin_demo(nClicks):
    # simulate calculation
    time.sleep(2)

    return False
"""
            }
        ]

```

### `views/AntdButton/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app
from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdButton('常规点击监听', id='button-basic-event'),
                        fac.AntdText(id='button-basic-event-output'),
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdButton(
                            '防抖点击监听',
                            id='button-debounce-event',
                            debounceWait=300,
                        ),
                        fac.AntdText(id='button-debounce-event-output'),
                    ]
                ),
            ],
            direction='vertical',
            style={
                'width': '100%',
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdButton('Basic Event', id='button-basic-event'),
                        fac.AntdText(id='button-basic-event-output'),
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdButton(
                            'Debounce Event',
                            id='button-debounce-event',
                            debounceWait=300,
                        ),
                        fac.AntdText(id='button-debounce-event-output'),
                    ]
                ),
            ],
            direction='vertical',
            style={
                'width': '100%',
            },
        )

    return demo_contents


@app.callback(
    Output('button-basic-event-output', 'children'),
    Input('button-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('button-debounce-event-output', 'children'),
    Input('button-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_debounce_event(nClicks):
    return f'nClicks: {nClicks}'


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdButton('常规点击监听', id='button-basic-event'),
                fac.AntdText(id='button-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdButton(
                    '防抖点击监听', id='button-debounce-event', debounceWait=300
                ),
                fac.AntdText(id='button-debounce-event-output'),
            ]
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('button-basic-event-output', 'children'),
    Input('button-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('button-debounce-event-output', 'children'),
    Input('button-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_debounce_event(nClicks):
    return f'nClicks: {nClicks}'
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdButton('Basic Event', id='button-basic-event'),
                fac.AntdText(id='button-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdButton(
                    'Debounce Event',
                    id='button-debounce-event',
                    debounceWait=300,
                ),
                fac.AntdText(id='button-debounce-event-output'),
            ]
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('button-basic-event-output', 'children'),
    Input('button-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('button-debounce-event-output', 'children'),
    Input('button-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def button_debounce_event(nClicks):
    return f'nClicks: {nClicks}'
"""
            }
        ]

```

### `views/AntdButton/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdButton('按钮示例')

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdButton('Button')

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdButton('按钮示例')
"""
            },
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdButton('Button')
"""
            },
        ]

```

### `views/AntdButton/demos/block_button.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdButton('按钮示例', type='primary', block=True)
    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdButton('Button', type='primary', block=True)

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdButton('按钮示例', type='primary', block=True)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdButton('Button', type='primary', block=True)
"""
            }
        ]

```

### `views/AntdButton/demos/button_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdSpace(
            [
                fac.AntdButton(
                    'fac文档首页', icon=fac.AntdIcon(icon='antd-search')
                ),
                fac.AntdButton(
                    'fac文档首页',
                    icon=fac.AntdIcon(icon='antd-search'),
                    iconPosition='end',
                ),
            ],
            wrap=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdButton(
                    'fac documentation', icon=fac.AntdIcon(icon='antd-search')
                ),
                fac.AntdButton(
                    'fac documentation',
                    icon=fac.AntdIcon(icon='antd-search'),
                    iconPosition='end',
                ),
            ],
            wrap=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            'fac文档首页', icon=fac.AntdIcon(icon='antd-search')
        ),
        fac.AntdButton(
            'fac文档首页',
            icon=fac.AntdIcon(icon='antd-search'),
            iconPosition='end',
        ),
    ],
    wrap=True
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            'fac documentation', icon=fac.AntdIcon(icon='antd-search')
        ),
        fac.AntdButton(
            'fac documentation',
            icon=fac.AntdIcon(icon='antd-search'),
            iconPosition='end',
        ),
    ],
    wrap=True,
)
"""
            }
        ]

```

### `views/AntdButton/demos/button_loading.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type, loading=True)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, loading=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdButton/demos/button_shape.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(shape, type='primary', shape=shape)
            for shape in ['default', 'circle', 'round']
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(shape, type='primary', shape=shape)
        for shape in ['default', 'circle', 'round']
    ],
    wrap=True
)
"""
    }
]

```

### `views/AntdButton/demos/button_types.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
"""
    }
]

```

### `views/AntdButton/demos/click_execute_js.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = [
            fac.AntdSpace(
                [
                    fac.AntdButton(
                        '执行js', clickExecuteJsString='alert("执行js示例")'
                    ),
                    fac.AntdButton(
                        '打开模态框',
                        clickExecuteJsString='dash_clientside.set_props("button-click-execute-js-modal", {"visible": true})',
                    ),
                ],
                wrap=True,
            ),
            # 示例模态框
            fac.AntdModal(
                '这是一个示例模态框',
                id='button-click-execute-js-modal',
                title='示例模态框',
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdSpace(
                [
                    fac.AntdButton(
                        'Execute js',
                        clickExecuteJsString='alert("Execute js example")',
                    ),
                    fac.AntdButton(
                        'Open modal',
                        clickExecuteJsString='dash_clientside.set_props("button-click-execute-js-modal", {"visible": true})',
                    ),
                ],
                wrap=True,
            ),
            # example modal
            fac.AntdModal(
                'This is an example modal',
                id='button-click-execute-js-modal',
                title='Example modal',
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
    fac.AntdSpace(
        [
            fac.AntdButton(
                '执行js', clickExecuteJsString='alert("执行js示例")'
            ),
            fac.AntdButton(
                '打开模态框',
                clickExecuteJsString='dash_clientside.set_props("button-click-execute-js-modal", {"visible": true})',
            ),
        ],
        wrap=True,
    ),
    # 示例模态框
    fac.AntdModal(
        '这是一个示例模态框',
        id='button-click-execute-js-modal',
        title='示例模态框',
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
    fac.AntdSpace(
        [
            fac.AntdButton(
                'Execute js',
                clickExecuteJsString='alert("Execute js example")',
            ),
            fac.AntdButton(
                'Open modal',
                clickExecuteJsString='dash_clientside.set_props("button-click-execute-js-modal", {"visible": true})',
            ),
        ],
        wrap=True,
    ),
    # example modal
    fac.AntdModal(
        'This is an example modal',
        id='button-click-execute-js-modal',
        title='Example modal',
    ),
]
"""
            }
        ]

```

### `views/AntdButton/demos/color_and_variant.py`
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
                    f'color: {color}',
                    *[
                        fac.AntdButton(variant, color=color, variant=variant)
                        for variant in [
                            'outlined',
                            'dashed',
                            'solid',
                            'filled',
                            'text',
                            'link',
                        ]
                    ],
                ],
                wrap=True,
            )
            for color in [
                'default',
                'primary',
                'danger',
                'blue',
                'purple',
                'cyan',
                'green',
                'magenta',
                'pink',
                'red',
                'orange',
                'yellow',
                'volcano',
                'geekblue',
                'lime',
                'gold',
            ]
        ],
        direction='vertical',
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    return [
        {
            'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                f'color: {color}',
                *[
                    fac.AntdButton(variant, color=color, variant=variant)
                    for variant in [
                        'outlined',
                        'dashed',
                        'solid',
                        'filled',
                        'text',
                        'link',
                    ]
                ],
            ],
            wrap=True,
        )
        for color in [
            'default',
            'primary',
            'danger',
            'blue',
            'purple',
            'cyan',
            'green',
            'magenta',
            'pink',
            'red',
            'orange',
            'yellow',
            'volcano',
            'geekblue',
            'lime',
            'gold',
        ]
    ],
    direction='vertical',
)
"""
        },
    ]

```

### `views/AntdButton/demos/danger_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type, danger=True)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, danger=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
"""
    }
]

```

### `views/AntdButton/demos/disabled_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type, disabled=True)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, disabled=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],
    wrap=True
)
"""
    }
]

```

### `views/AntdButton/demos/ghost_background.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(button_type, type=button_type, ghost=True)
            for button_type in [
                'primary',
                'default',
                'dashed',
                'text',
                'link',
            ]
        ],
        wrap=True,
        style={'background': '#d9d9d9', 'padding': 8},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(button_type, type=button_type, ghost=True)
        for button_type in [
            'primary',
            'default',
            'dashed',
            'text',
            'link',
        ]
    ],,
    wrap=True,
    style={'background': '#d9d9d9', 'padding': 8},
)
"""
    }
]

```

### `views/AntdButton/demos/motion_type.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdButton(
            '点我试试', type='primary', motionType='happy-work'
        )
    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdButton(
            'Click me', type='primary', motionType='happy-work'
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdButton(
    '点我试试', type='primary', motionType='happy-work'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdButton(
    'Click me', type='primary', motionType='happy-work'
)
"""
            }
        ]

```

### `views/AntdButton/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(size, size=size)
            for size in ['small', 'middle', 'large']
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(size, size=size)
        for size in ['small', 'middle', 'large']
    ],
    wrap=True,
)
"""
    }
]

```

## API 文档


- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- children (a list of or a singular dash component, string or number; optional):
    Component type, the embedded element inside the button.

- style (dict; optional):
    The CSS style of the current component.

- className (string | dict; optional):
    The CSS class name of the current component, supports [dynamic CSS class names](/advanced-classname).

- styles (dict; optional):
    Fine-grained control over the CSS styles of child elements.

    `styles` is a dict with keys:

    - icon (dict; optional):
        The CSS style for the button icon element.

- classNames (dict; optional):
    Fine-grained control over the CSS class names of child elements.

    `classNames` is a dict with keys:

    - icon (string; optional):
        The CSS class name for the button icon element.

- loadingChildren (a list of or a singular dash component, string or number; optional):
    Component type, the embedded element displayed when the button is in a loading state.

- type (a value equal to: 'default', 'primary', 'dashed', 'link', 'text'; default 'default'):
    The type of button, with options `'default'`, `'primary'`, `'dashed'`, `'link'`, `'text'`.
    Default value: `'default'`.

- href (string; optional):
    The link address for the button to jump to when clicked.

- target (string; default '_blank'):
    The method of the link to jump when the button is clicked. Default value: `'_blank'`.

- autoInsertSpace (boolean; default True):
    Whether to insert a space between two Chinese characters in the button. Default value: `True`.

- block (boolean; default False):
    Whether the button is rendered as a block-level element (width fills the parent container). Default value: `False`.

- danger (boolean; default False):
    Whether the button presents a danger style. Default value: `False`.

- disabled (boolean; default False):
    Whether the button presents a disabled state. Default value: `False`.

- ghost (boolean; default False):
    Whether the button presents a transparent background state. Default value: `False`.

- shape (a value equal to: 'default', 'circle', 'round'; default 'default'):
    The shape of the button, with options `'default'`, `'circle'`, `'round'`. Default value: `'default'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    The size specification of the button, with options `'small'`, `'middle'`, `'large'`. Default value: `'middle'`.

- nClicks (number; default 0):
    The cumulative number of button clicks, used to monitor button click behavior. Default value: `0`.

- clickExecuteJsString (string; optional):
    The string of JavaScript code to be executed when the button is clicked.

- debounceWait (number; default 0):
    The debounce delay for the button click event listener, in milliseconds. Default value: `0`.

- icon (a list of or a singular dash component, string or number; optional):
    Component type, the prefix icon element embedded before the button.

- iconPosition (a value equal to: 'start', 'end'; default 'start'):
    The position of the button icon component, with options `'start'`, `'end'`. Default value: `'start'`.

- loading (boolean; optional):
    Whether the button presents a loading state. Default value: `False`.

- autoSpin (boolean; default False):
    Whether the current button automatically enters a loading state after each click. Default value: `False`.

- motionType (a value equal to: 'happy-work'; optional):
    The additional special interaction type of the button, with options `'happy-work'`.

- color (a value equal to: 'default', 'primary', 'danger'; optional):
    The color style of the button, with options `'default'`, `'primary'`, `'danger'`.

- variant (a value equal to: 'outlined', 'dashed', 'solid', 'filled', 'text', 'link'; optional):
    The variant type, with options `'outlined'`, `'dashed'`, `'solid'`, `'filled'`, `'text'`, `'link'`.

- title (string; optional):
    The native button title attribute.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
