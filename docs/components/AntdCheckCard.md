# AntdCheckCard

## 简介源码：`views/AntdCheckCard/intro.py`
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
                {'title': translator.t('数据录入')},
                {'title': translator.t('AntdCheckCard 选择卡片')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCheckCard 选择卡片'), level=2),
        fac.AntdParagraph(translator.t('用于渲染具有状态切换功能的内容卡片。')),
    ]

```

## 示例源码（demos）

### `views/AntdCheckCard/demos/basic_callbacks.py`
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
            fac.AntdCheckCard(
                fac.AntdText('选择卡片示例' * 10),
                id='check-card-demo',
                defaultChecked=False,
            ),
            fac.AntdParagraph(id='check-card-demo-output'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdCheckCard(
                fac.AntdText('Demo' * 20),
                id='check-card-demo',
                defaultChecked=False,
            ),
            fac.AntdParagraph(id='check-card-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('check-card-demo-output', 'children'),
    Input('check-card-demo', 'checked'),
)
def check_card_demo(checked):
    return f'checked: {checked}'


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdCheckCard(
        fac.AntdText('选择卡片示例' * 10),
        id='check-card-demo',
        defaultChecked=False,
    ),
    fac.AntdParagraph(id='check-card-demo-output'),
]

...

@app.callback(
    Output('check-card-demo-output', 'children'),
    Input('check-card-demo', 'checked'),
)
def check_card_demo(checked):
    return f'checked: {checked}'
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdCheckCard(
        fac.AntdText('Demo' * 20),
        id='check-card-demo',
        defaultChecked=False,
    ),
    fac.AntdParagraph(id='check-card-demo-output'),
]

...

@app.callback(
    Output('check-card-demo-output', 'children'),
    Input('check-card-demo', 'checked'),
)
def check_card_demo(checked):
    return f'checked: {checked}'
"""
            }
        ]

```

### `views/AntdCheckCard/demos/basic_usage.py`
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
                fac.AntdCheckCard(fac.AntdText('选择卡片示例' * 10)),
                fac.AntdCheckCard(
                    fac.AntdStatistic(title='统计数值示例', value=1332971),
                    defaultChecked=True,
                ),
                fac.AntdCheckCard(
                    fac.AntdSpace(
                        [
                            fac.AntdAvatar(
                                mode='image',
                                size=48,
                                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                            ),
                            fac.AntdText('选择卡片示例' * 10),
                        ],
                        align='start',
                    )
                ),
            ],
            direction='vertical',
            size='small',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdCheckCard(fac.AntdText('Demo' * 20)),
                fac.AntdCheckCard(
                    fac.AntdStatistic(title='Statistic Demo', value=1332971),
                    defaultChecked=True,
                ),
                fac.AntdCheckCard(
                    fac.AntdSpace(
                        [
                            fac.AntdAvatar(
                                mode='image',
                                size=48,
                                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                            ),
                            fac.AntdText('Demo' * 20),
                        ],
                        align='start',
                    )
                ),
            ],
            direction='vertical',
            size='small',
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
        fac.AntdCheckCard(fac.AntdText('选择卡片示例' * 10)),
        fac.AntdCheckCard(
            fac.AntdStatistic(title='统计数值示例', value=1332971),
            defaultChecked=True,
        ),
        fac.AntdCheckCard(
            fac.AntdSpace(
                [
                    fac.AntdAvatar(
                        mode='image',
                        size=48,
                        src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                    ),
                    fac.AntdText('选择卡片示例' * 10),
                ],
                align='start',
            )
        ),
    ],
    direction='vertical',
    size='small',
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
        fac.AntdCheckCard(fac.AntdText('Demo' * 20)),
        fac.AntdCheckCard(
            fac.AntdStatistic(title='Statistic Demo', value=1332971),
            defaultChecked=True,
        ),
        fac.AntdCheckCard(
            fac.AntdSpace(
                [
                    fac.AntdAvatar(
                        mode='image',
                        size=48,
                        src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                    ),
                    fac.AntdText('Demo' * 20),
                ],
                align='start',
            )
        ),
    ],
    direction='vertical',
    size='small',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdCheckCard/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCheckCard(
            fac.AntdText('选择卡片示例' * 10), disabled=True, checked=True
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCheckCard(
            fac.AntdText('Demo' * 20), disabled=True, checked=True
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCheckCard(
    fac.AntdText('选择卡片示例' * 10), disabled=True, checked=True
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCheckCard(
    fac.AntdText('Demo' * 20), disabled=True, checked=True
)
"""
            }
        ]

```

### `views/AntdCheckCard/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCheckCard(
            fac.AntdText('选择卡片示例' * 10), readOnly=True, checked=True
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCheckCard(
            fac.AntdText('Demo' * 20), readOnly=True, checked=True
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCheckCard(
    fac.AntdText('选择卡片示例' * 10), readOnly=True, checked=True
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCheckCard(
    fac.AntdText('Demo' * 20), readOnly=True, checked=True
)
"""
            }
        ]

```

### `views/AntdCheckCard/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCheckCard(f'size="{size}"', size=size)
            for size in ['small', 'default', 'large']
        ],
        direction='vertical',
        size=0,
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdCheckCard(f'size="{size}"', size=size)
        for size in ['small', 'default', 'large']
    ],
    direction='vertical',
    size=0,
    style={'width': '100%'},
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
    Component type, nested elements.

- style (dict; optional):
    CSS styles for the current component.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- name (string; optional):
    Used in conjunction with the `AntdForm` form batch value collection/control feature, serving as the field name for the current form item, with `id` as the default value.

- checked (boolean; optional):
    Listens to or sets whether it is checked.

- defaultChecked (boolean; optional):
    Whether it is checked by default.

- bordered (boolean; default True):
    Whether to display a border. Default value: `True`.

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- size (a value equal to: 'small', 'default', 'large'; default 'default'):
    The size specification of the current component, with options `'small'`, `'default'`, `'large'`. Default value: `'default'`.

- value (number | string; optional):
    The value of the currently selected card.

- readOnly (boolean; default False):
    Whether to render as read-only. Default value: `False`.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- persistence (boolean | string | number; optional):
    Whether to enable [property persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'checked's; default ['checked']):
    The names of several properties that are enabled for property persistence, with the option `'checked'`. Default value: `['checked']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The storage type for property persistence, with options `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence).
    Default value: `'local'`.
