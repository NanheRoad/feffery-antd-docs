# AntdCenter

## 简介源码：`views/AntdCenter/intro.py`
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
                {'title': translator.t('AntdCenter 居中')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCenter 居中'), level=2),
        fac.AntdParagraph(translator.t('快捷实现内容在水平垂直方向上居中。')),
    ]

```

## 示例源码（demos）

### `views/AntdCenter/demos/auto_style_with_config_provider.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdConfigProvider(
        [
            fac.AntdCenter(
                'demo1', inheritStyleToken=True, style={'height': 200}
            ),
            fac.AntdCenter(
                'demo2',
                inheritStyleToken=True,
                style={'height': 200, 'fontSize': 24, 'color': '#ffffb8'},
            ),
        ],
        algorithm='dark',
        token={'colorTextBase': '#d3adf7', 'fontSize': 56},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdConfigProvider(
    [
        fac.AntdCenter(
            'demo1', inheritStyleToken=True, style={'height': 200}
        ),
        fac.AntdCenter(
            'demo2',
            inheritStyleToken=True,
            style={'height': 200, 'fontSize': 24, 'color': '#ffffb8'},
        ),
    ],
    algorithm='dark',
    token={'colorTextBase': '#d3adf7', 'fontSize': 56},
)
"""
    }
]

```

### `views/AntdCenter/demos/basic_usage.py`
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
                fac.AntdCenter(
                    '常规居中',
                    style={
                        'width': 300,
                        'height': 150,
                        'background': '#f0f0f0',
                    },
                ),
                fac.AntdParagraph(
                    [
                        '测试内容',
                        fac.AntdCenter(
                            '行内居中',
                            style={
                                'width': 100,
                                'height': 100,
                                'background': '#f0f0f0',
                            },
                            inline=True,
                        ),
                        '测试内容',
                    ]
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdCenter(
                    'Regular center',
                    style={
                        'width': 300,
                        'height': 150,
                        'background': '#f0f0f0',
                    },
                ),
                fac.AntdParagraph(
                    [
                        'Test content',
                        fac.AntdCenter(
                            'Inline center',
                            style={
                                'width': 100,
                                'height': 100,
                                'background': '#f0f0f0',
                            },
                            inline=True,
                        ),
                        'Test content',
                    ]
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
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
        fac.AntdCenter(
            '常规居中',
            style={'width': 300, 'height': 150, 'background': '#f0f0f0'},
        ),
        fac.AntdParagraph(
            [
                '测试内容',
                fac.AntdCenter(
                    '行内居中',
                    style={
                        'width': 100,
                        'height': 100,
                        'background': '#f0f0f0',
                    },
                    inline=True,
                ),
                '测试内容',
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
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
        fac.AntdCenter(
            'Regular center',
            style={
                'width': 300,
                'height': 150,
                'background': '#f0f0f0',
            },
        ),
        fac.AntdParagraph(
            [
                'Test content',
                fac.AntdCenter(
                    'Inline center',
                    style={
                        'width': 100,
                        'height': 100,
                        'background': '#f0f0f0',
                    },
                    inline=True,
                ),
                'Test content',
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

- children (a list of or a singular dash component, string or number; optional):
    Component type, nested elements.

- id (string; optional):
    Unique ID for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- inline (boolean; default False):
    Whether to render as an inline element. Default value: `False`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- style (dict; optional):
    CSS styles for the current component.
