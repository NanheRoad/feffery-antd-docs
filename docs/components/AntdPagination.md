# AntdPagination

## 简介源码：`views/AntdPagination/intro.py`
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
                {'title': translator.t('AntdPagination 分页')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdPagination 分页'), level=2),
        fac.AntdParagraph(
            translator.t('采用分页的形式分隔长列表，每次只加载单页内容。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdPagination/demos/add_more_function.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPagination(
            defaultPageSize=10,
            total=100,
            showQuickJumper=True,
            showSizeChanger=False,
            showTotalPrefix='总记录数：',
            showTotalSuffix='条！🧐',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPagination(
            defaultPageSize=10,
            total=100,
            showQuickJumper=True,
            showSizeChanger=False,
            showTotalPrefix='Total records: ',
            showTotalSuffix=' items!🧐',
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10,
    total=100,
    showQuickJumper=True,
    showSizeChanger=False,
    showTotalPrefix='总记录数：',
    showTotalSuffix='条！🧐'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10,
    total=100,
    showQuickJumper=True,
    showSizeChanger=False,
    showTotalPrefix='Total records: ',
    showTotalSuffix=' items!🧐',
    locale='en-us',
)
"""
            }
        ]

```

### `views/AntdPagination/demos/align.py`
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
            fac.AntdDivider("align='start'"),
            fac.AntdPagination(defaultPageSize=10, total=100, align='start'),
            fac.AntdDivider("align='center'"),
            fac.AntdPagination(defaultPageSize=10, total=100, align='center'),
            fac.AntdDivider("align='end'"),
            fac.AntdPagination(defaultPageSize=10, total=100, align='end'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider("align='start'"),
            fac.AntdPagination(
                defaultPageSize=10, total=100, align='start', locale='en-us'
            ),
            fac.AntdDivider("align='center'"),
            fac.AntdPagination(
                defaultPageSize=10, total=100, align='center', locale='en-us'
            ),
            fac.AntdDivider("align='end'"),
            fac.AntdPagination(
                defaultPageSize=10, total=100, align='end', locale='en-us'
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
    fac.AntdDivider("align='start'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='start'),
    fac.AntdDivider("align='center'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='center'),
    fac.AntdDivider("align='end'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='end'),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider("align='start'"),
    fac.AntdPagination(
        defaultPageSize=10, total=100, align='start', locale='en-us'
    ),
    fac.AntdDivider("align='center'"),
    fac.AntdPagination(
        defaultPageSize=10, total=100, align='center', locale='en-us'
    ),
    fac.AntdDivider("align='end'"),
    fac.AntdPagination(
        defaultPageSize=10, total=100, align='end', locale='en-us'
    ),
]
"""
            }
        ]

```

### `views/AntdPagination/demos/auto_hide_on_single_page.py`
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
            fac.AntdDivider(
                '默认hideOnSinglePage=False', innerTextOrientation='left'
            ),
            fac.AntdPagination(total=10, pageSize=20),
            fac.AntdDivider(
                'hideOnSinglePage=True', innerTextOrientation='left'
            ),
            fac.AntdPagination(total=10, pageSize=20, hideOnSinglePage=True),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'hideOnSinglePage=False', innerTextOrientation='left'
            ),
            fac.AntdPagination(total=10, pageSize=20, locale='en-us'),
            fac.AntdDivider(
                'hideOnSinglePage=True', innerTextOrientation='left'
            ),
            fac.AntdPagination(
                total=10, pageSize=20, hideOnSinglePage=True, locale='en-us'
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
    fac.AntdDivider(
        '默认hideOnSinglePage=False', innerTextOrientation='left'
    ),
    fac.AntdPagination(total=10, pageSize=20),
    fac.AntdDivider(
        'hideOnSinglePage=True', innerTextOrientation='left'
    ),
    fac.AntdPagination(total=10, pageSize=20, hideOnSinglePage=True),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider(
        'hideOnSinglePage=False', innerTextOrientation='left'
    ),
    fac.AntdPagination(total=10, pageSize=20, locale='en-us'),
    fac.AntdDivider(
        'hideOnSinglePage=True', innerTextOrientation='left'
    ),
    fac.AntdPagination(
        total=10, pageSize=20, hideOnSinglePage=True, locale='en-us'
    ),
]
"""
            }
        ]

```

### `views/AntdPagination/demos/basic_callbacks.py`
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
        demo_contents = [
            fac.AntdSpace(id='pagination-demo-output', direction='vertical'),
            fac.AntdPagination(
                id='pagination-demo',
                defaultPageSize=10,
                total=100,
                pageSizeOptions=[5, 10, 20],
                showSizeChanger=True,
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdSpace(id='pagination-demo-output', direction='vertical'),
            fac.AntdPagination(
                id='pagination-demo',
                defaultPageSize=10,
                total=100,
                pageSizeOptions=[5, 10, 20],
                showSizeChanger=True,
                locale='en-us',
            ),
        ]

    return demo_contents


@app.callback(
    Output('pagination-demo-output', 'children'),
    [Input('pagination-demo', 'current'), Input('pagination-demo', 'pageSize')],
)
def pagination_callback_demo(current, pageSize):
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            fac.AntdText(f'内容项{i}')
            for i in range((current - 1) * pageSize, current * pageSize)
        ]

    elif current_locale == 'en-us':
        return [
            fac.AntdText(f'Item {i}')
            for i in range((current - 1) * pageSize, current * pageSize)
        ]


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdSpace(id='pagination-demo-output', direction='vertical'),
    fac.AntdPagination(
        id='pagination-demo',
        defaultPageSize=10,
        total=100,
        pageSizeOptions=[5, 10, 20],
        showSizeChanger=True,
    ),
]

...

@app.callback(
    Output('pagination-demo-output', 'children'),
    [Input('pagination-demo', 'current'),
     Input('pagination-demo', 'pageSize')]
)
def pagination_callback_demo(current, pageSize):

    return [
        fac.AntdText(f'内容项{i}')
        for i in range((current - 1) * pageSize, current * pageSize)
    ]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdSpace(id='pagination-demo-output', direction='vertical'),
    fac.AntdPagination(
        id='pagination-demo',
        defaultPageSize=10,
        total=100,
        pageSizeOptions=[5, 10, 20],
        showSizeChanger=True,
        locale='en-us',
    ),
]

...

@app.callback(
    Output('pagination-demo-output', 'children'),
    [Input('pagination-demo', 'current'),
     Input('pagination-demo', 'pageSize')]
)
def pagination_callback_demo(current, pageSize):

    return [
        fac.AntdText(f'Item {i}')
        for i in range((current - 1) * pageSize, current * pageSize)
    ]
"""
            }
        ]

```

### `views/AntdPagination/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPagination(defaultPageSize=10, total=100)

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPagination(
            defaultPageSize=10, total=100, locale='en-us'
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPagination(defaultPageSize=10, total=100)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10, total=100, locale='en-us'
)
"""
            }
        ]

```

### `views/AntdPagination/demos/pagination_simple_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPagination(
            defaultPageSize=10, total=100, simple=True, showTotal=False
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPagination(
            defaultPageSize=10,
            total=100,
            simple=True,
            showTotal=False,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10, total=100, simple=True, showTotal=False
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10,
    total=100,
    simple=True,
    showTotal=False,
    locale='en-us',
)
"""
            }
        ]

```

### `views/AntdPagination/demos/pagination_size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdPagination(
            defaultPageSize=10, total=100, size='small'
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdPagination(
            defaultPageSize=10, total=100, size='small', locale='en-us'
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10, total=100, size='small'
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdPagination(
    defaultPageSize=10, total=100, size='small', locale='en-us'
)
"""
            }
        ]

```

### `views/AntdPagination/demos/show_less_items.py`
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
            fac.AntdDivider(
                'showLessItems=False（默认）', innerTextOrientation='left'
            ),
            fac.AntdPagination(defaultPageSize=10, total=100, current=5),
            fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
            fac.AntdPagination(
                defaultPageSize=10, total=100, showLessItems=True, current=5
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'showLessItems=False（default）', innerTextOrientation='left'
            ),
            fac.AntdPagination(
                defaultPageSize=10, total=100, current=5, locale='en-us'
            ),
            fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
            fac.AntdPagination(
                defaultPageSize=10,
                total=100,
                showLessItems=True,
                current=5,
                locale='en-us',
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
    fac.AntdDivider(
        'showLessItems=False（默认）', innerTextOrientation='left'
    ),
    fac.AntdPagination(defaultPageSize=10, total=100, current=5),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdPagination(
        defaultPageSize=10, total=100, showLessItems=True, current=5
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
    fac.AntdDivider(
        'showLessItems=False（default）', innerTextOrientation='left'
    ),
    fac.AntdPagination(
        defaultPageSize=10, total=100, current=5, locale='en-us'
    ),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdPagination(
        defaultPageSize=10,
        total=100,
        showLessItems=True,
        current=5,
        locale='en-us',
    ),
]
"""
            }
        ]

```

## API 文档

- id (string; optional):
    Unique identifier for the component.

- align (a value equal to: 'start', 'center', 'end'; default 'start'):
    Component alignment specification, with options `start`, `center`, `end`. Default value: `start`.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- batchPropsNames (list of strings; optional):
    List of property names to be included in batch property listening. Default value: `[]`.

- batchPropsValues (dict; optional):
    Batch listening for property values corresponding to the current batchPropsNames.

- className (string | dict; optional):
    Current component CSS class name, supporting [dynamic CSS](/advanced-classname).

- current (number; optional):
    Listening to or setting the current page number.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- defaultCurrent (number; default 1):
    The current page number upon initialization. Default value: `1`.

- defaultPageSize (number; default 10):
    The number of items per page upon initialization. Default value: `10`.

- disabled (boolean; default False):
    Whether to disable the functionality of the current component. Default value: `False`.

- hideOnSinglePage (boolean; default False):
    Whether to hide the pager when there is only one page. Default value: `False`.

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

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    Component text language, with options `zh-cn` (Simplified Chinese), `en-us` (English), `de-de` (German).
    Default value: `zh-cn`.

- pageSize (number; optional):
    Listening to or setting the number of items per page.

- pageSizeOptions (list of numbers; optional):
    Options for switching the number of items per page.

- persisted_props (list of a value equal to: 'current', 'pageSize's; default ['current', 'pageSize']):
    Array of property values enabled for persistence in the current component, with options `current`, `pageSize`. Default value: `['current', 'pageSize']`.

- persistence (boolean | string | number; optional):
    Whether to enable persistence for the current component.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The type of persistent storage for the current component's properties. Default value: `local`.

- showLessItems (boolean; default False):
    Whether to display fewer page jump buttons. Default value: `False`.

- showQuickJumper (boolean; default False):
    Whether to render a quick page jump control. Default value: `False`.

- showSizeChanger (boolean; default False):
    Whether to render a page size switcher. Default value: `False`.

- showTotal (boolean; default True):
    Whether to render a description of the total number of records. Default value: `True`.

- showTotalPrefix (string; optional):
    Prefix content for the total number of records description.

- showTotalSuffix (string; optional):
    Suffix content for the total number of records description.

- simple (boolean; default False):
    Whether to enable simple mode. Default value: `False`.

- size (a value equal to: 'default', 'small'; default 'default'):
    Component size specification, with options `default`, `small`. Default value: `default`.

- style (dict; optional):
    CSS styles for the current component.

- total (number; optional):
    Total number of records.
