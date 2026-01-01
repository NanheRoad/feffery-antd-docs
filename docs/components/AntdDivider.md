# AntdDivider

## 简介源码：`views/AntdDivider/intro.py`
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
                {'title': translator.t('AntdDivider 分割线')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdDivider 分割线'), level=2),
        fac.AntdParagraph(
            translator.t('对控件或功能区进行水平或竖直方向上的分割。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdDivider/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [fac.AntdDivider(), fac.AntdDivider(isDashed=True)]

    return demo_contents


code_string = [
    {
        'code': """
[fac.AntdDivider(), fac.AntdDivider(isDashed=True)]
"""
    }
]

```

### `views/AntdDivider/demos/inner_text.py`
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
            # 默认居中
            fac.AntdDivider('AntdDivider'),
            # 左对齐
            fac.AntdDivider('AntdDivider', innerTextOrientation='left'),
            # 右对齐且设置内嵌文字样式
            fac.AntdDivider(
                'AntdDivider', innerTextOrientation='right', fontStyle='oblique'
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            # default
            fac.AntdDivider('AntdDivider'),
            # left
            fac.AntdDivider('AntdDivider', innerTextOrientation='left'),
            # right
            fac.AntdDivider(
                'AntdDivider', innerTextOrientation='right', fontStyle='oblique'
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
    # 默认居中
    fac.AntdDivider('AntdDivider'),
    # 左对齐
    fac.AntdDivider('AntdDivider', innerTextOrientation='left'),
    # 右对齐且设置内嵌文字样式
    fac.AntdDivider(
        'AntdDivider', innerTextOrientation='right', fontStyle='oblique'
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
    # default
    fac.AntdDivider('AntdDivider'),
    # left
    fac.AntdDivider('AntdDivider', innerTextOrientation='left'),
    # right
    fac.AntdDivider(
        'AntdDivider', innerTextOrientation='right', fontStyle='oblique'
    ),
]
"""
            }
        ]

```

### `views/AntdDivider/demos/plain.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider('plain=False', plain=False),
        fac.AntdDivider('plain=True'),
    ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    return [
        {
            'code': """
[
    fac.AntdDivider('plain=False', plain=False),
    fac.AntdDivider('plain=True'),
]
"""
        }
    ]

```

### `views/AntdDivider/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSegmented(
                id='divider-size-demo',
                options=['small', 'middle', 'large'],
                value='large',
            ),
            'Demo content',
            fac.AntdDivider(id='divider-size-demo-output'),
            'Demo content',
        ],
        size=0,
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    Output('divider-size-demo-output', 'size'),
    Input('divider-size-demo', 'value'),
)
def update_divider_size(value):
    return value


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='divider-size-demo',
            options=['small', 'middle', 'large'],
            value='large',
        ),
        'Demo content',
        fac.AntdDivider(id='divider-size-demo-output'),
        'Demo content',
    ],
    size=0,
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('divider-size-demo-output', 'size'),
    Input('divider-size-demo', 'value'),
)
def update_divider_size(value):
    return value
"""
    }
]

```

### `views/AntdDivider/demos/variant.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider(
            'variant="dashed"', variant='dashed', lineColor='#595959'
        ),
        fac.AntdDivider(
            'variant="dotted"', variant='dotted', lineColor='#595959'
        ),
        fac.AntdDivider(
            'variant="solid"', variant='solid', lineColor='#595959'
        ),
    ]

    return demo_contents


code_string = [
    {
        'code': """
[
    fac.AntdDivider(
        'variant="dashed"', variant='dashed', lineColor='#595959'
    ),
    fac.AntdDivider(
        'variant="dotted"', variant='dotted', lineColor='#595959'
    ),
    fac.AntdDivider(
        'variant="solid"', variant='solid', lineColor='#595959'
    ),
]
"""
    }
]

```

### `views/AntdDivider/demos/vertical.py`
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
            '项目1',
            fac.AntdDivider(direction='vertical'),
            '项目2',
            fac.AntdDivider(direction='vertical', lineColor='black'),
            '项目3',
            fac.AntdDivider(direction='vertical', lineColor='red'),
            '项目4',
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            'Project1',
            fac.AntdDivider(direction='vertical'),
            'Project2',
            fac.AntdDivider(direction='vertical', lineColor='black'),
            'Project3',
            fac.AntdDivider(direction='vertical', lineColor='red'),
            'Project4',
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
    '项目1',
    fac.AntdDivider(direction='vertical'),
    '项目2',
    fac.AntdDivider(direction='vertical', lineColor='black'),
    '项目3',
    fac.AntdDivider(direction='vertical', lineColor='red'),
    '项目4',
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    'Project1',
    fac.AntdDivider(direction='vertical'),
    'Project2',
    fac.AntdDivider(direction='vertical', lineColor='black'),
    'Project3',
    fac.AntdDivider(direction='vertical', lineColor='red'),
    'Project4',
]
"""
            }
        ]

```

## API 文档

- children (a list of or a singular dash component, string or number; optional):
    Component type, child elements within the divider.

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- className (string | dict; optional):
    Current component CSS class name, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- direction (a value equal to: "horizontal", "vertical"; default 'horizontal'):
    Direction of the divider, options include `'horizontal'`, `'vertical'`. Default value: `'horizontal'`.

- fontColor (string; optional):
    Font color of the child elements.

- fontFamily (string; optional):
    Font of the child elements.

- fontSize (string | number; optional):
    Font size of the child elements.

- fontStyle (string; optional):
    Font style of the child elements.

- fontWeight (string; optional):
    Font weight of the child elements.

- innerTextOrientation (a value equal to: "left", "center", "right"; default 'center'):
    Alignment of the child elements, options include `'left'`, `'center'`, `'right'`. Default value: `'center'`.

- isDashed (boolean; default False):
    Whether to render as a dashed line. Default value: `False`.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- lineColor (string; optional):
    Color of the divider line.

- loading_state (dict; optional):

    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is currently loading.

    - prop_name (string; optional):
        Holds which property is currently loading.

- style (dict; optional):
    CSS styles for the current component.

- variant (a value equal to: 'dashed', 'dotted', 'solid'; default 'solid'):
    Variant of the divider, options include `'dashed'` (dashed line), `'dotted'` (dotted line), `'solid'` (solid line).
    Default value: `'solid'`.
