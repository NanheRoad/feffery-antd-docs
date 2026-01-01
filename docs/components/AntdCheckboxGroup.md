# AntdCheckboxGroup

## 简介源码：`views/AntdCheckboxGroup/intro.py`
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
                {'title': translator.t('AntdCheckboxGroup 组合选择框')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCheckboxGroup 组合选择框'), level=2),
        fac.AntdParagraph(
            translator.t('由若干选择框组成，用于在一组可选项中进行多项选择。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdCheckboxGroup/demos/basic_callbacks.py`
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
            fac.AntdCheckboxGroup(
                id='checkbox-group-demo1',
                options=[
                    {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
                ],
            ),
            fac.AntdParagraph(id='checkbox-group-demo1-output'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdCheckboxGroup(
                id='checkbox-group-demo1',
                options=[
                    {'label': f'Option{i}', 'value': f'Option{i}'}
                    for i in range(5)
                ],
            ),
            fac.AntdParagraph(id='checkbox-group-demo1-output'),
        ]

    return demo_contents


@app.callback(
    Output('checkbox-group-demo1-output', 'children'),
    Input('checkbox-group-demo1', 'value'),
)
def checkbox_group_demo1(value):
    return f'value: {value}'


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdCheckboxGroup(
        id='checkbox-group-demo1',
        options=[
            {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
        ],
    ),
    fac.AntdParagraph(id='checkbox-group-demo1-output'),
]

...

@app.callback(
    Output('checkbox-group-demo1-output', 'children'),
    Input('checkbox-group-demo1', 'value'),
)
def checkbox_group_demo1(value):
    return f'value: {value}'
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdCheckboxGroup(
        id='checkbox-group-demo1',
        options=[
            {'label': f'Option{i}', 'value': f'Option{i}'}
            for i in range(5)
        ],
    ),
    fac.AntdParagraph(id='checkbox-group-demo1-output'),
]

...

@app.callback(
    Output('checkbox-group-demo1-output', 'children'),
    Input('checkbox-group-demo1', 'value'),
)
def checkbox_group_demo1(value):
    return f'value: {value}'
"""
            }
        ]

```

### `views/AntdCheckboxGroup/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCheckboxGroup(
            options=[
                {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
            ]
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCheckboxGroup(
            options=[
                {'label': f'Option{i}', 'value': f'Option{i}'} for i in range(5)
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
fac.AntdCheckboxGroup(
    options=[
        {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCheckboxGroup(
    options=[
        {'label': f'Option{i}', 'value': f'Option{i}'} for i in range(5)
    ]
)
"""
            }
        ]

```

### `views/AntdCheckboxGroup/demos/disabled.py`
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
            fac.AntdDivider('禁用部分选项', innerTextOrientation='left'),
            fac.AntdCheckboxGroup(
                options=[
                    {
                        'label': f'选项{i}',
                        'value': f'选项{i}',
                        'disabled': i % 2 != 0,
                    }
                    for i in range(5)
                ]
            ),
            fac.AntdDivider('禁用整体', innerTextOrientation='left'),
            fac.AntdCheckboxGroup(
                options=[
                    {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
                ],
                disabled=True,
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'Disabled part of options', innerTextOrientation='left'
            ),
            fac.AntdCheckboxGroup(
                options=[
                    {
                        'label': f'Option{i}',
                        'value': f'Option{i}',
                        'disabled': i % 2 != 0,
                    }
                    for i in range(5)
                ]
            ),
            fac.AntdDivider('Disabled all', innerTextOrientation='left'),
            fac.AntdCheckboxGroup(
                options=[
                    {'label': f'Option{i}', 'value': f'Option{i}'}
                    for i in range(5)
                ],
                disabled=True,
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
    fac.AntdDivider('禁用部分选项', innerTextOrientation='left'),
    fac.AntdCheckboxGroup(
        options=[
            {
                'label': f'选项{i}',
                'value': f'选项{i}',
                'disabled': i % 2 != 0,
            }
            for i in range(5)
        ]
    ),
    fac.AntdDivider('禁用整体', innerTextOrientation='left'),
    fac.AntdCheckboxGroup(
        options=[
            {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
        ],
        disabled=True,
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
        'Disabled part of options', innerTextOrientation='left'
    ),
    fac.AntdCheckboxGroup(
        options=[
            {
                'label': f'Option{i}',
                'value': f'Option{i}',
                'disabled': i % 2 != 0,
            }
            for i in range(5)
        ]
    ),
    fac.AntdDivider('Disabled all', innerTextOrientation='left'),
    fac.AntdCheckboxGroup(
        options=[
            {'label': f'Option{i}', 'value': f'Option{i}'}
            for i in range(5)
        ],
        disabled=True,
    ),
]
"""
            }
        ]

```

### `views/AntdCheckboxGroup/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCheckboxGroup(
            options=[
                {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
            ],
            value=['选项1', '选项3'],
            readOnly=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCheckboxGroup(
            options=[
                {'label': f'Option{i}', 'value': f'Option{i}'} for i in range(5)
            ],
            value=['Option1', 'Option3'],
            readOnly=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCheckboxGroup(
    options=[
        {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
    ],
    value=['选项1', '选项3'],
    readOnly=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCheckboxGroup(
    options=[
        {'label': f'Option{i}', 'value': f'Option{i}'} for i in range(5)
    ],
    value=['Option1', 'Option3'],
    readOnly=True,
)
"""
            }
        ]

```

### `views/AntdCheckboxGroup/demos/select_all_with_callbacks.py`
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
        demo_contents = [
            fac.AntdCheckbox(
                id='checkbox-demo-client-side',
                label='全选',
                style={'marginRight': '8px'},
            ),
            fac.AntdCheckboxGroup(
                id='checkbox-group-demo-client-side',
                options=[
                    {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
                ],
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdCheckbox(
                id='checkbox-demo-client-side',
                label='Select All',
                style={'marginRight': '8px'},
            ),
            fac.AntdCheckboxGroup(
                id='checkbox-group-demo-client-side',
                options=[
                    {'label': f'Option{i}', 'value': f'Option{i}'}
                    for i in range(5)
                ],
            ),
        ]

    return demo_contents


app.clientside_callback(
    """(checked, value, options) => {
        let ctx = dash_clientside.callback_context;
        value = value || []
        if ( ctx?.triggered[0].prop_id === 'checkbox-group-demo-client-side.value' ) {
            return [
                value.length === options.length ? true : false,
                value,
                value.length > 0 && value.length < options.length ? true : false
            ]
        } else if ( ctx?.triggered[0].prop_id === 'checkbox-demo-client-side.checked' ) {
            return [
                checked,
                checked ? options.map(item => item.value) : [],
                !checked && value.length > 0 && value.length < options.length ? true : false
            ]
        }
        throw window.dash_clientside.PreventUpdate;
    }""",
    [
        Output('checkbox-demo-client-side', 'checked'),
        Output('checkbox-group-demo-client-side', 'value'),
        Output('checkbox-demo-client-side', 'indeterminate'),
    ],
    [
        Input('checkbox-demo-client-side', 'checked'),
        Input('checkbox-group-demo-client-side', 'value'),
    ],
    State('checkbox-group-demo-client-side', 'options'),
    prevent_initial_call=True,
)


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
[
    fac.AntdCheckbox(
        id='checkbox-demo-client-side',
        label='全选',
        style={'marginRight': '8px'},
    ),
    fac.AntdCheckboxGroup(
        id='checkbox-group-demo-client-side',
        options=[
            {'label': f'选项{i}', 'value': f'选项{i}'} for i in range(5)
        ],
    ),
]

...

app.clientside_callback(
    """(checked, value, options) => {
        let ctx = dash_clientside.callback_context;
        value = value || []
        if ( ctx?.triggered[0].prop_id === 'checkbox-group-demo-client-side.value' ) {
            return [
                value.length === options.length ? true : false,
                value,
                value.length > 0 && value.length < options.length ? true : false
            ]
        } else if ( ctx?.triggered[0].prop_id === 'checkbox-demo-client-side.checked' ) {
            return [
                checked,
                checked ? options.map(item => item.value) : [],
                !checked && value.length > 0 && value.length < options.length ? true : false
            ]
        }
        throw window.dash_clientside.PreventUpdate;
    }""",
    [
        Output('checkbox-demo-client-side', 'checked'),
        Output('checkbox-group-demo-client-side', 'value'),
        Output('checkbox-demo-client-side', 'indeterminate'),
    ],
    [
        Input('checkbox-demo-client-side', 'checked'),
        Input('checkbox-group-demo-client-side', 'value'),
    ],
    State('checkbox-group-demo-client-side', 'options'),
    prevent_initial_call=True,
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
[
    fac.AntdCheckbox(
        id='checkbox-demo-client-side',
        label='Select All',
        style={'marginRight': '8px'},
    ),
    fac.AntdCheckboxGroup(
        id='checkbox-group-demo-client-side',
        options=[
            {'label': f'Option{i}', 'value': f'Option{i}'}
            for i in range(5)
        ],
    ),
]

...

app.clientside_callback(
    """(checked, value, options) => {
        let ctx = dash_clientside.callback_context;
        value = value || []
        if ( ctx?.triggered[0].prop_id === 'checkbox-group-demo-client-side.value' ) {
            return [
                value.length === options.length ? true : false,
                value,
                value.length > 0 && value.length < options.length ? true : false
            ]
        } else if ( ctx?.triggered[0].prop_id === 'checkbox-demo-client-side.checked' ) {
            return [
                checked,
                checked ? options.map(item => item.value) : [],
                !checked && value.length > 0 && value.length < options.length ? true : false
            ]
        }
        throw window.dash_clientside.PreventUpdate;
    }""",
    [
        Output('checkbox-demo-client-side', 'checked'),
        Output('checkbox-group-demo-client-side', 'value'),
        Output('checkbox-demo-client-side', 'indeterminate'),
    ],
    [
        Input('checkbox-demo-client-side', 'checked'),
        Input('checkbox-group-demo-client-side', 'value'),
    ],
    State('checkbox-group-demo-client-side', 'options'),
    prevent_initial_call=True,
)
'''
            }
        ]

```

## API 文档

- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- style (dict; optional):
    CSS styles for the current component.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- name (string; optional):
    Used in conjunction with the `AntdForm` form for batch value collection/control, serving as the field name for the current form item, with `id` as the default value.

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- options (list of dicts; optional):
    Defines the data structure required to construct a combo box.

    `options` is a list of string | number | dict with keys:

    - disabled (boolean; optional):
        Whether to disable the current selection box. Default value: `False`.

    - label (a list of or a singular dash component, string or number; optional):
        Component type, the label content of the current selection box.

    - value (string | number; optional):
        The corresponding value of the current selection box.

- value (list of string | numbers; optional):
    To listen for or set the selected value.

- readOnly (boolean; default False):
    Whether to render in read-only state. Default value: `False`.

- batchPropsNames (list of strings; optional):
    Several property names to be included in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):
    Listens to the values of several properties specified in `batchPropsNames`.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional):
    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- persistence (boolean | string | number; optional):
    Whether to enable [property persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; default ['value']):
    Several property names for the property persistence feature, with the option `'value'`. Default value: `['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    Property persistence storage type, with options `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence).
    Default value: `'local'`.
