# AntdPageHeader

## 简介源码：`views/AntdPageHeader/intro.py`
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
                {'title': translator.t('AntdPageHeader 页头')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdPageHeader 页头'), level=2),
        fac.AntdParagraph(
            translator.t(
                '页头位于页容器顶部，起到内容概览和引导页级操作的作用。'
            )
        ),
    ]

```

## 示例源码（demos）

### `views/AntdPageHeader/demos/basic_callbacks.py`
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
        demo_contents = fac.AntdPageHeader(
            id='page-header-demo',
            title='页头标题示例',
            subTitle='页头副标题示例',
            historyBackDisabled=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPageHeader(
            id='page-header-demo',
            title='Page Header',
            subTitle='Page Header Subtitle',
            historyBackDisabled=True,
        )

    return demo_contents


@app.callback(
    Output('page-header-demo', 'children'),
    Input('page-header-demo', 'backClicks'),
)
def page_header_demo_callback(backClicks):
    return [fac.AntdText('backClicks: ', strong=True), fac.AntdText(backClicks)]


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPageHeader(
    id='page-header-demo',
    title='页头标题示例',
    subTitle='页头副标题示例',
    historyBackDisabled=True
)

...

@app.callback(
    Output('page-header-demo', 'children'),
    Input('page-header-demo', 'backClicks')
)
def page_header_demo_callback(backClicks):
    return [
        fac.AntdText('backClicks: ', strong=True),
        fac.AntdText(backClicks)
    ]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPageHeader(
    id='page-header-demo',
    title='Page Header',
    subTitle='Page Header Subtitle',
    historyBackDisabled=True,
)

...

@app.callback(
    Output('page-header-demo', 'children'),
    Input('page-header-demo', 'backClicks')
)
def page_header_demo_callback(backClicks):
    return [
        fac.AntdText('backClicks: ', strong=True),
        fac.AntdText(backClicks)
    ]
"""
            }
        ]

```

### `views/AntdPageHeader/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPageHeader(
            title='页头标题示例', subTitle='页头副标题示例'
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPageHeader(
            title='Page Header', subTitle='Page Header Subtitle'
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPageHeader(
    title='页头标题示例', subTitle='页头副标题示例'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPageHeader(
    title='Page Header', subTitle='Page Header Subtitle'
)
"""
            }
        ]

```

### `views/AntdPageHeader/demos/custom_children.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPageHeader(
            fac.AntdSpace(
                [
                    fac.AntdButton('按钮1'),
                    fac.AntdButton('按钮2', type='primary'),
                    fac.AntdSwitch(
                        checkedChildren='打开', unCheckedChildren='关闭'
                    ),
                    fac.AntdBadge(status='processing'),
                ]
            ),
            title='页头标题示例',
            subTitle='页头副标题示例',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPageHeader(
            fac.AntdSpace(
                [
                    fac.AntdButton('Button1'),
                    fac.AntdButton('Button2', type='primary'),
                    fac.AntdSwitch(
                        checkedChildren='Open', unCheckedChildren='Close'
                    ),
                    fac.AntdBadge(status='processing'),
                ]
            ),
            title='Page Header Example',
            subTitle='Page Header Subtitle',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPageHeader(
    fac.AntdSpace(
        [
            fac.AntdButton('按钮1'),
            fac.AntdButton('按钮2', type='primary'),
            fac.AntdSwitch(
                checkedChildren='打开',
                unCheckedChildren='关闭'
            ),
            fac.AntdBadge(status='processing')
        ]
    ),
    title='页头标题示例',
    subTitle='页头副标题示例'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPageHeader(
    fac.AntdSpace(
        [
            fac.AntdButton('Button1'),
            fac.AntdButton('Button2', type='primary'),
            fac.AntdSwitch(
                checkedChildren='Open', unCheckedChildren='Close'
            ),
            fac.AntdBadge(status='processing'),
        ]
    ),
    title='Page Header Example',
    subTitle='Page Header Subtitle',
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
    Wildcard for attributes in the `aria-*` format.

- backClicks (number; default 0):
    Number of times the back button has been clicked, used to monitor the behavior of back button clicks. Default value: `0`.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- ghost (boolean; default False):
    Whether to enable the transparent background mode. Default value: `False`.

- historyBackDisabled (boolean; default False):
    Whether to disable the function of going back to the previous address by clicking the back button. Default value: `False`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the current component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- showBackIcon (boolean; default True):
    Whether to render the back button. Default value: `True`.

- style (dict; optional):
    The CSS style for the current component.

- subTitle (a list of or a singular dash component, string or number; optional):
    Component type, content for the page header subtitle.

- title (a list of or a singular dash component, string or number; optional):
    Component type, content for the page header title.
