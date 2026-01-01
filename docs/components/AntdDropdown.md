# AntdDropdown

## 简介源码：`views/AntdDropdown/intro.py`
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
                {'title': translator.t('导航')},
                {'title': translator.t('AntdDropdown 下拉菜单')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdDropdown 下拉菜单'), level=2),
        fac.AntdParagraph(
            translator.t('用于展示具有若干选项或链接的向下弹出的列表。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdDropdown/demos/basic_callbacks.py`
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
            fac.AntdDropdown(
                id='dropdown-demo',
                title='触发点',
                arrow=True,
                placement='topCenter',
                menuItems=[
                    {
                        'title': '子页面1',
                        'key': '子页面1',
                    },
                    {
                        'title': '子页面2',
                        'key': '子页面2',
                    },
                    {'isDivider': True},
                    {'title': '子页面3-1', 'key': '子页面3-1'},
                    {'title': '子页面3-2', 'key': '子页面3-2'},
                ],
            ),
            html.Div(id='dropdown-demo-output'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDropdown(
                id='dropdown-demo',
                title='Trigger point',
                arrow=True,
                placement='topCenter',
                menuItems=[
                    {
                        'title': 'Subpage1',
                        'key': 'Subpage1',
                    },
                    {
                        'title': 'Subpage2',
                        'key': 'Subpage2',
                    },
                    {'isDivider': True},
                    {'title': 'Subpage3-1', 'key': 'Subpage3-1'},
                    {'title': 'Subpage3-2', 'key': 'Subpage3-2'},
                ],
            ),
            html.Div(id='dropdown-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('dropdown-demo-output', 'children'),
    [Input('dropdown-demo', 'clickedKey'), Input('dropdown-demo', 'nClicks')],
    prevent_initial_call=True,
)
def dropdown_demo_callback(clickedKey, nClicks):
    return [
        fac.AntdText('clickedKey: ', strong=True),
        fac.AntdText(clickedKey),
        fac.AntdText('　nClicks: ', strong=True),
        fac.AntdText(nClicks),
    ]


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDropdown(
        id='dropdown-demo',
        title='触发点',
        arrow=True,
        placement='topCenter',
        menuItems=[
            {
                'title': '子页面1',
                'key': '子页面1',
            },
            {
                'title': '子页面2',
                'key': '子页面2',
            },
            {'isDivider': True},
            {'title': '子页面3-1', 'key': '子页面3-1'},
            {'title': '子页面3-2', 'key': '子页面3-2'},
        ],
    ),
    html.Div(id='dropdown-demo-output'),
]

...

@app.callback(
    Output('dropdown-demo-output', 'children'),
    [Input('dropdown-demo', 'clickedKey'), Input('dropdown-demo', 'nClicks')],
    prevent_initial_call=True,
)
def dropdown_demo_callback(clickedKey, nClicks):
    return [
        fac.AntdText('clickedKey: ', strong=True),
        fac.AntdText(clickedKey),
        fac.AntdText('　nClicks: ', strong=True),
        fac.AntdText(nClicks),
    ]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDropdown(
        id='dropdown-demo',
        title='Trigger point',
        arrow=True,
        placement='topCenter',
        menuItems=[
            {
                'title': 'Subpage1',
                'key': 'Subpage1',
            },
            {
                'title': 'Subpage2',
                'key': 'Subpage2',
            },
            {'isDivider': True},
            {'title': 'Subpage3-1', 'key': 'Subpage3-1'},
            {'title': 'Subpage3-2', 'key': 'Subpage3-2'},
        ],
    ),
    html.Div(id='dropdown-demo-output'),
]

...

@app.callback(
    Output('dropdown-demo-output', 'children'),
    [Input('dropdown-demo', 'clickedKey'), Input('dropdown-demo', 'nClicks')],
    prevent_initial_call=True,
)
def dropdown_demo_callback(clickedKey, nClicks):
    return [
        fac.AntdText('clickedKey: ', strong=True),
        fac.AntdText(clickedKey),
        fac.AntdText('　nClicks: ', strong=True),
        fac.AntdText(nClicks),
    ]
"""
            }
        ]

```

### `views/AntdDropdown/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            menuItems=[
                {'title': '选项1'},
                {'title': '选项2'},
                {'isDivider': True},
                {'title': '选项3-1'},
                {'title': '选项3-2'},
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            menuItems=[
                {'title': 'Option1'},
                {'title': 'Option2'},
                {'isDivider': True},
                {'title': 'Option3-1'},
                {'title': 'Option3-2'},
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    menuItems=[
        {'title': '选项1'},
        {'title': '选项2'},
        {'isDivider': True},
        {'title': '选项3-1'},
        {'title': '选项3-2'},
    ],
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    menuItems=[
        {'title': 'Option1'},
        {'title': 'Option2'},
        {'isDivider': True},
        {'title': 'Option3-1'},
        {'title': 'Option3-2'},
    ],
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/button_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            buttonMode=True,
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
            buttonProps={
                'icon': fac.AntdIcon(icon='antd-user'),
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            buttonMode=True,
            menuItems=[
                {'title': 'Subpage1'},
                {'title': 'Subpage2'},
                {'isDivider': True},
                {'title': 'Subpage3-1'},
                {'title': 'Subpage3-2'},
            ],
            buttonProps={
                'icon': fac.AntdIcon(icon='antd-user'),
            },
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    buttonMode=True,
    menuItems=[
        {'title': '子页面1'},
        {'title': '子页面2'},
        {'isDivider': True},
        {'title': '子页面3-1'},
        {'title': '子页面3-2'},
    ],
    buttonProps={
        'icon': fac.AntdIcon(icon='antd-user'),
    },
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    buttonMode=True,
    menuItems=[
        {'title': 'Subpage1'},
        {'title': 'Subpage2'},
        {'isDivider': True},
        {'title': 'Subpage3-1'},
        {'title': 'Subpage3-2'},
    ],
    buttonProps={
        'icon': fac.AntdIcon(icon='antd-user'),
    },
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/button_mode.py`
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
                fac.AntdDropdown(
                    title='触发点',
                    buttonMode=True,
                    menuItems=[
                        {'title': '子页面1'},
                        {'title': '子页面2'},
                        {'isDivider': True},
                        {'title': '子页面3-1'},
                        {'title': '子页面3-2'},
                    ],
                ),
                fac.AntdDropdown(
                    title='触发点',
                    buttonMode=True,
                    buttonProps={'size': 'large', 'type': 'dashed'},
                    menuItems=[
                        {'title': '子页面1'},
                        {'title': '子页面2'},
                        {'isDivider': True},
                        {'title': '子页面3-1'},
                        {'title': '子页面3-2'},
                    ],
                ),
                fac.AntdDropdown(
                    title='触发点',
                    buttonMode=True,
                    buttonProps={
                        'size': 'small',
                        'type': 'primary',
                        'danger': True,
                    },
                    menuItems=[
                        {'title': '子页面1'},
                        {'title': '子页面2'},
                        {'isDivider': True},
                        {'title': '子页面3-1'},
                        {'title': '子页面3-2'},
                    ],
                ),
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDropdown(
                    title='Trigger point',
                    buttonMode=True,
                    menuItems=[
                        {'title': 'Subpage1'},
                        {'title': 'Subpage2'},
                        {'isDivider': True},
                        {'title': 'Subpage3-1'},
                        {'title': 'Subpage3-2'},
                    ],
                ),
                fac.AntdDropdown(
                    title='Trigger point',
                    buttonMode=True,
                    buttonProps={'size': 'large', 'type': 'dashed'},
                    menuItems=[
                        {'title': 'Subpage1'},
                        {'title': 'Subpage2'},
                        {'isDivider': True},
                        {'title': 'Subpage3-1'},
                        {'title': 'Subpage3-2'},
                    ],
                ),
                fac.AntdDropdown(
                    title='Trigger point',
                    buttonMode=True,
                    buttonProps={
                        'size': 'small',
                        'type': 'primary',
                        'danger': True,
                    },
                    menuItems=[
                        {'title': 'Subpage1'},
                        {'title': 'Subpage2'},
                        {'isDivider': True},
                        {'title': 'Subpage3-1'},
                        {'title': 'Subpage3-2'},
                    ],
                ),
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
fac.AntdSpace(
    [
        fac.AntdDropdown(
            title='触发点',
            buttonMode=True,
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        ),
        fac.AntdDropdown(
            title='触发点',
            buttonMode=True,
            buttonProps={'size': 'large', 'type': 'dashed'},
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        ),
        fac.AntdDropdown(
            title='触发点',
            buttonMode=True,
            buttonProps={
                'size': 'small',
                'type': 'primary',
                'danger': True,
            },
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        ),
    ]
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
        fac.AntdDropdown(
            title='Trigger point',
            buttonMode=True,
            menuItems=[
                {'title': 'Subpage1'},
                {'title': 'Subpage2'},
                {'isDivider': True},
                {'title': 'Subpage3-1'},
                {'title': 'Subpage3-2'},
            ],
        ),
        fac.AntdDropdown(
            title='Trigger point',
            buttonMode=True,
            buttonProps={'size': 'large', 'type': 'dashed'},
            menuItems=[
                {'title': 'Subpage1'},
                {'title': 'Subpage2'},
                {'isDivider': True},
                {'title': 'Subpage3-1'},
                {'title': 'Subpage3-2'},
            ],
        ),
        fac.AntdDropdown(
            title='Trigger point',
            buttonMode=True,
            buttonProps={
                'size': 'small',
                'type': 'primary',
                'danger': True,
            },
            menuItems=[
                {'title': 'Subpage1'},
                {'title': 'Subpage2'},
                {'isDivider': True},
                {'title': 'Subpage3-1'},
                {'title': 'Subpage3-2'},
            ],
        ),
    ]
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/custom_button_style.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            buttonMode=True,
            buttonProps={
                'style': {
                    'color': 'white',
                    'width': 150,
                    'background': 'linear-gradient(135deg,#8a2be2,#ffa500,#f8f8ff)',
                }
            },
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            buttonMode=True,
            buttonProps={
                'style': {
                    'color': 'white',
                    'width': 150,
                    'background': 'linear-gradient(135deg,#8a2be2,#ffa500,#f8f8ff)',
                }
            },
            menuItems=[
                {'title': 'Option1'},
                {'title': 'Option2'},
                {'isDivider': True},
                {'title': 'Option3-1'},
                {'title': 'Option3-2'},
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    buttonMode=True,
    buttonProps={
        'style': {
            'color': 'white',
            'width': 150,
            'background': 'linear-gradient(135deg,#8a2be2,#ffa500,#f8f8ff)',
        }
    },
    menuItems=[
        {'title': '子页面1'},
        {'title': '子页面2'},
        {'isDivider': True},
        {'title': '子页面3-1'},
        {'title': '子页面3-2'},
    ],
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    buttonMode=True,
    buttonProps={
        'style': {
            'color': 'white',
            'width': 150,
            'background': 'linear-gradient(135deg,#8a2be2,#ffa500,#f8f8ff)',
        }
    },
    menuItems=[
        {'title': 'Option1'},
        {'title': 'Option2'},
        {'isDivider': True},
        {'title': 'Option3-1'},
        {'title': 'Option3-2'},
    ],
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/custom_children.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            fac.AntdAvatar(
                icon='antd-user',
                size='large',
                style={'background': '#1890ff', 'cursor': 'pointer'},
            ),
            menuItems=[
                {
                    'title': fac.AntdSpace(
                        [
                            fac.AntdAvatar(
                                text='我',
                                mode='text',
                                style={'background': '#2f54eb'},
                            ),
                            fac.AntdSpace(
                                [
                                    '用户示例',
                                    fac.AntdTag(content='vip', color='red'),
                                ],
                                direction='vertical',
                                size=0,
                            ),
                        ]
                    )
                }
            ],
            trigger='hover',
            placement='bottomRight',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            fac.AntdAvatar(
                icon='antd-user',
                size='large',
                style={'background': '#1890ff', 'cursor': 'pointer'},
            ),
            menuItems=[
                {
                    'title': fac.AntdSpace(
                        [
                            fac.AntdAvatar(
                                text='Me',
                                mode='text',
                                style={'background': '#2f54eb'},
                            ),
                            fac.AntdSpace(
                                [
                                    'User example',
                                    fac.AntdTag(content='vip', color='red'),
                                ],
                                direction='vertical',
                                size=0,
                            ),
                        ]
                    )
                }
            ],
            trigger='hover',
            placement='bottomRight',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    fac.AntdAvatar(
        icon='antd-user',
        size='large',
        style={'background': '#1890ff', 'cursor': 'pointer'},
    ),
    menuItems=[
        {
            'title': fac.AntdSpace(
                [
                    fac.AntdAvatar(
                        text='我',
                        mode='text',
                        style={'background': '#2f54eb'},
                    ),
                    fac.AntdSpace(
                        [
                            '用户示例',
                            fac.AntdTag(content='vip', color='red'),
                        ],
                        direction='vertical',
                        size=0,
                    ),
                ]
            )
        }
    ],
    trigger='hover',
    placement='bottomRight',
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    fac.AntdAvatar(
        icon='antd-user',
        size='large',
        style={'background': '#1890ff', 'cursor': 'pointer'},
    ),
    menuItems=[
        {
            'title': fac.AntdSpace(
                [
                    fac.AntdAvatar(
                        text='Me',
                        mode='text',
                        style={'background': '#2f54eb'},
                    ),
                    fac.AntdSpace(
                        [
                            'User example',
                            fac.AntdTag(content='vip', color='red'),
                        ],
                        direction='vertical',
                        size=0,
                    ),
                ]
            )
        }
    ],
    trigger='hover',
    placement='bottomRight',
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/dropdown_arrow.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            arrow=True,
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            arrow=True,
            menuItems=[
                {'title': 'Subpage1'},
                {'title': 'Subpage2'},
                {'isDivider': True},
                {'title': 'Subpage3-1'},
                {'title': 'Subpage3-2'},
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    arrow=True,
    menuItems=[
        {'title': '子页面1'},
        {'title': '子页面2'},
        {'isDivider': True},
        {'title': '子页面3-1'},
        {'title': '子页面3-2'},
    ],
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    arrow=True,
    menuItems=[
        {'title': 'Subpage1'},
        {'title': 'Subpage2'},
        {'isDivider': True},
        {'title': 'Subpage3-1'},
        {'title': 'Subpage3-2'},
    ],
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/dropdown_placement.py`
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
                fac.AntdDropdown(
                    title=placement,
                    arrow=True,
                    placement=placement,
                    menuItems=[
                        {'title': '子页面1'},
                        {'title': '子页面2'},
                        {'isDivider': True},
                        {'title': '子页面3-1'},
                        {'title': '子页面3-2'},
                    ],
                )
                for placement in [
                    'bottomLeft',
                    'bottomCenter',
                    'bottomRight',
                    'topLeft',
                    'topCenter',
                    'topRight',
                ]
            ],
            size=20,
            wrap=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDropdown(
                    title=placement,
                    arrow=True,
                    placement=placement,
                    menuItems=[
                        {'title': 'Option1'},
                        {'title': 'Option2'},
                        {'isDivider': True},
                        {'title': 'Option3-1'},
                        {'title': 'Option3-2'},
                    ],
                )
                for placement in [
                    'bottomLeft',
                    'bottomCenter',
                    'bottomRight',
                    'topLeft',
                    'topCenter',
                    'topRight',
                ]
            ],
            size=20,
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
        fac.AntdDropdown(
            title=placement,
            arrow=True,
            placement=placement,
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        )
        for placement in [
            'bottomLeft',
            'bottomCenter',
            'bottomRight',
            'topLeft',
            'topCenter',
            'topRight',
        ]
    ],
    size=20,
    wrap=True,
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
        fac.AntdDropdown(
            title=placement,
            arrow=True,
            placement=placement,
            menuItems=[
                {'title': 'Option1'},
                {'title': 'Option2'},
                {'isDivider': True},
                {'title': 'Option3-1'},
                {'title': 'Option3-2'},
            ],
        )
        for placement in [
            'bottomLeft',
            'bottomCenter',
            'bottomRight',
            'topLeft',
            'topCenter',
            'topRight',
        ]
    ],
    size=20,
    wrap=True,
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/dropdown_selectable.py`
```python
import json
import dash
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
            fac.AntdSpace(
                [
                    fac.AntdSpace(
                        [
                            fac.AntdText('是否开启选择结果排除指定菜单项：'),
                            fac.AntdSwitch(
                                id='dropdown-demo-selectable-switch',
                                checked=False,
                            ),
                        ]
                    ),
                    fac.AntdSpace(
                        [
                            fac.AntdDropdown(
                                id='dropdown-demo-selectable-single',
                                title='单选',
                                menuItems=[
                                    {
                                        'title': '单选子页面1',
                                        'key': '单选子页面1',
                                    },
                                    {
                                        'title': '单选子页面2',
                                        'key': '单选子页面2',
                                    },
                                    {'isDivider': True},
                                    {
                                        'title': '单选子页面3-1',
                                        'key': '单选子页面3-1',
                                    },
                                    {
                                        'title': '单选子页面3-2',
                                        'key': '单选子页面3-2',
                                    },
                                ],
                                selectable=True,
                            ),
                            fac.AntdDropdown(
                                id='dropdown-demo-selectable-multiple',
                                title='多选',
                                menuItems=[
                                    {
                                        'title': '多选子页面1',
                                        'key': '多选子页面1',
                                    },
                                    {
                                        'title': '多选子页面2',
                                        'key': '多选子页面2',
                                    },
                                    {'isDivider': True},
                                    {
                                        'title': '多选子页面3-1',
                                        'key': '多选子页面3-1',
                                    },
                                    {
                                        'title': '多选子页面3-2',
                                        'key': '多选子页面3-2',
                                    },
                                ],
                                selectable=True,
                                multiple=True,
                            ),
                        ],
                        size=20,
                    ),
                ],
                direction='vertical',
            ),
            html.Div(id='dropdown-demo-selectable-output'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdSpace(
                [
                    fac.AntdSpace(
                        [
                            fac.AntdText(
                                'Whether to exclude the specified menu item when selecting results:'
                            ),
                            fac.AntdSwitch(
                                id='dropdown-demo-selectable-switch',
                                checked=False,
                            ),
                        ]
                    ),
                    fac.AntdSpace(
                        [
                            fac.AntdDropdown(
                                id='dropdown-demo-selectable-single',
                                title='Single',
                                menuItems=[
                                    {
                                        'title': 'Single page 1',
                                        'key': 'Single page 1',
                                    },
                                    {
                                        'title': 'Single page 2',
                                        'key': 'Single page 2',
                                    },
                                    {'isDivider': True},
                                    {
                                        'title': 'Single page 3-1',
                                        'key': 'Single page 3-1',
                                    },
                                    {
                                        'title': 'Single page 3-2',
                                        'key': 'Single page 3-2',
                                    },
                                ],
                                selectable=True,
                            ),
                            fac.AntdDropdown(
                                id='dropdown-demo-selectable-multiple',
                                title='Multiple',
                                menuItems=[
                                    {
                                        'title': 'Multiple page 1',
                                        'key': 'Multiple page 1',
                                    },
                                    {
                                        'title': 'Multiple page 2',
                                        'key': 'Multiple page 2',
                                    },
                                    {'isDivider': True},
                                    {
                                        'title': 'Multiple page 3-1',
                                        'key': 'Multiple page 3-1',
                                    },
                                    {
                                        'title': 'Multiple page 3-2',
                                        'key': 'Multiple page 3-2',
                                    },
                                ],
                                selectable=True,
                                multiple=True,
                            ),
                        ],
                        size=20,
                    ),
                ],
                direction='vertical',
            ),
            html.Div(id='dropdown-demo-selectable-output'),
        ]

    return demo_contents


@app.callback(
    [
        Output('dropdown-demo-selectable-single', 'nonSelectableKeys'),
        Output('dropdown-demo-selectable-multiple', 'nonSelectableKeys'),
    ],
    Input('dropdown-demo-selectable-switch', 'checked'),
)
def swtich_select_mode(checked):
    if checked:
        current_locale = get_current_locale()
        if current_locale == 'zh-cn':
            return [['单选子页面1'], ['多选子页面1']]
        elif current_locale == 'en-us':
            return [['Single page 1'], ['Multiple page 1']]
    return [[], []]


@app.callback(
    Output('dropdown-demo-selectable-output', 'children'),
    [
        Input('dropdown-demo-selectable-single', 'selectedKeys'),
        Input('dropdown-demo-selectable-multiple', 'selectedKeys'),
    ],
    prevent_initial_call=True,
)
def selectable_demo(single_selectedKeys, multiple_selectedKeys):
    trigger_id = dash.ctx.triggered_id
    if trigger_id == 'dropdown-demo-selectable-single':
        return json.dumps(
            dict(selectedKeys=single_selectedKeys), indent=4, ensure_ascii=False
        )
    elif trigger_id == 'dropdown-demo-selectable-multiple':
        return json.dumps(
            dict(selectedKeys=multiple_selectedKeys),
            indent=4,
            ensure_ascii=False,
        )
    return dash.no_update


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
            fac.AntdSpace(
                [
                    fac.AntdText('是否开启选择结果排除指定菜单项：'),
                    fac.AntdSwitch(
                        id='dropdown-demo-selectable-switch',
                        checked=False,
                    ),
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdDropdown(
                        id='dropdown-demo-selectable-single',
                        title='单选',
                        menuItems=[
                            {
                                'title': '单选子页面1',
                                'key': '单选子页面1',
                            },
                            {
                                'title': '单选子页面2',
                                'key': '单选子页面2',
                            },
                            {'isDivider': True},
                            {
                                'title': '单选子页面3-1',
                                'key': '单选子页面3-1',
                            },
                            {
                                'title': '单选子页面3-2',
                                'key': '单选子页面3-2',
                            },
                        ],
                        selectable=True,
                    ),
                    fac.AntdDropdown(
                        id='dropdown-demo-selectable-multiple',
                        title='多选',
                        menuItems=[
                            {
                                'title': '多选子页面1',
                                'key': '多选子页面1',
                            },
                            {
                                'title': '多选子页面2',
                                'key': '多选子页面2',
                            },
                            {'isDivider': True},
                            {
                                'title': '多选子页面3-1',
                                'key': '多选子页面3-1',
                            },
                            {
                                'title': '多选子页面3-2',
                                'key': '多选子页面3-2',
                            },
                        ],
                        selectable=True,
                        multiple=True,
                    ),
                ],
                size=20,
            ),
        ],
        direction='vertical',
    ),
    html.Div(id='dropdown-demo-selectable-output'),
]

...

@app.callback(
    [
        Output('dropdown-demo-selectable-single', 'nonSelectableKeys'),
        Output('dropdown-demo-selectable-multiple', 'nonSelectableKeys'),
    ],
    Input('dropdown-demo-selectable-switch', 'checked'),
)
def swtich_select_mode(checked):
    if checked:
        return [['单选子页面1'], ['多选子页面1']]
    return [[], []]


@app.callback(
    Output('dropdown-demo-selectable-output', 'children'),
    [
        Input('dropdown-demo-selectable-single', 'selectedKeys'),
        Input('dropdown-demo-selectable-multiple', 'selectedKeys'),
    ],
    prevent_initial_call=True,
)
def selectable_demo(single_selectedKeys, multiple_selectedKeys):
    trigger_id = dash.ctx.triggered_id
    if trigger_id == 'dropdown-demo-selectable-single':
        return json.dumps(
            dict(selectedKeys=single_selectedKeys), indent=4, ensure_ascii=False
        )
    elif trigger_id == 'dropdown-demo-selectable-multiple':
        return json.dumps(
            dict(selectedKeys=multiple_selectedKeys),
            indent=4,
            ensure_ascii=False,
        )
    return dash.no_update
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
            fac.AntdSpace(
                [
                    fac.AntdText(
                        'Whether to exclude the specified menu item when selecting results:'
                    ),
                    fac.AntdSwitch(
                        id='dropdown-demo-selectable-switch',
                        checked=False,
                    ),
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdDropdown(
                        id='dropdown-demo-selectable-single',
                        title='Single',
                        menuItems=[
                            {
                                'title': 'Single page 1',
                                'key': 'Single page 1',
                            },
                            {
                                'title': 'Single page 2',
                                'key': 'Single page 2',
                            },
                            {'isDivider': True},
                            {
                                'title': 'Single page 3-1',
                                'key': 'Single page 3-1',
                            },
                            {
                                'title': 'Single page 3-2',
                                'key': 'Single page 3-2',
                            },
                        ],
                        selectable=True,
                    ),
                    fac.AntdDropdown(
                        id='dropdown-demo-selectable-multiple',
                        title='Multiple',
                        menuItems=[
                            {
                                'title': 'Multiple page 1',
                                'key': 'Multiple page 1',
                            },
                            {
                                'title': 'Multiple page 2',
                                'key': 'Multiple page 2',
                            },
                            {'isDivider': True},
                            {
                                'title': 'Multiple page 3-1',
                                'key': 'Multiple page 3-1',
                            },
                            {
                                'title': 'Multiple page 3-2',
                                'key': 'Multiple page 3-2',
                            },
                        ],
                        selectable=True,
                        multiple=True,
                    ),
                ],
                size=20,
            ),
        ],
        direction='vertical',
    ),
    html.Div(id='dropdown-demo-selectable-output'),
]

...

@app.callback(
    [
        Output('dropdown-demo-selectable-single', 'nonSelectableKeys'),
        Output('dropdown-demo-selectable-multiple', 'nonSelectableKeys'),
    ],
    Input('dropdown-demo-selectable-switch', 'checked'),
)
def swtich_select_mode(checked):
    if checked:
        return [['Single page 1'], ['Multiple page 1']]
    return [[], []]


@app.callback(
    Output('dropdown-demo-selectable-output', 'children'),
    [
        Input('dropdown-demo-selectable-single', 'selectedKeys'),
        Input('dropdown-demo-selectable-multiple', 'selectedKeys'),
    ],
    prevent_initial_call=True,
)
def selectable_demo(single_selectedKeys, multiple_selectedKeys):
    trigger_id = dash.ctx.triggered_id
    if trigger_id == 'dropdown-demo-selectable-single':
        return json.dumps(
            dict(selectedKeys=single_selectedKeys), indent=4, ensure_ascii=False
        )
    elif trigger_id == 'dropdown-demo-selectable-multiple':
        return json.dumps(
            dict(selectedKeys=multiple_selectedKeys),
            indent=4,
            ensure_ascii=False,
        )
    return dash.no_update
"""
            }
        ]

```

### `views/AntdDropdown/demos/dropdown_trigger.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            trigger='click',
            menuItems=[
                {'title': '子页面1'},
                {'title': '子页面2'},
                {'isDivider': True},
                {'title': '子页面3-1'},
                {'title': '子页面3-2'},
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            trigger='click',
            menuItems=[
                {'title': 'Option1'},
                {'title': 'Option2'},
                {'isDivider': True},
                {'title': 'Option3-1'},
                {'title': 'Option3-2'},
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    trigger='click',
    menuItems=[
        {'title': '子页面1'},
        {'title': '子页面2'},
        {'isDivider': True},
        {'title': '子页面3-1'},
        {'title': '子页面3-2'},
    ],
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    trigger='click',
    menuItems=[
        {'title': 'Option1'},
        {'title': 'Option2'},
        {'isDivider': True},
        {'title': 'Option3-1'},
        {'title': 'Option3-2'},
    ],
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/extra.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdDropdown(
            title='触发点',
            menuItems=[
                {'title': '选项1', 'extra': '1'},
                {'title': '选项2', 'extra': '2'},
                {'isDivider': True},
                {'title': '选项3-1', 'extra': '3-1'},
                {'title': '选项3-2', 'extra': '3-2'},
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdDropdown(
            title='Trigger point',
            menuItems=[
                {'title': 'Option1', 'extra': '1'},
                {'title': 'Option2', 'extra': '2'},
                {'isDivider': True},
                {'title': 'Option3-1', 'extra': '3-1'},
                {'title': 'Option3-2', 'extra': '3-2'},
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='触发点',
    menuItems=[
        {'title': '选项1', 'extra': '1'},
        {'title': '选项2', 'extra': '2'},
        {'isDivider': True},
        {'title': '选项3-1', 'extra': '3-1'},
        {'title': '选项3-2', 'extra': '3-2'},
    ],
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdDropdown(
    title='Trigger point',
    menuItems=[
        {'title': 'Option1', 'extra': '1'},
        {'title': 'Option2', 'extra': '2'},
        {'isDivider': True},
        {'title': 'Option3-1', 'extra': '3-1'},
        {'title': 'Option3-2', 'extra': '3-2'},
    ],
)
"""
            }
        ]

```

### `views/AntdDropdown/demos/free_position_mode.py`
```python
import uuid
from dash import html
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component, Input, Output

from server import app

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = [
            fuc.FefferyDiv(
                '请在此区域内任意位置点击鼠标右键',
                id='dropdown-free-position-demo-trigger',
                enableListenContextMenu=True,
                style={
                    'borderRadius': 6,
                    'background': '#adb5bd',
                    'height': 400,
                    'color': 'white',
                    'display': 'flex',
                    'justifyContent': 'center',
                    'alignItems': 'center',
                },
            ),
            html.Div(id='dropdown-free-position-demo-container'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fuc.FefferyDiv(
                'Please click the mouse right button anywhere in this area',
                id='dropdown-free-position-demo-trigger',
                enableListenContextMenu=True,
                style={
                    'borderRadius': 6,
                    'background': '#adb5bd',
                    'height': 400,
                    'color': 'white',
                    'display': 'flex',
                    'justifyContent': 'center',
                    'alignItems': 'center',
                },
            ),
            html.Div(id='dropdown-free-position-demo-container'),
        ]

    return demo_contents


@app.callback(
    Output('dropdown-free-position-demo-container', 'children'),
    Input('dropdown-free-position-demo-trigger', 'contextMenuEvent'),
    prevent_initial_call=True,
)
def dropdown_free_position_demo(contextMenuEvent):
    if contextMenuEvent:
        current_locale = get_current_locale()

        if current_locale == 'zh-cn':
            return fac.AntdDropdown(
                key=str(uuid.uuid4()),
                visible=True,
                freePosition=True,
                freePositionStyle={
                    'left': contextMenuEvent['clientX'],
                    'top': contextMenuEvent['clientY'],
                },
                menuItems=[
                    {'title': f'右键菜单选项{i}', 'key': f'右键菜单选项{i}'}
                    for i in range(1, 6)
                ],
                trigger='click',
            )

        elif current_locale == 'en-us':
            return fac.AntdDropdown(
                key=str(uuid.uuid4()),
                visible=True,
                freePosition=True,
                freePositionStyle={
                    'left': contextMenuEvent['clientX'],
                    'top': contextMenuEvent['clientY'],
                },
                menuItems=[
                    {
                        'title': f'Right click menu item{i}',
                        'key': f'Right click menu item{i}',
                    }
                    for i in range(1, 6)
                ],
                trigger='click',
            )


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fuc.FefferyDiv(
        '请在此区域内任意位置点击鼠标右键',
        id='dropdown-free-position-demo-trigger',
        enableListenContextMenu=True,
        style={
            'borderRadius': 6,
            'background': '#adb5bd',
            'height': 400,
            'color': 'white',
            'display': 'flex',
            'justifyContent': 'center',
            'alignItems': 'center',
        },
    ),
    html.Div(id='dropdown-free-position-demo-container'),
]

...

@app.callback(
    Output('dropdown-free-position-demo-container', 'children'),
    Input('dropdown-free-position-demo-trigger', 'contextMenuEvent'),
    prevent_initial_call=True,
)
def dropdown_free_position_demo(contextMenuEvent):
    if contextMenuEvent:
        return fac.AntdDropdown(
            key=str(uuid.uuid4()),
            visible=True,
            freePosition=True,
            freePositionStyle={
                'left': contextMenuEvent['clientX'],
                'top': contextMenuEvent['clientY'],
            },
            menuItems=[
                {'title': f'右键菜单选项{i}', 'key': f'右键菜单选项{i}'}
                for i in range(1, 6)
            ],
            trigger='click',
        )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fuc.FefferyDiv(
        'Please click the mouse right button anywhere in this area',
        id='dropdown-free-position-demo-trigger',
        enableListenContextMenu=True,
        style={
            'borderRadius': 6,
            'background': '#adb5bd',
            'height': 400,
            'color': 'white',
            'display': 'flex',
            'justifyContent': 'center',
            'alignItems': 'center',
        },
    ),
    html.Div(id='dropdown-free-position-demo-container'),
]

...

@app.callback(
    Output('dropdown-free-position-demo-container', 'children'),
    Input('dropdown-free-position-demo-trigger', 'contextMenuEvent'),
    prevent_initial_call=True,
)
def dropdown_free_position_demo(contextMenuEvent):
    if contextMenuEvent:
        return fac.AntdDropdown(
            key=str(uuid.uuid4()),
            visible=True,
            freePosition=True,
            freePositionStyle={
                'left': contextMenuEvent['clientX'],
                'top': contextMenuEvent['clientY'],
            },
            menuItems=[
                {
                    'title': f'Right click menu item{i}',
                    'key': f'Right click menu item{i}',
                }
                for i in range(1, 6)
            ],
            trigger='click',
        )
"""
            }
        ]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, dropdown menu trigger anchor element.

- id (string; optional):
    Unique ID for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- arrow (boolean; default False):
    Whether the dropdown menu renders an arrow. Default value: `False`.

- autoAdjustOverflow (boolean; default True):
    Whether the dropdown menu automatically adjusts its position when it is obscured. Default value: `True`.

- batchPropsNames (list of strings; optional):
    Attribute names to be included in batch property listening. Default value: `[]`.

- batchPropsValues (dict; optional):
    Batch listening to attribute values corresponding to the current batchPropsNames.

- buttonMode (boolean; default False):
    Whether the dropdown menu trigger element is rendered as a button, effective when the children parameter is not set. Default value: `False`.

- buttonProps (dict; optional):
    Further configuration for the button form of the dropdown menu trigger element.

    `buttonProps` is a dict with keys:

    - className (string; optional):
        Button CSS class name.

    - danger (boolean; optional):
        Whether the button displays a danger style. Default value: `False`.

    - size (a value equal to: 'small', 'middle', 'large'; optional):
        Button size specification, options include `'small'`, `'middle'`, `'large'`. Default value: `'middle'`.

    - style (dict; optional):
        Button CSS style.

    - type (a value equal to: 'default', 'primary', 'ghost', 'dashed', 'link', 'text'; optional):
        Button type, options include `'default'`, `'primary'`, `'ghost'`, `'dashed'`, `'link'`, `'text'`.
        Default value: `'default'`.

- className (string | dict; optional):
    The current component's CSS class name, supports [dynamic CSS](/advanced-classname).

- clickedKey (string; optional):
    Listening to the key value of the clicked dropdown menu option.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- disabled (boolean; default False):
    Whether to disable the component's functionality. Default value: `False`.

- freePosition (boolean; default False):
    Whether to enable free position mode. Default value: `False`.

- freePositionClassName (string; optional):
    CSS class name for the anchor position when free position mode is enabled.

- freePositionStyle (dict; optional):
    CSS style for the anchor position when free position mode is enabled.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the current component.

- loading_state (dict; optional):

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- menuItems (list of dicts; optional):
    The data structure of the dropdown menu.

    `menuItems` is a list of dicts with keys:

    - disabled (boolean; optional):
        Whether the node is disabled. Default value: `False`.

    - href (string; optional):
        Node link address.

    - icon (string; optional):
        Node prefix icon name, associated with `iconRenderer` method, same as AntdIcon's icon parameter under `'AntdIcon'` method, represents the icon's CSS class name under `'fontawesome'` method.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
        The rendering method of the prefix icon, options include `'AntdIcon'`, `'fontawesome'`. Default value: `'AntdIcon'`.

    - isDivider (boolean; optional):
        Whether the node is rendered as a divider.

    - key (string; optional):
        Unique key value of the node.

    - target (string; optional):
        Node link jump behavior.

    - title (a list of or a singular dash component, string or number; optional):
        Component type, node title.

- multiple (boolean; default False):
    Whether menu items can be selected multiple times. Default value: `False`.

- nClicks (number; default 0):
    Listening to the cumulative number of times the dropdown menu option has been clicked. Default value: `0`.

- nonSelectableKeys (list of strings; optional):
    Setting an array of key values for non-selectable items. Default value: `[]`.

- overlayClassName (string | dict; optional):
    The CSS class name of the dropdown menu container, supports [dynamic CSS](/advanced-classname).

- overlayStyle (dict; optional):
    The CSS style of the dropdown menu container.

- placement (a value equal to: 'bottomLeft', 'bottomCenter', 'bottomRight', 'topLeft', 'topCenter', 'topRight'; optional):
    The direction in which the dropdown menu pops up, options include `'bottomLeft'`, `'bottomCenter'`, `'bottomRight'`, `'topLeft'`, `'topCenter'`, `'topRight'`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    The anchor strategy for the dropdown menu's expansion layer, options include `'parent'`, `'body'`. Default value: `'body'`.

- selectable (boolean; default False):
    Whether menu items can be selected. Default value: `False`.

- selectedKeys (list of strings; optional):
    Set or listen to the key values of the currently selected menu items.

- style (dict; optional):
    The current component's CSS style.

- title (string; optional):
    The title content of the dropdown menu trigger element, effective when the children parameter is not set.

- trigger (a value equal to: 'click', 'hover'; default 'hover'):
    The trigger method for displaying the dropdown menu, options include `'click'`, `'hover'`. Default value: `'hover'`.

- visible (boolean; default False):
    Listening to or setting whether the dropdown menu is expanded. Default value: `False`.

- wrapperClassName (string | dict; optional):
    The CSS class name of the anchor element's parent container.

- wrapperStyle (dict; optional):
    The CSS style of the anchor element's parent container.
