# AntdIcon

## 简介源码：`views/AntdIcon/intro.py`
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
                {'title': translator.t('AntdIcon 图标')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdIcon 图标'), level=2),
        fac.AntdParagraph(translator.t('用于提示不同的功能及场景。')),
    ]

```

## 示例源码（demos）

### `views/AntdIcon/demos/basic_callbacks.py`
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
                        fac.AntdText('常规点击事件：'),
                        fac.AntdIcon(
                            id='icon-basic-event',
                            icon='antd-thunderbolt',
                            style={'cursor': 'pointer'},
                        ),
                        fac.AntdText(id='icon-basic-event-output'),
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdText('防抖点击事件：'),
                        fac.AntdIcon(
                            id='icon-debounce-event',
                            icon='antd-thunderbolt',
                            debounceWait=300,
                            style={'cursor': 'pointer'},
                        ),
                        fac.AntdText(id='icon-debounce-event-output'),
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
                        fac.AntdText('Regular click event:'),
                        fac.AntdIcon(
                            id='icon-basic-event',
                            icon='antd-thunderbolt',
                            style={'cursor': 'pointer'},
                        ),
                        fac.AntdText(id='icon-basic-event-output'),
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdText('Debounced click event:'),
                        fac.AntdIcon(
                            id='icon-debounce-event',
                            icon='antd-thunderbolt',
                            debounceWait=300,
                            style={'cursor': 'pointer'},
                        ),
                        fac.AntdText(id='icon-debounce-event-output'),
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
    Output('icon-basic-event-output', 'children'),
    Input('icon-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('icon-debounce-event-output', 'children'),
    Input('icon-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_debounce_event(nClicks):
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
                fac.AntdText('常规点击事件：'),
                fac.AntdIcon(
                    id='icon-basic-event',
                    icon='antd-thunderbolt',
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdText('防抖点击事件：'),
                fac.AntdIcon(
                    id='icon-debounce-event',
                    icon='antd-thunderbolt',
                    debounceWait=300,
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-debounce-event-output'),
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
    Output('icon-basic-event-output', 'children'),
    Input('icon-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('icon-debounce-event-output', 'children'),
    Input('icon-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_debounce_event(nClicks):
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
                fac.AntdText('Regular click event:'),
                fac.AntdIcon(
                    id='icon-basic-event',
                    icon='antd-thunderbolt',
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdText('Debounced click event:'),
                fac.AntdIcon(
                    id='icon-debounce-event',
                    icon='antd-thunderbolt',
                    debounceWait=300,
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-debounce-event-output'),
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
    Output('icon-basic-event-output', 'children'),
    Input('icon-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('icon-debounce-event-output', 'children'),
    Input('icon-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_debounce_event(nClicks):
    return f'nClicks: {nClicks}'
"""
            }
        ]

```

### `views/AntdIcon/demos/basic_usage.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component

from config import DemosConfig
from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdRow(
            [
                fac.AntdCol(
                    fac.AntdSpace(
                        [
                            # 懒加载优化
                            fuc.FefferyLazyLoad(
                                fac.AntdIcon(icon=icon, style={'fontSize': 26}),
                                height=44,
                            ),
                            fac.AntdText(
                                icon,
                                locale='zh-cn',
                                copyable=True,
                                style={'borderBottom': '1px dashed #e1dfdd'},
                            ),
                        ],
                        direction='vertical',
                        size=0,
                        style={
                            'display': 'flex',
                            'alignItems': 'center',
                            'justifyContent': 'center',
                            'marginBottom': '5px',
                        },
                    ),
                    # 响应式显示优化
                    xs=24,
                    sm=12,
                    md=12,
                    lg=12,
                    xl=8,
                    xxl=6,
                )
                for icon in DemosConfig.all_icons
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdRow(
            [
                fac.AntdCol(
                    fac.AntdSpace(
                        [
                            # lazy load optimization
                            fuc.FefferyLazyLoad(
                                fac.AntdIcon(icon=icon, style={'fontSize': 26}),
                                height=44,
                            ),
                            fac.AntdText(
                                icon,
                                locale='en-us',
                                copyable=True,
                                style={'borderBottom': '1px dashed #e1dfdd'},
                            ),
                        ],
                        direction='vertical',
                        size=0,
                        style={
                            'display': 'flex',
                            'alignItems': 'center',
                            'justifyContent': 'center',
                            'marginBottom': '5px',
                        },
                    ),
                    # responsive display optimization
                    xs=24,
                    sm=12,
                    md=12,
                    lg=12,
                    xl=8,
                    xxl=6,
                )
                for icon in DemosConfig.all_icons
            ]
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdSpace(
                [
                    # 懒加载优化
                    fuc.FefferyLazyLoad(
                        fac.AntdIcon(icon=icon, style={'fontSize': 26}),
                        height=44,
                    ),
                    fac.AntdText(
                        icon,
                        locale='zh-cn',
                        copyable=True,
                        style={'borderBottom': '1px dashed #e1dfdd'},
                    ),
                ],
                direction='vertical',
                size=0,
                style={
                    'display': 'flex',
                    'alignItems': 'center',
                    'justifyContent': 'center',
                    'marginBottom': '5px',
                },
            ),
            # 响应式显示优化
            xs=24,
            sm=12,
            md=12,
            lg=12,
            xl=8,
            xxl=6,
        )
        for icon in DemosConfig.all_icons
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdSpace(
                [
                    # lazy load optimization
                    fuc.FefferyLazyLoad(
                        fac.AntdIcon(icon=icon, style={'fontSize': 26}),
                        height=44,
                    ),
                    fac.AntdText(
                        icon,
                        locale='en-us',
                        copyable=True,
                        style={'borderBottom': '1px dashed #e1dfdd'},
                    ),
                ],
                direction='vertical',
                size=0,
                style={
                    'display': 'flex',
                    'alignItems': 'center',
                    'justifyContent': 'center',
                    'marginBottom': '5px',
                },
            ),
            # responsive display optimization
            xs=24,
            sm=12,
            md=12,
            lg=12,
            xl=8,
            xxl=6,
        )
        for icon in DemosConfig.all_icons
    ]
)
"""
            }
        ]

```

### `views/AntdIcon/demos/use_iconfont.py`
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
                    fac.AntdIcon(
                        icon=icon,
                        mode='iconfont',
                        scriptUrl='//at.alicdn.com/t/font_8d5l8fzk5b87iudi.js',
                    )
                    for icon in ['icon-tuichu', 'icon-facebook', 'icon-twitter']
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdIcon(
                        icon=icon,
                        mode='iconfont',
                        scriptUrl=[
                            '//at.alicdn.com/t/font_1788044_0dwu4guekcwr.js',
                            '//at.alicdn.com/t/font_1788592_a5xf2bdic3u.js',
                        ],
                    )
                    for icon in [
                        'icon-javascript',
                        'icon-java',
                        'icon-shoppingcart',
                        'icon-python',
                    ]
                ]
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
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
                fac.AntdIcon(
                    icon=icon,
                    mode='iconfont',
                    scriptUrl='//at.alicdn.com/t/font_8d5l8fzk5b87iudi.js',
                )
                for icon in ['icon-tuichu', 'icon-facebook', 'icon-twitter']
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdIcon(
                    icon=icon,
                    mode='iconfont',
                    scriptUrl=[
                        '//at.alicdn.com/t/font_1788044_0dwu4guekcwr.js',
                        '//at.alicdn.com/t/font_1788592_a5xf2bdic3u.js',
                    ],
                )
                for icon in [
                    'icon-javascript',
                    'icon-java',
                    'icon-shoppingcart',
                    'icon-python',
                ]
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
        }
    ]

```

## API 文档

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- debounceWait (number; default 0):
    Debounce delay for the icon click event listener, in milliseconds. Default value: `0`.

- icon (string; optional):
    Name of the icon.

- key (string; optional):
    Updating the `key` value of the current component can force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:
    - component_name (string; optional):
        Holds the name of the component that is loading.
    - is_loading (boolean; optional):
        Determines if the component is loading or not.
    - prop_name (string; optional):
        Holds which property is loading.

- nClicks (number; default 0):
    Number of times the icon has been clicked, used to monitor icon click behavior. Default value: `0`.

- style (dict; optional):
    CSS styles for the current component.
