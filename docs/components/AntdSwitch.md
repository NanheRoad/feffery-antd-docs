# AntdSwitch

## 简介源码：`views/AntdSwitch/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {"title": translator.t("组件介绍")},
                {"title": translator.t("数据录入")},
                {"title": translator.t("AntdSwitch 开关")},
            ],
            style={"marginBottom": 8},
        ),
        fac.AntdTitle(translator.t("AntdSwitch 开关"), level=2),
        fac.AntdParagraph(translator.t("使用开关在两种状态之间切换。")),
    ]

```

## 示例源码（demos）

### `views/AntdSwitch/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render this demo case"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        title_basic = "基础回调"
        title_simple = "简单用例"
        placeholder = "切换右侧开关状态以激活/禁用输入框"
    elif current_locale == "en-us":
        title_basic = "Basic callbacks"
        title_simple = "Simple example"
        placeholder = "Toggle the switch on the right to enable/disable the input"

    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider(title_basic, innerTextOrientation="left"),
            fac.AntdSwitch(id="switch-callback-demo"),
            fac.AntdCard(
                id="switch-callback-output-demo",
                styles={"header": {"display": "none"}},
            ),
            fac.AntdDivider(title_simple, innerTextOrientation="left"),
            fac.AntdFlex(
                [
                    fac.AntdInput(
                        placeholder=placeholder,
                        id="input-switch-simple-demo",
                        disabled=True,
                    ),
                    fac.AntdSwitch(
                        id="switch-input-simple-demo",
                        checked=False,
                    ),
                ],
                align="center",
                gap=5,
            ),
        ],
        direction="vertical",
        style={"width": "100%"},
    )

    return demo_contents


# 基础回调展示 / Basic callback
@app.callback(
    Output("switch-callback-output-demo", "children"),
    Input("switch-callback-demo", "checked"),
    prevent_initial_call=True,
)
def switch_callback_demo(checked):
    # keeping label 'checked' consistent with source demo
    return f"checked: {checked}"


# 简单用例展示 / Simple example
@app.callback(
    Output("input-switch-simple-demo", "disabled"),
    Input("switch-input-simple-demo", "checked"),
    prevent_initial_call=True,
)
def switch_input_callback_demo(checked):
    return not checked


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for current locale"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('基础回调', innerTextOrientation='left'),
        fac.AntdSwitch(id='switch-callback-demo'),
        fac.AntdCard(
            id='switch-callback-output-demo',
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider('简单用例', innerTextOrientation='left'),
        fac.AntdFlex(
            [
                fac.AntdInput(
                    placeholder='切换右侧开关状态以激活/禁用输入框',
                    id='input-switch-simple-demo',
                    disabled=True,
                ),
                fac.AntdSwitch(
                    id='switch-input-simple-demo',
                    checked=False,
                ),
            ],
            align='center',
            gap=5,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)


# 基础回调展示
@app.callback(
    Output('switch-callback-output-demo', 'children'),
    Input('switch-callback-demo', 'checked'),
    prevent_initial_call=True,
)
def switch_callback_demo(checked):
    return f'checked: {checked}'


# 简单用例展示
@app.callback(
    Output('input-switch-simple-demo', 'disabled'),
    Input('switch-input-simple-demo', 'checked'),
    prevent_initial_call=True,
)
def switch_input_callback_demo(checked):
    return not checked
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDivider('Basic callbacks', innerTextOrientation='left'),
        fac.AntdSwitch(id='switch-callback-demo'),
        fac.AntdCard(
            id='switch-callback-output-demo',
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider('Simple example', innerTextOrientation='left'),
        fac.AntdFlex(
            [
                fac.AntdInput(
                    placeholder='Toggle the switch on the right to enable/disable the input',
                    id='input-switch-simple-demo',
                    disabled=True,
                ),
                fac.AntdSwitch(
                    id='switch-input-simple-demo',
                    checked=False,
                ),
            ],
            align='center',
            gap=5,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)


@app.callback(
    Output('switch-callback-output-demo', 'children'),
    Input('switch-callback-demo', 'checked'),
    prevent_initial_call=True,
)
def switch_callback_demo(checked):
    return f'checked: {checked}'


@app.callback(
    Output('input-switch-simple-demo', 'disabled'),
    Input('switch-input-simple-demo', 'checked'),
    prevent_initial_call=True,
)
def switch_input_callback_demo(checked):
    return not checked
"""
            }
        ]

```

### `views/AntdSwitch/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(),
            fac.AntdSwitch(checked=True),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(),
        fac.AntdSwitch(checked=True),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdSwitch/demos/custom_checked_children.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render this demo case"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                # 直接传入字符串
                fac.AntdSwitch(checkedChildren="开", unCheckedChildren="关"),
                # 传入AntdIcon组件
                fac.AntdSwitch(
                    checkedChildren=fac.AntdIcon(icon="antd-check"),
                    unCheckedChildren=fac.AntdIcon(icon="antd-close"),
                    checked=True,
                ),
                # 传入任意适宜静态展示的组件并配合style属性自定义样式，以AntdText为例
                fac.AntdSwitch(
                    checkedChildren=fac.AntdText(
                        "checked", strong=True, style={"color": "yellow"}
                    ),
                    unCheckedChildren=fac.AntdText(
                        "unChecked", strong=True, style={"color": "black"}
                    ),
                ),
            ],
            direction="vertical",
            style={"width": "100%"},
        )
    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                # Pass plain strings directly
                fac.AntdSwitch(checkedChildren="On", unCheckedChildren="Off"),
                # Pass an AntdIcon component
                fac.AntdSwitch(
                    checkedChildren=fac.AntdIcon(icon="antd-check"),
                    unCheckedChildren=fac.AntdIcon(icon="antd-close"),
                    checked=True,
                ),
                # Pass any component suitable for static display and customize styles via style prop; AntdText as an example
                fac.AntdSwitch(
                    checkedChildren=fac.AntdText(
                        "checked", strong=True, style={"color": "yellow"}
                    ),
                    unCheckedChildren=fac.AntdText(
                        "unChecked", strong=True, style={"color": "black"}
                    ),
                ),
            ],
            direction="vertical",
            style={"width": "100%"},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for current locale"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        # 直接传入字符串
        fac.AntdSwitch(
            checkedChildren='开',
            unCheckedChildren='关',
        ),
        # 传入AntdIcon组件
        fac.AntdSwitch(
            checkedChildren=fac.AntdIcon(icon='antd-check'),
            unCheckedChildren=fac.AntdIcon(icon='antd-close'),
            checked=True,
        ),
        # 传入任意适宜静态展示的组件并配合style属性自定义样式，以AntdText为例
        fac.AntdSwitch(
            checkedChildren=fac.AntdText(
                'checked', strong=True, style={'color': 'yellow'}
            ),
            unCheckedChildren=fac.AntdText(
                'unChecked', strong=True, style={'color': 'black'}
            ),
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        # Pass plain strings directly
        fac.AntdSwitch(
            checkedChildren='On',
            unCheckedChildren='Off',
        ),
        # Pass an AntdIcon component
        fac.AntdSwitch(
            checkedChildren=fac.AntdIcon(icon='antd-check'),
            unCheckedChildren=fac.AntdIcon(icon='antd-close'),
            checked=True,
        ),
        # Pass any component suitable for static display and customize styles via style prop; AntdText as an example
        fac.AntdSwitch(
            checkedChildren=fac.AntdText(
                'checked', strong=True, style={'color': 'yellow'}
            ),
            unCheckedChildren=fac.AntdText(
                'unChecked', strong=True, style={'color': 'black'}
            ),
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdSwitch/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(disabled=True),
            fac.AntdSwitch(disabled=True, checked=True),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(disabled=True),
        fac.AntdSwitch(disabled=True, checked=True),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdSwitch/demos/loading.py`
```python
import time

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render this demo case"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        tip_text = "点击切换后loading 3秒："
    elif current_locale == "en-us":
        tip_text = "After toggling, loading for 3 seconds:"

    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(loading=True),
            fac.AntdSwitch(loading=True, checked=True),
            fac.AntdText(tip_text),
            fac.AntdSwitch(
                # 需要设置好checked参数，否则会无法避免初次加载
                checked=False,
                id="switch-loading-demo",
            ),
            html.Div(id="switch-output-demo"),
        ],
        direction="vertical",
        style={"width": "100%"},
    )

    return demo_contents


@app.callback(
    Output("switch-output-demo", "children"),
    Input("switch-loading-demo", "checked"),
    # 配合running参数，实现回调运行中和运行结束后设置loading状态的效果
    running=[[Output("switch-loading-demo", "loading"), True, False]],
    prevent_initial_call=True,
)
def callback_func(checked):
    # 模拟进行一些耗时的回调内操作
    time.sleep(3)

    locale = get_current_locale()
    if locale == "zh-cn":
        content = "已开启" if checked else "已关闭"
    else:
        content = "Turned on" if checked else "Turned off"

    return fac.AntdMessage(
        content=content,
        type="success" if checked else "warning",
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSwitch(loading=True),
        fac.AntdSwitch(loading=True, checked=True),
        fac.AntdText('点击切换后loading 3秒：'),
        fac.AntdSwitch(
            # 需要设置好checked参数，否则会无法避免初次加载
            checked=False,
            id='switch-loading-demo',
        ),
        html.Div(id='switch-output-demo'),
    ],
    direction='vertical',
    style={'width': '100%'},
)


@app.callback(
    Output('switch-output-demo', 'children'),
    Input('switch-loading-demo', 'checked'),
    # 配合running参数，实现回调运行中和运行结束后设置loading状态的效果
    running=[[Output('switch-loading-demo', 'loading'), True, False]],
    prevent_initial_call=True,
)
def callback_func(checked):
    # 模拟进行一些耗时的回调内操作
    time.sleep(3)

    return fac.AntdMessage(
        content='已开启' if checked else '已关闭',
        type='success' if checked else 'warning',
    )
"""
            }
        ]
    elif locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSwitch(loading=True),
        fac.AntdSwitch(loading=True, checked=True),
        fac.AntdText('After toggling, loading for 3 seconds:'),
        fac.AntdSwitch(
            checked=False,
            id='switch-loading-demo',
        ),
        html.Div(id='switch-output-demo'),
    ],
    direction='vertical',
    style={'width': '100%'},
)


@app.callback(
    Output('switch-output-demo', 'children'),
    Input('switch-loading-demo', 'checked'),
    running=[[Output('switch-loading-demo', 'loading'), True, False]],
    prevent_initial_call=True,
)
def callback_func(checked):
    time.sleep(3)

    return fac.AntdMessage(
        content='Turned on' if checked else 'Turned off',
        type='success' if checked else 'warning',
    )
"""
            }
        ]

```

### `views/AntdSwitch/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(readOnly=True),
            fac.AntdSwitch(readOnly=True, checked=True),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(readOnly=True),
        fac.AntdSwitch(readOnly=True, checked=True),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdSwitch/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(checked=True),
            fac.AntdSwitch(size='small', checked=True),
        ],
        direction='vertical',
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(checked=True),
        fac.AntdSwitch(size='small', checked=True),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
"""
    }
]

```

## API 文档

- id (string; optional):
  Component unique id.

- key (string; optional):
  Update the `key` value of the current component to force a re-render of the current component.

- className (string | dict; optional):
  CSS class name of the current component, supports [dynamic css](/advanced-classname).

- name (string; optional):
  Used with `AntdForm` for batch value collection/control, serving as the field name of the current form item, with `id` as the default value.

- enableBatchControl (boolean; default True):
  Controls whether the current component participates in the effective `AntdForm` batch value collection/control feature. Default: `True`.

- disabled (boolean; default False):
  Whether to disable the current component. Default: `False`.

- autoFocus (boolean; default False):
  Whether to automatically gain focus. Default: `False`.

- checked (boolean; optional):
  Listen to or set whether the current switch is on.

- checkedChildren (a list of or a singular dash component, string or number; optional):
  Component type, embedded content when in the “on” state.

- unCheckedChildren (a list of or a singular dash component, string or number; optional):
  Component type, embedded content when in the “off” state.

- size (a value equal to: 'default', 'small'; default 'default'):
  Current component size specification. Options are `'small'`, `'middle'`. Default: `'default'`.

- loading (boolean; default False):
  Whether to render a loading state. Default: `False`.

- readOnly (boolean; default False):
  Whether to render as read-only. Default: `False`.

- batchPropsNames (list of strings; optional):
  Several property names that need to be included in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):
  Listen to several property values specified in `batchPropsNames`.

- data-_ (string; optional):
  Wildcard attributes in `data-_` format.

- aria-_ (string; optional):
  Wildcard attributes in `aria-_` format.

- loading_state (dict; optional)

  `loading_state` is a dict with keys:

  - is_loading (boolean; optional):
    Determines if the component is loading or not.

  - prop_name (string; optional):
    Holds which property is loading.

  - component_name (string; optional):
    Holds the name of the component that is loading.

- persistence (boolean | string | number; optional):
  Whether to enable [prop persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'checked's; optional):
  Several property names for which the persistence feature is enabled. Options are `'checked'`. Default: `['checked']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
  Type of persistent storage for properties. Options are `'local'` (local persistence), `'session'` (session persistence), `'memory'` (in-memory persistence)
  Default: `'local'`.
