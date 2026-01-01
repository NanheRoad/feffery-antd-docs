# AntdTitle

## 简介源码：`views/AntdTitle/intro.py`
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
                {'title': translator.t('AntdTitle 标题')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTitle 标题'), level=2),
        fac.AntdParagraph(translator.t('用于渲染具有丰富样式和功能的标题。')),
    ]

```

## 示例源码（demos）

### `views/AntdTitle/demos/different_title_level.py`
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
                fac.AntdTitle('一级标题', level=1),
                fac.AntdTitle('二级标题', level=2),
                fac.AntdTitle('三级标题', level=3),
                fac.AntdTitle('四级标题', level=4),
                fac.AntdTitle('五级标题', level=5),
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdParagraph(
            [
                fac.AntdTitle('Level1 Title', level=1),
                fac.AntdTitle('Level2 Title', level=2),
                fac.AntdTitle('Level3 Title', level=3),
                fac.AntdTitle('Level4 Title', level=4),
                fac.AntdTitle('Level5 Title', level=5),
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
        fac.AntdTitle('一级标题', level=1),
        fac.AntdTitle('二级标题', level=2),
        fac.AntdTitle('三级标题', level=3),
        fac.AntdTitle('四级标题', level=4),
        fac.AntdTitle('五级标题', level=5)
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
        fac.AntdTitle('Level1 Title', level=1),
        fac.AntdTitle('Level2 Title', level=2),
        fac.AntdTitle('Level3 Title', level=3),
        fac.AntdTitle('Level4 Title', level=4),
        fac.AntdTitle('Level5 Title', level=5),
    ]
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

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- code (boolean; optional):
    Whether to render in code format.

- copyable (boolean; optional):
    Whether to enable the quick copy feature.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- disabled (boolean; optional):
    Whether to render in a disabled state.

- italic (boolean; optional):
    Whether to render in italic format.

- key (string; optional):
    Update the `key` value for the current component, which can force a redraw of the current component.

- keyboard (boolean; optional):
    Whether to render in keyboard format.

- level (number; default 1):
    Heading level, options include `1`, `2`, `3`, `4`, `5`. Default value: `1`.

- loading_state (dict; optional):
    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    Component text language, options include `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German).
    Default value: `'zh-cn'`.

- mark (boolean; optional):
    Whether to render in highlighted format.

- strikethrough (boolean; optional):
    Whether to render in strikethrough format.

- strong (boolean; optional):
    Whether to render in bold format.

- style (dict; optional):
    CSS styles for the current component.

- type (a value equal to: 'secondary', 'success', 'warning', 'danger'; optional):
    Set special state format for content, options include `'secondary'`, `'success'`, `'warning'`, `'danger'`.

- underline (boolean; optional):
    Whether to render in underline format.
