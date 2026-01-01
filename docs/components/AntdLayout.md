# AntdLayout

## 简介源码：`views/AntdLayout/intro.py`
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
                {'title': translator.t('经典布局')},
                {'title': translator.t('AntdLayout 布局容器')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdLayout 布局容器'), level=2),
        fac.AntdParagraph(translator.t('用于在经典布局方案中作为容器。')),
    ]

```

## 示例源码（demos）

### `views/AntdLayout/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdHeader(
                    fac.AntdTitle(
                        '页首示例',
                        level=2,
                        style={'color': 'white', 'margin': '0'},
                    ),
                    style={
                        'display': 'flex',
                        'justifyContent': 'center',
                        'alignItems': 'center',
                    },
                ),
                fac.AntdLayout(
                    [
                        fac.AntdSider(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    '侧边栏示例', level=2, style={'margin': '0'}
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={
                                'backgroundColor': 'rgb(240, 242, 245)',
                                'display': 'flex',
                                'justifyContent': 'center',
                            },
                        ),
                        fac.AntdLayout(
                            [
                                fac.AntdContent(
                                    fac.AntdCenter(
                                        fac.AntdTitle(
                                            '内容区示例',
                                            level=2,
                                            style={'margin': '0'},
                                        ),
                                        style={
                                            'height': '100%',
                                        },
                                    ),
                                    style={'backgroundColor': 'white'},
                                ),
                                fac.AntdFooter(
                                    fac.AntdCenter(
                                        fac.AntdTitle(
                                            '页尾示例',
                                            level=2,
                                            style={'margin': '0'},
                                        ),
                                        style={
                                            'height': '100%',
                                        },
                                    ),
                                    style={
                                        'backgroundColor': 'rgb(193, 193, 193)',
                                        'height': '40px',
                                    },
                                ),
                            ]
                        ),
                    ],
                    style={'height': '100%'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdHeader(
                    fac.AntdTitle(
                        'Header Demo',
                        level=2,
                        style={'color': 'white', 'margin': '0'},
                    ),
                    style={
                        'display': 'flex',
                        'justifyContent': 'center',
                        'alignItems': 'center',
                    },
                ),
                fac.AntdLayout(
                    [
                        fac.AntdSider(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    'Sider Demo', level=2, style={'margin': '0'}
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={
                                'backgroundColor': 'rgb(240, 242, 245)',
                                'display': 'flex',
                                'justifyContent': 'center',
                            },
                        ),
                        fac.AntdLayout(
                            [
                                fac.AntdContent(
                                    fac.AntdCenter(
                                        fac.AntdTitle(
                                            'Content Demo',
                                            level=2,
                                            style={'margin': '0'},
                                        ),
                                        style={
                                            'height': '100%',
                                        },
                                    ),
                                    style={'backgroundColor': 'white'},
                                ),
                                fac.AntdFooter(
                                    fac.AntdCenter(
                                        fac.AntdTitle(
                                            'Footer Demo',
                                            level=2,
                                            style={'margin': '0'},
                                        ),
                                        style={
                                            'height': '100%',
                                        },
                                    ),
                                    style={
                                        'backgroundColor': 'rgb(193, 193, 193)',
                                        'height': '40px',
                                    },
                                ),
                            ]
                        ),
                    ],
                    style={'height': '100%'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdHeader(
            fac.AntdTitle(
                '页首示例', level=2, style={'color': 'white', 'margin': '0'}
            ),
            style={
                'display': 'flex',
                'justifyContent': 'center',
                'alignItems': 'center',
            },
        ),
        fac.AntdLayout(
            [
                fac.AntdSider(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '侧边栏示例', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={
                        'backgroundColor': 'rgb(240, 242, 245)',
                        'display': 'flex',
                        'justifyContent': 'center',
                    },
                ),
                fac.AntdLayout(
                    [
                        fac.AntdContent(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    '内容区示例',
                                    level=2,
                                    style={'margin': '0'},
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={'backgroundColor': 'white'},
                        ),
                        fac.AntdFooter(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    '页尾示例',
                                    level=2,
                                    style={'margin': '0'},
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={
                                'backgroundColor': 'rgb(193, 193, 193)',
                                'height': '40px',
                            },
                        ),
                    ]
                ),
            ],
            style={'height': '100%'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdHeader(
            fac.AntdTitle(
                'Header Demo',
                level=2,
                style={'color': 'white', 'margin': '0'},
            ),
            style={
                'display': 'flex',
                'justifyContent': 'center',
                'alignItems': 'center',
            },
        ),
        fac.AntdLayout(
            [
                fac.AntdSider(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Sider Demo', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={
                        'backgroundColor': 'rgb(240, 242, 245)',
                        'display': 'flex',
                        'justifyContent': 'center',
                    },
                ),
                fac.AntdLayout(
                    [
                        fac.AntdContent(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    'Content Demo',
                                    level=2,
                                    style={'margin': '0'},
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={'backgroundColor': 'white'},
                        ),
                        fac.AntdFooter(
                            fac.AntdCenter(
                                fac.AntdTitle(
                                    'Footer Demo',
                                    level=2,
                                    style={'margin': '0'},
                                ),
                                style={
                                    'height': '100%',
                                },
                            ),
                            style={
                                'backgroundColor': 'rgb(193, 193, 193)',
                                'height': '40px',
                            },
                        ),
                    ]
                ),
            ],
            style={'height': '100%'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

```

### `views/AntdLayout/demos/collapsible_sider.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    collapsible=True,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '内容区示例', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    collapsible=True,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Content Demo', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            collapsible=True,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle('内容区示例', level=2, style={'margin': '0'}),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            collapsible=True,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle(
                    'Content Demo', level=2, style={'margin': '0'}
                ),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

```

### `views/AntdLayout/demos/collapsible_sider_custom_trigger.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from server import app

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    id='sider-custom-trigger-demo',
                    collapsible=True,
                    trigger=None,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdButton(
                        '折叠/展开',
                        id='sider-custom-trigger-button-demo',
                        type='primary',
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    id='sider-custom-trigger-demo',
                    collapsible=True,
                    trigger=None,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdButton(
                        'Collapse/Expand',
                        id='sider-custom-trigger-button-demo',
                        type='primary',
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


app.clientside_callback(
    """(nClicks, collapsed) => !collapsed""",
    Output('sider-custom-trigger-demo', 'collapsed'),
    Input('sider-custom-trigger-button-demo', 'nClicks'),
    State('sider-custom-trigger-demo', 'collapsed'),
    prevent_initial_call=True,
)


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdLayout(
    [
        fac.AntdSider(
            id='sider-custom-trigger-demo',
            collapsible=True,
            trigger=None,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdButton(
                '折叠/展开',
                id='sider-custom-trigger-button-demo',
                type='primary',
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)

...

app.clientside_callback(
    """(nClicks, collapsed) => !collapsed""",
    Output('sider-custom-trigger-demo', 'collapsed'),
    Input('sider-custom-trigger-button-demo', 'nClicks'),
    State('sider-custom-trigger-demo', 'collapsed'),
    prevent_initial_call=True,
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
fac.AntdLayout(
    [
        fac.AntdSider(
            id='sider-custom-trigger-demo',
            collapsible=True,
            trigger=None,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdButton(
                'Collapse/Expand',
                id='sider-custom-trigger-button-demo',
                type='primary',
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)

...

app.clientside_callback(
    """(nClicks, collapsed) => !collapsed""",
    Output('sider-custom-trigger-demo', 'collapsed'),
    Input('sider-custom-trigger-button-demo', 'nClicks'),
    State('sider-custom-trigger-demo', 'collapsed'),
    prevent_initial_call=True,
)
'''
            }
        ]

```

### `views/AntdLayout/demos/collapsible_sider_with_menu.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    [
                        fac.AntdMenu(
                            menuItems=[
                                {
                                    'component': 'Item',
                                    'props': {
                                        'key': f'图标{icon}',
                                        'title': f'图标{icon}',
                                        'icon': icon,
                                    },
                                }
                                for icon in [
                                    'antd-home',
                                    'antd-cloud-upload',
                                    'antd-bar-chart',
                                    'antd-pie-chart',
                                    'antd-dot-chart',
                                    'antd-line-chart',
                                    'antd-apartment',
                                    'antd-app-store',
                                    'antd-app-store-add',
                                    'antd-bell',
                                    'antd-calculator',
                                    'antd-calendar',
                                    'antd-database',
                                    'antd-history',
                                ]
                            ],
                            mode='inline',
                            style={'height': '100%', 'overflow': 'hidden auto'},
                        )
                    ],
                    collapsible=True,
                    collapsedWidth=60,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '内容区示例', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    [
                        fac.AntdMenu(
                            menuItems=[
                                {
                                    'component': 'Item',
                                    'props': {
                                        'key': icon,
                                        'title': icon,
                                        'icon': icon,
                                    },
                                }
                                for icon in [
                                    'antd-home',
                                    'antd-cloud-upload',
                                    'antd-bar-chart',
                                    'antd-pie-chart',
                                    'antd-dot-chart',
                                    'antd-line-chart',
                                    'antd-apartment',
                                    'antd-app-store',
                                    'antd-app-store-add',
                                    'antd-bell',
                                    'antd-calculator',
                                    'antd-calendar',
                                    'antd-database',
                                    'antd-history',
                                ]
                            ],
                            mode='inline',
                            style={'height': '100%', 'overflow': 'hidden auto'},
                        )
                    ],
                    collapsible=True,
                    collapsedWidth=60,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Content Demo', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            [
                fac.AntdMenu(
                    menuItems=[
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'图标{icon}',
                                'title': f'图标{icon}',
                                'icon': icon,
                            },
                        }
                        for icon in [
                            'antd-home',
                            'antd-cloud-upload',
                            'antd-bar-chart',
                            'antd-pie-chart',
                            'antd-dot-chart',
                            'antd-line-chart',
                            'antd-apartment',
                            'antd-app-store',
                            'antd-app-store-add',
                            'antd-bell',
                            'antd-calculator',
                            'antd-calendar',
                            'antd-database',
                            'antd-history',
                        ]
                    ],
                    mode='inline',
                    style={'height': '100%', 'overflow': 'hidden auto'},
                )
            ],
            collapsible=True,
            collapsedWidth=60,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle('内容区示例', level=2, style={'margin': '0'}),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            [
                fac.AntdMenu(
                    menuItems=[
                        {
                            'component': 'Item',
                            'props': {
                                'key': icon,
                                'title': icon,
                                'icon': icon,
                            },
                        }
                        for icon in [
                            'antd-home',
                            'antd-cloud-upload',
                            'antd-bar-chart',
                            'antd-pie-chart',
                            'antd-dot-chart',
                            'antd-line-chart',
                            'antd-apartment',
                            'antd-app-store',
                            'antd-app-store-add',
                            'antd-bell',
                            'antd-calculator',
                            'antd-calendar',
                            'antd-database',
                            'antd-history',
                        ]
                    ],
                    mode='inline',
                    style={'height': '100%', 'overflow': 'hidden auto'},
                )
            ],
            collapsible=True,
            collapsedWidth=60,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle(
                    'Content Demo', level=2, style={'margin': '0'}
                ),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

```

### `views/AntdLayout/demos/responsive_collapsible_sider.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    breakpoint='xl',
                    collapsible=True,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '内容区示例', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdSider(
                    breakpoint='xl',
                    collapsible=True,
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Content Demo', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'white'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            breakpoint='xl',
            collapsible=True,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle('内容区示例', level=2, style={'margin': '0'}),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdSider(
            breakpoint='xl',
            collapsible=True,
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle(
                    'Content Demo', level=2, style={'margin': '0'}
                ),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'white'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

```

### `views/AntdLayout/demos/right_sider.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdLayout(
            [
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '内容区示例', level=2, style={'margin': '0'}
                        ),
                        style={'height': '100%'},
                    ),
                    style={'backgroundColor': 'white'},
                ),
                fac.AntdSider(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            '右侧侧边栏', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
            ],
            style={'height': '100vh'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdLayout(
            [
                fac.AntdContent(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Content Demo', level=2, style={'margin': '0'}
                        ),
                        style={'height': '100%'},
                    ),
                    style={'backgroundColor': 'white'},
                ),
                fac.AntdSider(
                    fac.AntdCenter(
                        fac.AntdTitle(
                            'Right Sider', level=2, style={'margin': '0'}
                        ),
                        style={
                            'height': '100%',
                        },
                    ),
                    style={'backgroundColor': 'rgb(240, 242, 245)'},
                ),
            ],
            style={'height': '100vh'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle('内容区示例', level=2, style={'margin': '0'}),
                style={'height': '100%'},
            ),
            style={'backgroundColor': 'white'},
        ),
        fac.AntdSider(
            fac.AntdCenter(
                fac.AntdTitle('右侧侧边栏', level=2, style={'margin': '0'}),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdLayout(
    [
        fac.AntdContent(
            fac.AntdCenter(
                fac.AntdTitle(
                    'Content Demo', level=2, style={'margin': '0'}
                ),
                style={'height': '100%'},
            ),
            style={'backgroundColor': 'white'},
        ),
        fac.AntdSider(
            fac.AntdCenter(
                fac.AntdTitle(
                    'Right Sider', level=2, style={'margin': '0'}
                ),
                style={
                    'height': '100%',
                },
            ),
            style={'backgroundColor': 'rgb(240, 242, 245)'},
        ),
    ],
    style={'height': '100vh'},
)
"""
            }
        ]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, for embedded elements.

- id (string; optional):
    The unique identifier for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` attribute format.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` attribute format.

- key (string; optional):
    Updates the `key` value of the current component, which can force a re-rendering of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with the following keys:

    - component_name (string; optional):
        Holds the name of the component that is currently loading.

    - is_loading (boolean; optional):
        Indicates whether the component is in a loading state or not.

    - prop_name (string; optional):
        Indicates which property of the component is currently loading.

- style (dict; optional):
    The CSS styles for the current component.
