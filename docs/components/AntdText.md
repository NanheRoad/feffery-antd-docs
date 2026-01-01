# AntdText

## 简介源码：`views/AntdText/intro.py`
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
                {'title': translator.t('排版相关')},
                {'title': translator.t('AntdText 文字')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdText 文字', level=2),
        fac.AntdParagraph(
            translator.t('用于渲染具有丰富样式和功能的行内文字。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdText/demos/content_ellipsis.py`
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
                fac.AntdText(
                    '内容省略示例' + '巴拉巴拉巴拉巴拉' * 100, ellipsis=True
                ),
                fac.AntdText(
                    '内容省略示例' + '巴拉巴拉巴拉巴拉' * 100,
                    ellipsis={'suffix': '👉'},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdText(
                    'Content ellipsis example ' + 'bala' * 100,
                    ellipsis=True,
                ),
                fac.AntdText(
                    'Content ellipsis example ' + 'bala' * 100,
                    ellipsis={'suffix': '👉'},
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
        fac.AntdText(
            '内容省略示例' + '巴拉巴拉巴拉巴拉' * 100, ellipsis=True
        ),
        fac.AntdText(
            '内容省略示例' + '巴拉巴拉巴拉巴拉' * 100,
            ellipsis={'suffix': '👉'},
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
        fac.AntdText(
            'Content ellipsis example ' + 'bala' * 100,
            ellipsis=True,
        ),
        fac.AntdText(
            'Content ellipsis example ' + 'bala' * 100,
            ellipsis={'suffix': '👉'},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdText/demos/different_render_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdParagraph(
            [
                fac.AntdText('code示例', code=True),
                fac.AntdText('copyable示例', copyable=True),
                fac.AntdText('strikethrough示例', strikethrough=True),
                fac.AntdText('disabled示例', disabled=True),
                fac.AntdText('mark示例', mark=True),
                fac.AntdText('strong示例', strong=True),
                fac.AntdText('underline示例', underline=True),
                fac.AntdText('keyboard示例', keyboard=True),
                fac.AntdText('secondary示例', type='secondary'),
                fac.AntdText('success示例', type='success'),
                fac.AntdText('warning示例', type='warning'),
                fac.AntdText('danger示例', type='danger'),
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdParagraph(
            [
                fac.AntdText('code', code=True),
                fac.AntdText('copyable', copyable=True),
                fac.AntdText('strikethrough', strikethrough=True),
                fac.AntdText('disabled', disabled=True),
                fac.AntdText('mark', mark=True),
                fac.AntdText('strong', strong=True),
                fac.AntdText('underline', underline=True),
                fac.AntdText('keyboard', keyboard=True),
                fac.AntdText('secondary', type='secondary'),
                fac.AntdText('success', type='success'),
                fac.AntdText('warning', type='warning'),
                fac.AntdText('danger', type='danger'),
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
fac.AntdParagraph(
    [
        fac.AntdText('code示例', code=True),
        fac.AntdText('copyable示例', copyable=True),
        fac.AntdText('strikethrough示例', strikethrough=True),
        fac.AntdText('disabled示例', disabled=True),
        fac.AntdText('mark示例', mark=True),
        fac.AntdText('strong示例', strong=True),
        fac.AntdText('underline示例', underline=True),
        fac.AntdText('keyboard示例', keyboard=True),
        fac.AntdText('secondary示例', type='secondary'),
        fac.AntdText('success示例', type='success'),
        fac.AntdText('warning示例', type='warning'),
        fac.AntdText('danger示例', type='danger'),
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdParagraph(
    [
        fac.AntdText('code', code=True),
        fac.AntdText('copyable', copyable=True),
        fac.AntdText('strikethrough', strikethrough=True),
        fac.AntdText('disabled', disabled=True),
        fac.AntdText('mark', mark=True),
        fac.AntdText('strong', strong=True),
        fac.AntdText('underline', underline=True),
        fac.AntdText('keyboard', keyboard=True),
        fac.AntdText('secondary', type='secondary'),
        fac.AntdText('success', type='success'),
        fac.AntdText('warning', type='warning'),
        fac.AntdText('danger', type='danger'),
    ]
)
"""
            }
        ]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, for nested elements.

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- className (string | dict; optional):
    Current component's CSS class name, supports [dynamic CSS](/advanced-classname).

- code (boolean; optional):
    Whether to render in code format.

- copyable (boolean; optional):
    Whether to enable the quick copy feature.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- disabled (boolean; optional):
    Whether to render in a disabled state.

- ellipsis (dict; default False):
    Configuration for content truncation features, set to `False` to disable. Default value: `False`.

    `ellipsis` can be a boolean or a dict with keys:

    - suffix (string; optional):
        Custom suffix for content after truncation.

- italic (boolean; optional):
    Whether to render in italic format.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- keyboard (boolean; optional):
    Whether to render in keyboard format.

- loading_state (dict; optional):
    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is in a loading state.

    - prop_name (string; optional):
        Holds which property is currently loading.

- locale (a value equal to: 'zh-cn', 'en-us'; default 'zh-cn'):
    Component's text language, options include `'zh-cn'`, `'en-us'`. Default value: `'zh-cn'`.

- mark (boolean; optional):
    Whether to render in highlighted format.

- strikethrough (boolean; optional):
    Whether to render with a strikethrough.

- strong (boolean; optional):
    Whether to render in bold format.

- style (dict; optional):
    CSS styles for the current component.

- type (a value equal to: 'secondary', 'success', 'warning', 'danger'; optional):
    Set the special state of the content, options include `'secondary'`, `'success'`, `'warning'`, `'danger'`.

- underline (boolean; optional):
    Whether to render with an underline.
