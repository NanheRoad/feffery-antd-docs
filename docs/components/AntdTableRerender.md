# AntdTableRerender

## 简介源码：`views/AntdTableRerender/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('数据展示')},
                {'title': translator.t('AntdTable 表格')},
                {'title': translator.t('再渲染模式')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件中使用不同的再渲染模式。')),
    ]

```

## 示例源码（demos）

### `views/AntdTableRerender/demos/button_mode_and_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-button-demo',
                columns=[
                    {
                        'title': 'button示例1',
                        'dataIndex': 'button示例1',
                        'renderOptions': {'renderType': 'button'},
                    },
                    {
                        'title': 'button示例2',
                        'dataIndex': 'button示例2',
                        'renderOptions': {'renderType': 'button'},
                    },
                    {
                        'title': 'button示例3',
                        'dataIndex': 'button示例3',
                        'renderOptions': {
                            'renderType': 'button',
                            'renderButtonPopConfirmProps': {
                                'title': '确认执行？',
                                'okText': '确认',
                                'cancelText': '取消',
                            },
                        },
                    },
                ],
                data=[
                    {
                        'button示例1': {
                            'content': f'按钮1-{i}',
                            'type': 'link',
                            'custom': 'balabalabalabala',
                        },
                        'button示例2': [
                            {
                                'content': f'按钮2-{i}-{j}',
                                'type': 'primary',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 3)
                        ],
                        'button示例3': [
                            {
                                'content': f'按钮3-{i}-{j}',
                                'type': 'dashed',
                                'danger': True,
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 3)
                        ],
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
            ),
            html.Pre(id='table-rerender-button-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-button-demo',
                locale='en-us',
                columns=[
                    {
                        'title': 'Button Example 1',
                        'dataIndex': 'Button Example 1',
                        'renderOptions': {'renderType': 'button'},
                    },
                    {
                        'title': 'Button Example 2',
                        'dataIndex': 'Button Example 2',
                        'renderOptions': {'renderType': 'button'},
                    },
                    {
                        'title': 'Button Example 3',
                        'dataIndex': 'Button Example 3',
                        'renderOptions': {
                            'renderType': 'button',
                            'renderButtonPopConfirmProps': {
                                'title': 'Confirm action?',
                                'okText': 'Confirm',
                                'cancelText': 'Cancel',
                            },
                        },
                    },
                ],
                data=[
                    {
                        'Button Example 1': {
                            'content': f'Button1-{i}',
                            'type': 'link',
                            'custom': 'balabalabalabala',
                        },
                        'Button Example 2': [
                            {
                                'content': f'Button2-{i}-{j}',
                                'type': 'primary',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 3)
                        ],
                        'Button Example 3': [
                            {
                                'content': f'Button3-{i}-{j}',
                                'type': 'dashed',
                                'danger': True,
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 3)
                        ],
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
            ),
            html.Pre(id='table-rerender-button-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-rerender-button-demo-output', 'children'),
    Input('table-rerender-button-demo', 'nClicksButton'),
    [
        State('table-rerender-button-demo', 'clickedContent'),
        State('table-rerender-button-demo', 'clickedCustom'),
        State('table-rerender-button-demo', 'recentlyButtonClickedDataIndex'),
        State('table-rerender-button-demo', 'recentlyButtonClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_button_demo(
    nClicksButton,
    clickedContent,
    clickedCustom,
    recentlyButtonClickedDataIndex,
    recentlyButtonClickedRow,
):
    return json.dumps(
        dict(
            nClicksButton=nClicksButton,
            clickedContent=clickedContent,
            clickedCustom=clickedCustom,
            recentlyButtonClickedDataIndex=recentlyButtonClickedDataIndex,
            recentlyButtonClickedRow=recentlyButtonClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-button-demo',
        columns=[
            {
                'title': 'button示例1',
                'dataIndex': 'button示例1',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'button示例2',
                'dataIndex': 'button示例2',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'button示例3',
                'dataIndex': 'button示例3',
                'renderOptions': {
                    'renderType': 'button',
                    'renderButtonPopConfirmProps': {
                        'title': '确认执行？',
                        'okText': '确认',
                        'cancelText': '取消',
                    },
                },
            },
        ],
        data=[
            {
                'button示例1': {
                    'content': f'按钮1-{i}',
                    'type': 'link',
                    'custom': 'balabalabalabala',
                },
                'button示例2': [
                    {
                        'content': f'按钮2-{i}-{j}',
                        'type': 'primary',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
                'button示例3': [
                    {
                        'content': f'按钮3-{i}-{j}',
                        'type': 'dashed',
                        'danger': True,
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-rerender-button-demo-output'),
]

...

@app.callback(
    Output('table-rerender-button-demo-output', 'children'),
    Input('table-rerender-button-demo', 'nClicksButton'),
    [
        State('table-rerender-button-demo', 'clickedContent'),
        State('table-rerender-button-demo', 'clickedCustom'),
        State('table-rerender-button-demo', 'recentlyButtonClickedDataIndex'),
        State('table-rerender-button-demo', 'recentlyButtonClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_button_demo(
    nClicksButton,
    clickedContent,
    clickedCustom,
    recentlyButtonClickedDataIndex,
    recentlyButtonClickedRow,
):
    return json.dumps(
        dict(
            nClicksButton=nClicksButton,
            clickedContent=clickedContent,
            clickedCustom=clickedCustom,
            recentlyButtonClickedDataIndex=recentlyButtonClickedDataIndex,
            recentlyButtonClickedRow=recentlyButtonClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-button-demo',
        locale='en-us',
        columns=[
            {
                'title': 'Button Example 1',
                'dataIndex': 'Button Example 1',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'Button Example 2',
                'dataIndex': 'Button Example 2',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'Button Example 3',
                'dataIndex': 'Button Example 3',
                'renderOptions': {
                    'renderType': 'button',
                    'renderButtonPopConfirmProps': {
                        'title': 'Confirm action?',
                        'okText': 'Confirm',
                        'cancelText': 'Cancel',
                    },
                },
            },
        ],
        data=[
            {
                'Button Example 1': {
                    'content': f'Button1-{i}',
                    'type': 'link',
                    'custom': 'balabalabalabala',
                },
                'Button Example 2': [
                    {
                        'content': f'Button2-{i}-{j}',
                        'type': 'primary',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
                'Button Example 3': [
                    {
                        'content': f'Button3-{i}-{j}',
                        'type': 'dashed',
                        'danger': True,
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-rerender-button-demo-output'),
]

...

@app.callback(
    Output('table-rerender-button-demo-output', 'children'),
    Input('table-rerender-button-demo', 'nClicksButton'),
    [
        State('table-rerender-button-demo', 'clickedContent'),
        State('table-rerender-button-demo', 'clickedCustom'),
        State('table-rerender-button-demo', 'recentlyButtonClickedDataIndex'),
        State('table-rerender-button-demo', 'recentlyButtonClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_button_demo(
    nClicksButton,
    clickedContent,
    clickedCustom,
    recentlyButtonClickedDataIndex,
    recentlyButtonClickedRow,
):
    return json.dumps(
        dict(
            nClicksButton=nClicksButton,
            clickedContent=clickedContent,
            clickedCustom=clickedCustom,
            recentlyButtonClickedDataIndex=recentlyButtonClickedDataIndex,
            recentlyButtonClickedRow=recentlyButtonClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableRerender/demos/button_mode_color.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'dataIndex': 'variant参数值',
                    'title': 'variant参数值',
                },
                {
                    'dataIndex': '渲染效果',
                    'title': '渲染效果',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    'variant参数值': variant,
                    '渲染效果': [
                        {'content': color, 'color': color, 'variant': variant}
                        for color in [
                            'default',
                            'primary',
                            'danger',
                            'blue',
                            'purple',
                            'cyan',
                            'green',
                            'magenta',
                            'pink',
                            'red',
                            'orange',
                            'yellow',
                            'volcano',
                            'geekblue',
                            'lime',
                            'gold',
                        ]
                    ],
                }
                for variant in [
                    'outlined',
                    'dashed',
                    'solid',
                    'filled',
                    'text',
                    'link',
                ]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'dataIndex': 'Variant Value',
                    'title': 'Variant Value',
                },
                {
                    'dataIndex': 'Render Effect',
                    'title': 'Render Effect',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    'Variant Value': variant,
                    'Render Effect': [
                        {'content': color, 'color': color, 'variant': variant}
                        for color in [
                            'default',
                            'primary',
                            'danger',
                            'blue',
                            'purple',
                            'cyan',
                            'green',
                            'magenta',
                            'pink',
                            'red',
                            'orange',
                            'yellow',
                            'volcano',
                            'geekblue',
                            'lime',
                            'gold',
                        ]
                    ],
                }
                for variant in [
                    'outlined',
                    'dashed',
                    'solid',
                    'filled',
                    'text',
                    'link',
                ]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'dataIndex': 'variant参数值',
            'title': 'variant参数值',
        },
        {
            'dataIndex': '渲染效果',
            'title': '渲染效果',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            'variant参数值': variant,
            '渲染效果': [
                {'content': color, 'color': color, 'variant': variant}
                for color in [
                    'default',
                    'primary',
                    'danger',
                    'blue',
                    'purple',
                    'cyan',
                    'green',
                    'magenta',
                    'pink',
                    'red',
                    'orange',
                    'yellow',
                    'volcano',
                    'geekblue',
                    'lime',
                    'gold',
                ]
            ],
        }
        for variant in [
            'outlined',
            'dashed',
            'solid',
            'filled',
            'text',
            'link',
        ]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'dataIndex': 'Variant Value',
            'title': 'Variant Value',
        },
        {
            'dataIndex': 'Render Effect',
            'title': 'Render Effect',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            'Variant Value': variant,
            'Render Effect': [
                {'content': color, 'color': color, 'variant': variant}
                for color in [
                    'default',
                    'primary',
                    'danger',
                    'blue',
                    'purple',
                    'cyan',
                    'green',
                    'magenta',
                    'pink',
                    'red',
                    'orange',
                    'yellow',
                    'volcano',
                    'geekblue',
                    'lime',
                    'gold',
                ]
            ],
        }
        for variant in [
            'outlined',
            'dashed',
            'solid',
            'filled',
            'text',
            'link',
        ]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/button_mode_independent_add_popconfirm.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'dataIndex': '按钮示例',
                    'title': '按钮示例',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    '按钮示例': [
                        {
                            'content': '带气泡确认',
                            'popConfirmProps': {
                                'title': '气泡确认标题',
                                'okText': '确认',
                                'cancelText': '取消',
                            },
                        },
                        {
                            'content': '不带气泡确认',
                        },
                    ]
                }
            ],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'dataIndex': 'Button Example',
                    'title': 'Button Example',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    'Button Example': [
                        {
                            'content': 'With PopConfirm',
                            'popConfirmProps': {
                                'title': 'PopConfirm Title',
                                'okText': 'Confirm',
                                'cancelText': 'Cancel',
                            },
                        },
                        {
                            'content': 'Without PopConfirm',
                        },
                    ]
                }
            ],
            bordered=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'dataIndex': '按钮示例',
            'title': '按钮示例',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            '按钮示例': [
                {
                    'content': '带气泡确认',
                    'popConfirmProps': {
                        'title': '气泡确认标题',
                        'okText': '确认',
                        'cancelText': '取消',
                    },
                },
                {
                    'content': '不带气泡确认',
                },
            ]
        }
    ],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'dataIndex': 'Button Example',
            'title': 'Button Example',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            'Button Example': [
                {
                    'content': 'With PopConfirm',
                    'popConfirmProps': {
                        'title': 'PopConfirm Title',
                        'okText': 'Confirm',
                        'cancelText': 'Cancel',
                    },
                },
                {
                    'content': 'Without PopConfirm',
                },
            ]
        }
    ],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/button_mode_independent_add_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'dataIndex': '按钮示例',
                    'title': '按钮示例',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    '按钮示例': [
                        {
                            'content': '带tooltip',
                            'tooltip': {'title': 'tooltip示例'},
                        },
                        {
                            'content': '不带tooltip',
                        },
                    ]
                }
            ],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'dataIndex': 'Button Example',
                    'title': 'Button Example',
                    'renderOptions': {'renderType': 'button'},
                },
            ],
            data=[
                {
                    'Button Example': [
                        {
                            'content': 'With tooltip',
                            'tooltip': {'title': 'Tooltip Example'},
                        },
                        {
                            'content': 'Without tooltip',
                        },
                    ]
                }
            ],
            bordered=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'dataIndex': '按钮示例',
            'title': '按钮示例',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            '按钮示例': [
                {
                    'content': '带tooltip',
                    'tooltip': {'title': 'tooltip示例'},
                },
                {
                    'content': '不带tooltip',
                },
            ]
        }
    ],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'dataIndex': 'Button Example',
            'title': 'Button Example',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            'Button Example': [
                {
                    'content': 'With tooltip',
                    'tooltip': {'title': 'Tooltip Example'},
                },
                {
                    'content': 'Without tooltip',
                },
            ]
        }
    ],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/checkbox_mode_and_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-checkbox-demo',
                columns=[
                    {
                        'title': 'checkbox示例',
                        'dataIndex': 'checkbox示例',
                        'renderOptions': {'renderType': 'checkbox'},
                    }
                ],
                data=[
                    {
                        'checkbox示例': {
                            'checked': i % 2 == 0,
                            'label': f'选项{i}',
                            'custom': 'balabalabalabala',
                        }
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-checkbox-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-checkbox-demo',
                locale='en-us',
                columns=[
                    {
                        'title': 'Checkbox Example',
                        'dataIndex': 'Checkbox Example',
                        'renderOptions': {'renderType': 'checkbox'},
                    }
                ],
                data=[
                    {
                        'Checkbox Example': {
                            'checked': i % 2 == 0,
                            'label': f'Option {i}',
                            'custom': 'balabalabalabala',
                        }
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-checkbox-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-rerender-checkbox-demo-output', 'children'),
    [
        Input('table-rerender-checkbox-demo', 'recentlyCheckedLabel'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedDataIndex'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedStatus'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_checkbox_demo(
    recentlyCheckedLabel,
    recentlyCheckedDataIndex,
    recentlyCheckedStatus,
    recentlyCheckedRow,
):
    return json.dumps(
        dict(
            recentlyCheckedLabel=recentlyCheckedLabel,
            recentlyCheckedDataIndex=recentlyCheckedDataIndex,
            recentlyCheckedStatus=recentlyCheckedStatus,
            recentlyCheckedRow=recentlyCheckedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-checkbox-demo',
        columns=[
            {
                'title': 'checkbox示例',
                'dataIndex': 'checkbox示例',
                'renderOptions': {'renderType': 'checkbox'},
            }
        ],
        data=[
            {
                'checkbox示例': {
                    'checked': i % 2 == 0,
                    'label': f'选项{i}',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-checkbox-demo-output'),
]

...

@app.callback(
    Output('table-rerender-checkbox-demo-output', 'children'),
    [
        Input('table-rerender-checkbox-demo', 'recentlyCheckedLabel'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedDataIndex'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedStatus'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_checkbox_demo(
    recentlyCheckedLabel,
    recentlyCheckedDataIndex,
    recentlyCheckedStatus,
    recentlyCheckedRow,
):
    return json.dumps(
        dict(
            recentlyCheckedLabel=recentlyCheckedLabel,
            recentlyCheckedDataIndex=recentlyCheckedDataIndex,
            recentlyCheckedStatus=recentlyCheckedStatus,
            recentlyCheckedRow=recentlyCheckedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-checkbox-demo',
        locale='en-us',
        columns=[
            {
                'title': 'Checkbox Example',
                'dataIndex': 'Checkbox Example',
                'renderOptions': {'renderType': 'checkbox'},
            }
        ],
        data=[
            {
                'Checkbox Example': {
                    'checked': i % 2 == 0,
                    'label': f'Option {i}',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-checkbox-demo-output'),
]

...

@app.callback(
    Output('table-rerender-checkbox-demo-output', 'children'),
    [
        Input('table-rerender-checkbox-demo', 'recentlyCheckedLabel'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedDataIndex'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedStatus'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_checkbox_demo(
    recentlyCheckedLabel,
    recentlyCheckedDataIndex,
    recentlyCheckedStatus,
    recentlyCheckedRow,
):
    return json.dumps(
        dict(
            recentlyCheckedLabel=recentlyCheckedLabel,
            recentlyCheckedDataIndex=recentlyCheckedDataIndex,
            recentlyCheckedStatus=recentlyCheckedStatus,
            recentlyCheckedRow=recentlyCheckedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableRerender/demos/copyable_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'copyable示例',
                    'dataIndex': 'copyable示例',
                    'renderOptions': {'renderType': 'copyable'},
                }
            ],
            data=[{'copyable示例': '可复制内容'}],
            bordered=True,
            style={'width': 200},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Copyable Example',
                    'dataIndex': 'Copyable Example',
                    'renderOptions': {'renderType': 'copyable'},
                }
            ],
            data=[{'Copyable Example': 'Copyable Content'}],
            bordered=True,
            style={'width': 200},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'copyable示例',
            'dataIndex': 'copyable示例',
            'renderOptions': {'renderType': 'copyable'},
        }
    ],
    data=[{'copyable示例': '可复制内容'}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'Copyable Example',
            'dataIndex': 'Copyable Example',
            'renderOptions': {'renderType': 'copyable'},
        }
    ],
    data=[{'Copyable Example': 'Copyable Content'}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/corner_mark_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            size='small',
            columns=[
                {
                    'title': '角标模式',
                    'dataIndex': '角标模式',
                    'renderOptions': {'renderType': 'corner-mark'},
                }
            ],
            data=[
                {
                    'key': i,
                    '角标模式': {
                        'content': '角标模式',
                        'color': ['red', 'blue', 'green'][i],
                        'offsetX': -7.5,
                        'offsetY': -8.5,
                        'placement': 'top-left',
                        'hide': [False, True, False][i],
                    },
                }
                for i in range(3)
            ],
            bordered=True,
            style={'width': '200px'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            size='small',
            columns=[
                {
                    'title': 'Corner Mark Mode',
                    'dataIndex': 'Corner Mark Mode',
                    'renderOptions': {'renderType': 'corner-mark'},
                }
            ],
            data=[
                {
                    'key': i,
                    'Corner Mark Mode': {
                        'content': 'Corner Mark',
                        'color': ['red', 'blue', 'green'][i],
                        'offsetX': -7.5,
                        'offsetY': -8.5,
                        'placement': 'top-left',
                        'hide': [False, True, False][i],
                    },
                }
                for i in range(3)
            ],
            bordered=True,
            style={'width': '200px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    size='small',
    columns=[
        {
            'title': '角标模式',
            'dataIndex': '角标模式',
            'renderOptions': {'renderType': 'corner-mark'},
        }
    ],
    data=[
        {
            'key': i,
            '角标模式': {
                'content': '角标模式',
                'color': ['red', 'blue', 'green'][i],
                'offsetX': -7.5,
                'offsetY': -8.5,
                'placement': 'top-left',
                'hide': [False, True, False][i],
            },
        }
        for i in range(3)
    ],
    bordered=True,
    style={'width': '200px'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    size='small',
    columns=[
        {
            'title': 'Corner Mark Mode',
            'dataIndex': 'Corner Mark Mode',
            'renderOptions': {'renderType': 'corner-mark'},
        }
    ],
    data=[
        {
            'key': i,
            'Corner Mark Mode': {
                'content': 'Corner Mark',
                'color': ['red', 'blue', 'green'][i],
                'offsetX': -7.5,
                'offsetY': -8.5,
                'placement': 'top-left',
                'hide': [False, True, False][i],
            },
        }
        for i in range(3)
    ],
    bordered=True,
    style={'width': '200px'},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/custom_component_cell_render.py`
```python
import feffery_antd_components as fac
import feffery_markdown_components as fmc
import feffery_utils_components as fuc
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 中文演示
        demo_contents = fac.AntdTable(
            columns=[
                {'title': '自定义元素示例', 'dataIndex': '自定义元素示例'}
            ],
            data=[
                {
                    '自定义元素示例': html.Div(
                        fac.AntdText(
                            '示例内容' * 100, style={'textIndent': '2rem'}
                        ),
                        style={
                            'maxHeight': 50,
                            'overflowY': 'auto',
                            'textAlign': 'left',
                        },
                    )
                },
                {
                    '自定义元素示例': fmc.FefferyMarkdown(
                        markdownStr="""
```python
import numpy as np
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
```
"""
                    )
                },
                {
                    '自定义元素示例': fuc.FefferyQRCode(
                        value='FefferyQRCode示例'
                    )
                },
            ],
            bordered=True,
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # English demo
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Custom Component Example',
                    'dataIndex': 'Custom Component Example',
                }
            ],
            data=[
                {
                    'Custom Component Example': html.Div(
                        fac.AntdText(
                            'Example content' * 100,
                            style={'textIndent': '2rem'},
                        ),
                        style={
                            'maxHeight': 50,
                            'overflowY': 'auto',
                            'textAlign': 'left',
                        },
                    )
                },
                {
                    'Custom Component Example': fmc.FefferyMarkdown(
                        markdownStr="""
```python
import numpy as np
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
```
"""
                    )
                },
                {
                    'Custom Component Example': fuc.FefferyQRCode(
                        value='FefferyQRCode example'
                    )
                },
            ],
            bordered=True,
            style={'width': '100%'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdTable(
    columns=[{'title': '自定义元素示例', 'dataIndex': '自定义元素示例'}],
    data=[
        {
            '自定义元素示例': html.Div(
                fac.AntdText(
                    '示例内容' * 100, style={'textIndent': '2rem'}
                ),
                style={
                    'maxHeight': 50,
                    'overflowY': 'auto',
                    'textAlign': 'left',
                },
            )
        },
        {
            '自定义元素示例': fmc.FefferyMarkdown(
                markdownStr="""
```python
import numpy as np
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
```
"""
            )
        },
        {'自定义元素示例': fuc.FefferyQRCode(value='FefferyQRCode示例')},
    ],
    bordered=True,
    style={'width': '100%'},
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
fac.AntdTable(
    locale='en-us',
    columns=[{'title': 'Custom Component Example', 'dataIndex': 'Custom Component Example'}],
    data=[
        {
            'Custom Component Example': html.Div(
                fac.AntdText(
                    'Example content' * 100, style={'textIndent': '2rem'}
                ),
                style={
                    'maxHeight': 50,
                    'overflowY': 'auto',
                    'textAlign': 'left',
                },
            )
        },
        {
            'Custom Component Example': fmc.FefferyMarkdown(
                markdownStr="""
```python
import numpy as np
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
```
"""
            )
        },
        {'Custom Component Example': fuc.FefferyQRCode(value='FefferyQRCode example')},
    ],
    bordered=True,
    style={'width': '100%'},
)
'''
            }
        ]

```

### `views/AntdTableRerender/demos/custom_format_mode.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': '数值测试1',
                    'dataIndex': '数值测试1',
                    'width': '50%',
                    'renderOptions': {'renderType': 'custom-format'},
                },
                {
                    'title': '数值测试2',
                    'dataIndex': '数值测试2',
                    'width': '50%',
                    'renderOptions': {'renderType': 'custom-format'},
                },
            ],
            data=[
                {'数值测试1': np.random.rand(), '数值测试2': np.random.rand()}
                for i in range(10)
            ],
            sortOptions={'sortDataIndexes': ['数值测试1', '数值测试2']},
            bordered=True,
            customFormatFuncs={
                '数值测试1': '(x) => `${(x*100).toFixed(2)}%`',
                '数值测试2': '(x) => x <= 0.5 ? `低水平：${x.toFixed(2)}` : `高水平：${x.toFixed(2)}`',
            },
            style={'width': '500px'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Numeric Test 1',
                    'dataIndex': 'Numeric Test 1',
                    'width': '50%',
                    'renderOptions': {'renderType': 'custom-format'},
                },
                {
                    'title': 'Numeric Test 2',
                    'dataIndex': 'Numeric Test 2',
                    'width': '50%',
                    'renderOptions': {'renderType': 'custom-format'},
                },
            ],
            data=[
                {
                    'Numeric Test 1': np.random.rand(),
                    'Numeric Test 2': np.random.rand(),
                }
                for i in range(10)
            ],
            sortOptions={
                'sortDataIndexes': ['Numeric Test 1', 'Numeric Test 2']
            },
            bordered=True,
            customFormatFuncs={
                'Numeric Test 1': '(x) => `${(x*100).toFixed(2)}%`',
                'Numeric Test 2': '(x) => x <= 0.5 ? `Low Level: ${x.toFixed(2)}` : `High Level: ${x.toFixed(2)}`',
            },
            style={'width': '500px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': '数值测试1',
            'dataIndex': '数值测试1',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
        {
            'title': '数值测试2',
            'dataIndex': '数值测试2',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
    ],
    data=[
        {'数值测试1': np.random.rand(), '数值测试2': np.random.rand()}
        for i in range(10)
    ],
    sortOptions={'sortDataIndexes': ['数值测试1', '数值测试2']},
    bordered=True,
    customFormatFuncs={
        '数值测试1': '(x) => `${(x*100).toFixed(2)}%`',
        '数值测试2': '(x) => x <= 0.5 ? `低水平：${x.toFixed(2)}` : `高水平：${x.toFixed(2)}`',
    },
    style={'width': '500px'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'Numeric Test 1',
            'dataIndex': 'Numeric Test 1',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
        {
            'title': 'Numeric Test 2',
            'dataIndex': 'Numeric Test 2',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
    ],
    data=[
        {'Numeric Test 1': np.random.rand(), 'Numeric Test 2': np.random.rand()}
        for i in range(10)
    ],
    sortOptions={'sortDataIndexes': ['Numeric Test 1', 'Numeric Test 2']},
    bordered=True,
    customFormatFuncs={
        'Numeric Test 1': '(x) => `${(x*100).toFixed(2)}%`',
        'Numeric Test 2': '(x) => x <= 0.5 ? `Low Level: ${x.toFixed(2)}` : `High Level: ${x.toFixed(2)}`',
    },
    style={'width': '500px'},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/dropdown_links_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'dropdown-links示例1',
                    'dataIndex': 'dropdown-links示例1',
                    'renderOptions': {'renderType': 'dropdown-links'},
                    'width': '30%',
                },
                {
                    'title': 'dropdown-links示例2',
                    'dataIndex': 'dropdown-links示例2',
                    'renderOptions': {
                        'renderType': 'dropdown-links',
                        'dropdownProps': {'title': '更多'},
                    },
                    'width': '70%',
                },
            ],
            data=[
                {
                    'dropdown-links示例1': [
                        {
                            'title': f'image示例{i}.png',
                            'href': f'assets/imgs/image示例{i}.png',
                        }
                        for i in range(1, 8)
                    ],
                    'dropdown-links示例2': [
                        {
                            'title': f'image示例{i}.png',
                            'href': f'assets/imgs/image示例{i}.png',
                        }
                        for i in range(1, 8)
                    ],
                }
            ]
            * 3,
            bordered=True,
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Dropdown Links Example 1',
                    'dataIndex': 'Dropdown Links Example 1',
                    'renderOptions': {'renderType': 'dropdown-links'},
                    'width': '30%',
                },
                {
                    'title': 'Dropdown Links Example 2',
                    'dataIndex': 'Dropdown Links Example 2',
                    'renderOptions': {
                        'renderType': 'dropdown-links',
                        'dropdownProps': {'title': 'More'},
                    },
                    'width': '70%',
                },
            ],
            data=[
                {
                    'Dropdown Links Example 1': [
                        {
                            'title': f'image-example-{i}.png',
                            'href': f'assets/imgs/image-example-{i}.png',
                        }
                        for i in range(1, 8)
                    ],
                    'Dropdown Links Example 2': [
                        {
                            'title': f'image-example-{i}.png',
                            'href': f'assets/imgs/image-example-{i}.png',
                        }
                        for i in range(1, 8)
                    ],
                }
            ]
            * 3,
            bordered=True,
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'dropdown-links示例1',
            'dataIndex': 'dropdown-links示例1',
            'renderOptions': {'renderType': 'dropdown-links'},
            'width': '30%',
        },
        {
            'title': 'dropdown-links示例2',
            'dataIndex': 'dropdown-links示例2',
            'renderOptions': {
                'renderType': 'dropdown-links',
                'dropdownProps': {'title': '更多'},
            },
            'width': '70%',
        },
    ],
    data=[
        {
            'dropdown-links示例1': [
                {
                    'title': f'image示例{i}.png',
                    'href': f'assets/imgs/image示例{i}.png',
                }
                for i in range(1, 8)
            ],
            'dropdown-links示例2': [
                {
                    'title': f'image示例{i}.png',
                    'href': f'assets/imgs/image示例{i}.png',
                }
                for i in range(1, 8)
            ],
        }
    ]
    * 3,
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'Dropdown Links Example 1',
            'dataIndex': 'Dropdown Links Example 1',
            'renderOptions': {'renderType': 'dropdown-links'},
            'width': '30%',
        },
        {
            'title': 'Dropdown Links Example 2',
            'dataIndex': 'Dropdown Links Example 2',
            'renderOptions': {
                'renderType': 'dropdown-links',
                'dropdownProps': {'title': 'More'},
            },
            'width': '70%',
        },
    ],
    data=[
        {
            'Dropdown Links Example 1': [
                {
                    'title': f'image-example-{i}.png',
                    'href': f'assets/imgs/image-example-{i}.png',
                }
                for i in range(1, 8)
            ],
            'Dropdown Links Example 2': [
                {
                    'title': f'image-example-{i}.png',
                    'href': f'assets/imgs/image-example-{i}.png',
                }
                for i in range(1, 8)
            ],
        }
    ]
    * 3,
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/dropdown_mode_and_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-dropdown-demo',
                columns=[
                    {
                        'title': 'dropdown示例1',
                        'dataIndex': 'dropdown示例1',
                        'renderOptions': {'renderType': 'dropdown'},
                    },
                    {
                        'title': 'dropdown示例2',
                        'dataIndex': 'dropdown示例2',
                        'renderOptions': {
                            'renderType': 'dropdown',
                            'dropdownProps': {'title': '更多'},
                        },
                    },
                ],
                data=[
                    {
                        'dropdown示例1': [
                            {
                                'title': f'示例1-{i}-{j}',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 6)
                        ],
                        'dropdown示例2': [
                            {
                                'title': f'示例2-{i}-{j}',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 6)
                        ],
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-dropdown-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-dropdown-demo',
                locale='en-us',
                columns=[
                    {
                        'title': 'Dropdown Example 1',
                        'dataIndex': 'Dropdown Example 1',
                        'renderOptions': {'renderType': 'dropdown'},
                    },
                    {
                        'title': 'Dropdown Example 2',
                        'dataIndex': 'Dropdown Example 2',
                        'renderOptions': {
                            'renderType': 'dropdown',
                            'dropdownProps': {'title': 'More'},
                        },
                    },
                ],
                data=[
                    {
                        'Dropdown Example 1': [
                            {
                                'title': f'Example1-{i}-{j}',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 6)
                        ],
                        'Dropdown Example 2': [
                            {
                                'title': f'Example2-{i}-{j}',
                                'custom': 'balabalabalabala',
                            }
                            for j in range(1, 6)
                        ],
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-dropdown-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-rerender-dropdown-demo-output', 'children'),
    Input('table-rerender-dropdown-demo', 'nClicksDropdownItem'),
    [
        State(
            'table-rerender-dropdown-demo', 'recentlyClickedDropdownItemTitle'
        ),
        State(
            'table-rerender-dropdown-demo',
            'recentlyDropdownItemClickedDataIndex',
        ),
        State('table-rerender-dropdown-demo', 'recentlyDropdownItemClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_dropdown_demo(
    nClicksDropdownItem,
    recentlyClickedDropdownItemTitle,
    recentlyDropdownItemClickedDataIndex,
    recentlyDropdownItemClickedRow,
):
    return json.dumps(
        dict(
            nClicksDropdownItem=nClicksDropdownItem,
            recentlyClickedDropdownItemTitle=recentlyClickedDropdownItemTitle,
            recentlyDropdownItemClickedDataIndex=recentlyDropdownItemClickedDataIndex,
            recentlyDropdownItemClickedRow=recentlyDropdownItemClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-dropdown-demo',
        columns=[
            {
                'title': 'dropdown示例1',
                'dataIndex': 'dropdown示例1',
                'renderOptions': {'renderType': 'dropdown'},
            },
            {
                'title': 'dropdown示例2',
                'dataIndex': 'dropdown示例2',
                'renderOptions': {
                    'renderType': 'dropdown',
                    'dropdownProps': {'title': '更多'},
                },
            },
        ],
        data=[
            {
                'dropdown示例1': [
                    {
                        'title': f'示例1-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
                'dropdown示例2': [
                    {
                        'title': f'示例2-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-dropdown-demo-output'),
]

...

@app.callback(
    Output('table-rerender-dropdown-demo-output', 'children'),
    Input('table-rerender-dropdown-demo', 'nClicksDropdownItem'),
    [
        State(
            'table-rerender-dropdown-demo', 'recentlyClickedDropdownItemTitle'
        ),
        State(
            'table-rerender-dropdown-demo',
            'recentlyDropdownItemClickedDataIndex',
        ),
        State('table-rerender-dropdown-demo', 'recentlyDropdownItemClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_dropdown_demo(
    nClicksDropdownItem,
    recentlyClickedDropdownItemTitle,
    recentlyDropdownItemClickedDataIndex,
    recentlyDropdownItemClickedRow,
):
    return json.dumps(
        dict(
            nClicksDropdownItem=nClicksDropdownItem,
            recentlyClickedDropdownItemTitle=recentlyClickedDropdownItemTitle,
            recentlyDropdownItemClickedDataIndex=recentlyDropdownItemClickedDataIndex,
            recentlyDropdownItemClickedRow=recentlyDropdownItemClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-dropdown-demo',
        locale='en-us',
        columns=[
            {
                'title': 'Dropdown Example 1',
                'dataIndex': 'Dropdown Example 1',
                'renderOptions': {'renderType': 'dropdown'},
            },
            {
                'title': 'Dropdown Example 2',
                'dataIndex': 'Dropdown Example 2',
                'renderOptions': {
                    'renderType': 'dropdown',
                    'dropdownProps': {'title': 'More'},
                },
            },
        ],
        data=[
            {
                'Dropdown Example 1': [
                    {
                        'title': f'Example1-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
                'Dropdown Example 2': [
                    {
                        'title': f'Example2-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-dropdown-demo-output'),
]

...

@app.callback(
    Output('table-rerender-dropdown-demo-output', 'children'),
    Input('table-rerender-dropdown-demo', 'nClicksDropdownItem'),
    [
        State('table-rerender-dropdown-demo', 'recentlyClickedDropdownItemTitle'),
        State('table-rerender-dropdown-demo', 'recentlyDropdownItemClickedDataIndex'),
        State('table-rerender-dropdown-demo', 'recentlyDropdownItemClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_dropdown_demo(
    nClicksDropdownItem,
    recentlyClickedDropdownItemTitle,
    recentlyDropdownItemClickedDataIndex,
    recentlyDropdownItemClickedRow,
):
    return json.dumps(
        dict(
            nClicksDropdownItem=nClicksDropdownItem,
            recentlyClickedDropdownItemTitle=recentlyClickedDropdownItemTitle,
            recentlyDropdownItemClickedDataIndex=recentlyDropdownItemClickedDataIndex,
            recentlyDropdownItemClickedRow=recentlyDropdownItemClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableRerender/demos/ellipsis_copyable_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'ellipsis-copyable示例',
                    'dataIndex': 'ellipsis-copyable示例',
                    'renderOptions': {'renderType': 'ellipsis-copyable'},
                }
            ],
            data=[{'ellipsis-copyable示例': 'bala' * 10}],
            bordered=True,
            style={'width': 200},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'ellipsis-copyable Example',
                    'dataIndex': 'ellipsis-copyable Example',
                    'renderOptions': {'renderType': 'ellipsis-copyable'},
                }
            ],
            data=[{'ellipsis-copyable Example': 'bala' * 10}],
            bordered=True,
            style={'width': 200},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'ellipsis-copyable示例',
            'dataIndex': 'ellipsis-copyable示例',
            'renderOptions': {'renderType': 'ellipsis-copyable'},
        }
    ],
    data=[{'ellipsis-copyable示例': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'ellipsis-copyable Example',
            'dataIndex': 'ellipsis-copyable Example',
            'renderOptions': {'renderType': 'ellipsis-copyable'},
        }
    ],
    data=[{'ellipsis-copyable Example': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/ellipsis_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'ellipsis示例',
                    'dataIndex': 'ellipsis示例',
                    'renderOptions': {'renderType': 'ellipsis'},
                }
            ],
            data=[{'ellipsis示例': 'bala' * 10}],
            bordered=True,
            style={'width': 200},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'ellipsis Example',
                    'dataIndex': 'ellipsis Example',
                    'renderOptions': {'renderType': 'ellipsis'},
                }
            ],
            data=[{'ellipsis Example': 'bala' * 10}],
            bordered=True,
            style={'width': 200},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'ellipsis示例',
            'dataIndex': 'ellipsis示例',
            'renderOptions': {'renderType': 'ellipsis'},
        }
    ],
    data=[{'ellipsis示例': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'ellipsis Example',
            'dataIndex': 'ellipsis Example',
            'renderOptions': {'renderType': 'ellipsis'},
        }
    ],
    data=[{'ellipsis Example': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/image_avatar_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'image-avatar示例1',
                    'dataIndex': 'image-avatar示例1',
                    'renderOptions': {'renderType': 'image-avatar'},
                    'width': '50%',
                },
                {
                    'title': 'image-avatar示例2',
                    'dataIndex': 'image-avatar示例2',
                    'renderOptions': {'renderType': 'image-avatar'},
                    'width': '50%',
                },
            ],
            data=[
                {
                    'image-avatar示例1': {
                        'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg'
                    },
                    'image-avatar示例2': {
                        'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                        'shape': 'square',
                    },
                }
            ]
            * 3,
            bordered=True,
            style={'width': 300},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'image-avatar Example 1',
                    'dataIndex': 'image-avatar Example 1',
                    'renderOptions': {'renderType': 'image-avatar'},
                    'width': '50%',
                },
                {
                    'title': 'image-avatar Example 2',
                    'dataIndex': 'image-avatar Example 2',
                    'renderOptions': {'renderType': 'image-avatar'},
                    'width': '50%',
                },
            ],
            data=[
                {
                    'image-avatar Example 1': {
                        'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg'
                    },
                    'image-avatar Example 2': {
                        'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                        'shape': 'square',
                    },
                }
            ]
            * 3,
            bordered=True,
            style={'width': 300},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'image-avatar示例1',
            'dataIndex': 'image-avatar示例1',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
        {
            'title': 'image-avatar示例2',
            'dataIndex': 'image-avatar示例2',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
    ],
    data=[
        {
            'image-avatar示例1': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg'
            },
            'image-avatar示例2': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                'shape': 'square',
            },
        }
    ]
    * 3,
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'image-avatar Example 1',
            'dataIndex': 'image-avatar Example 1',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
        {
            'title': 'image-avatar Example 2',
            'dataIndex': 'image-avatar Example 2',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
    ],
    data=[
        {
            'image-avatar Example 1': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg'
            },
            'image-avatar Example 2': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                'shape': 'square',
            },
        }
    ]
    * 3,
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/image_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': '交互式图片',
                    'dataIndex': '交互式图片',
                    'renderOptions': {'renderType': 'image'},
                },
                {
                    'title': '静态图片',
                    'dataIndex': '静态图片',
                    'renderOptions': {'renderType': 'image'},
                },
            ],
            data=[
                {
                    '交互式图片': {
                        'src': '/assets/imgs/fac-logo.svg',
                        'height': '75px',
                    },
                    '静态图片': {
                        'src': '/assets/imgs/fac-logo.svg',
                        'height': '75px',
                        'preview': False,
                    },
                }
                for i in range(5)
            ],
            bordered=True,
            style={'width': '300px'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Interactive Image',
                    'dataIndex': 'Interactive Image',
                    'renderOptions': {'renderType': 'image'},
                },
                {
                    'title': 'Static Image',
                    'dataIndex': 'Static Image',
                    'renderOptions': {'renderType': 'image'},
                },
            ],
            data=[
                {
                    'Interactive Image': {
                        'src': '/assets/imgs/fac-logo.svg',
                        'height': '75px',
                    },
                    'Static Image': {
                        'src': '/assets/imgs/fac-logo.svg',
                        'height': '75px',
                        'preview': False,
                    },
                }
                for i in range(5)
            ],
            bordered=True,
            style={'width': '300px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': '交互式图片',
            'dataIndex': '交互式图片',
            'renderOptions': {'renderType': 'image'},
        },
        {
            'title': '静态图片',
            'dataIndex': '静态图片',
            'renderOptions': {'renderType': 'image'},
        },
    ],
    data=[
        {
            '交互式图片': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
            },
            '静态图片': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
                'preview': False,
            },
        }
        for i in range(5)
    ],
    bordered=True,
    style={'width': '300px'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'Interactive Image',
            'dataIndex': 'Interactive Image',
            'renderOptions': {'renderType': 'image'},
        },
        {
            'title': 'Static Image',
            'dataIndex': 'Static Image',
            'renderOptions': {'renderType': 'image'},
        },
    ],
    data=[
        {
            'Interactive Image': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
            },
            'Static Image': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
                'preview': False,
            },
        }
        for i in range(5)
    ],
    bordered=True,
    style={'width': '300px'},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/link_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'link示例1',
                    'dataIndex': 'link示例1',
                    'renderOptions': {'renderType': 'link'},
                    'width': '50%',
                },
                {
                    'title': 'link示例2',
                    'dataIndex': 'link示例2',
                    'renderOptions': {
                        'renderType': 'link',
                        'renderLinkText': '示例链接',
                    },
                    'width': '50%',
                },
            ],
            data=[
                {
                    'link示例1': {'content': f'{content}仓库', 'href': href},
                    'link示例2': {'href': '/AntdTable-rerender'},
                }
                for href, content in zip(
                    [
                        'https://github.com/CNFeffery/feffery-antd-components',
                        'https://github.com/CNFeffery/feffery-utils-components',
                        'https://github.com/CNFeffery/feffery-antd-charts',
                        'https://github.com/CNFeffery/feffery-markdown-components',
                        'https://github.com/CNFeffery/feffery-leaflet-components',
                    ],
                    ['fac', 'fuc', 'fact', 'fmc', 'flc'],
                )
            ],
            bordered=True,
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'link Example 1',
                    'dataIndex': 'link Example 1',
                    'renderOptions': {'renderType': 'link'},
                    'width': '50%',
                },
                {
                    'title': 'link Example 2',
                    'dataIndex': 'link Example 2',
                    'renderOptions': {
                        'renderType': 'link',
                        'renderLinkText': 'Example Link',
                    },
                    'width': '50%',
                },
            ],
            data=[
                {
                    'link Example 1': {
                        'content': f'{content} repo',
                        'href': href,
                    },
                    'link Example 2': {'href': '/AntdTable-rerender'},
                }
                for href, content in zip(
                    [
                        'https://github.com/CNFeffery/feffery-antd-components',
                        'https://github.com/CNFeffery/feffery-utils-components',
                        'https://github.com/CNFeffery/feffery-antd-charts',
                        'https://github.com/CNFeffery/feffery-markdown-components',
                        'https://github.com/CNFeffery/feffery-leaflet-components',
                    ],
                    ['fac', 'fuc', 'fact', 'fmc', 'flc'],
                )
            ],
            bordered=True,
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'link示例1',
            'dataIndex': 'link示例1',
            'renderOptions': {'renderType': 'link'},
            'width': '50%',
        },
        {
            'title': 'link示例2',
            'dataIndex': 'link示例2',
            'renderOptions': {
                'renderType': 'link',
                'renderLinkText': '示例链接',
            },
            'width': '50%',
        },
    ],
    data=[
        {
            'link示例1': {'content': f'{content}仓库', 'href': href},
            'link示例2': {'href': '/AntdTable-rerender'},
        }
        for href, content in zip(
            [
                'https://github.com/CNFeffery/feffery-antd-components',
                'https://github.com/CNFeffery/feffery-utils-components',
                'https://github.com/CNFeffery/feffery-antd-charts',
                'https://github.com/CNFeffery/feffery-markdown-components',
                'https://github.com/CNFeffery/feffery-leaflet-components',
            ],
            ['fac', 'fuc', 'fact', 'fmc', 'flc'],
        )
    ],
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale='en-us',
    columns=[
        {
            'title': 'link Example 1',
            'dataIndex': 'link Example 1',
            'renderOptions': {'renderType': 'link'},
            'width': '50%',
        },
        {
            'title': 'link Example 2',
            'dataIndex': 'link Example 2',
            'renderOptions': {
                'renderType': 'link',
                'renderLinkText': 'Example Link',
            },
            'width': '50%',
        },
    ],
    data=[
        {
            'link Example 1': {'content': f'{content} repo', 'href': href},
            'link Example 2': {'href': '/AntdTable-rerender'},
        }
        for href, content in zip(
            [
                'https://github.com/CNFeffery/feffery-antd-components',
                'https://github.com/CNFeffery/feffery-utils-components',
                'https://github.com/CNFeffery/feffery-antd-charts',
                'https://github.com/CNFeffery/feffery-markdown-components',
                'https://github.com/CNFeffery/feffery-leaflet-components',
            ],
            ['fac', 'fuc', 'fact', 'fmc', 'flc'],
        )
    ],
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_area_mode.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-area示例1',
                    'dataIndex': 'mini-area示例1',
                    'renderOptions': {'renderType': 'mini-area'},
                },
                {
                    'title': 'mini-area示例2',
                    'dataIndex': 'mini-area示例2',
                    'renderOptions': {
                        'renderType': 'mini-area',
                        'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': '自定义颜色示例',
                    'dataIndex': '自定义颜色示例',
                    'renderOptions': {
                        'renderType': 'mini-area',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-area示例1': [np.random.rand() for i in range(25)],
                    'mini-area示例2': [np.random.rand() for i in range(25)],
                    '自定义颜色示例': [np.random.rand() for i in range(25)],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-area Example 1',
                    'dataIndex': 'mini-area Example 1',
                    'renderOptions': {'renderType': 'mini-area'},
                },
                {
                    'title': 'mini-area Example 2',
                    'dataIndex': 'mini-area Example 2',
                    'renderOptions': {
                        'renderType': 'mini-area',
                        'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': 'Custom Color Example',
                    'dataIndex': 'Custom Color Example',
                    'renderOptions': {
                        'renderType': 'mini-area',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-area Example 1': [
                        np.random.rand() for i in range(25)
                    ],
                    'mini-area Example 2': [
                        np.random.rand() for i in range(25)
                    ],
                    'Custom Color Example': [
                        np.random.rand() for i in range(25)
                    ],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdTable(
    columns=[
        {
            'title': 'mini-area示例1',
            'dataIndex': 'mini-area示例1',
            'renderOptions': {'renderType': 'mini-area'},
        },
        {
            'title': 'mini-area示例2',
            'dataIndex': 'mini-area示例2',
            'renderOptions': {
                'renderType': 'mini-area',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-area',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-area示例1': [np.random.rand() for i in range(25)],
            'mini-area示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-area Example 1',
            'dataIndex': 'mini-area Example 1',
            'renderOptions': {'renderType': 'mini-area'},
        },
        {
            'title': 'mini-area Example 2',
            'dataIndex': 'mini-area Example 2',
            'renderOptions': {
                'renderType': 'mini-area',
                'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': 'Custom Color Example',
            'dataIndex': 'Custom Color Example',
            'renderOptions': {
                'renderType': 'mini-area',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-area Example 1': [np.random.rand() for i in range(25)],
            'mini-area Example 2': [np.random.rand() for i in range(25)],
            'Custom Color Example': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

```

### `views/AntdTableRerender/demos/mini_bar_mode.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-bar示例1',
                    'dataIndex': 'mini-bar示例1',
                    'renderOptions': {'renderType': 'mini-bar'},
                },
                {
                    'title': 'mini-bar示例2',
                    'dataIndex': 'mini-bar示例2',
                    'renderOptions': {
                        'renderType': 'mini-bar',
                        'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': '自定义颜色示例',
                    'dataIndex': '自定义颜色示例',
                    'renderOptions': {
                        'renderType': 'mini-bar',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-bar示例1': [np.random.rand() for i in range(25)],
                    'mini-bar示例2': [np.random.rand() for i in range(25)],
                    '自定义颜色示例': [np.random.rand() for i in range(25)],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-bar Example 1',
                    'dataIndex': 'mini-bar Example 1',
                    'renderOptions': {'renderType': 'mini-bar'},
                },
                {
                    'title': 'mini-bar Example 2',
                    'dataIndex': 'mini-bar Example 2',
                    'renderOptions': {
                        'renderType': 'mini-bar',
                        'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': 'Custom Color Example',
                    'dataIndex': 'Custom Color Example',
                    'renderOptions': {
                        'renderType': 'mini-bar',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-bar Example 1': [np.random.rand() for i in range(25)],
                    'mini-bar Example 2': [np.random.rand() for i in range(25)],
                    'Custom Color Example': [
                        np.random.rand() for i in range(25)
                    ],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdTable(
    columns=[
        {
            'title': 'mini-bar示例1',
            'dataIndex': 'mini-bar示例1',
            'renderOptions': {'renderType': 'mini-bar'},
        },
        {
            'title': 'mini-bar示例2',
            'dataIndex': 'mini-bar示例2',
            'renderOptions': {
                'renderType': 'mini-bar',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-bar',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-bar示例1': [np.random.rand() for i in range(25)],
            'mini-bar示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-bar Example 1',
            'dataIndex': 'mini-bar Example 1',
            'renderOptions': {'renderType': 'mini-bar'},
        },
        {
            'title': 'mini-bar Example 2',
            'dataIndex': 'mini-bar Example 2',
            'renderOptions': {
                'renderType': 'mini-bar',
                'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': 'Custom Color Example',
            'dataIndex': 'Custom Color Example',
            'renderOptions': {
                'renderType': 'mini-bar',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-bar Example 1': [np.random.rand() for i in range(25)],
            'mini-bar Example 2': [np.random.rand() for i in range(25)],
            'Custom Color Example': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

```

### `views/AntdTableRerender/demos/mini_line_mode.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-line示例1',
                    'dataIndex': 'mini-line示例1',
                    'renderOptions': {'renderType': 'mini-line'},
                },
                {
                    'title': 'mini-line示例2',
                    'dataIndex': 'mini-line示例2',
                    'renderOptions': {
                        'renderType': 'mini-line',
                        'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': '自定义颜色示例',
                    'dataIndex': '自定义颜色示例',
                    'renderOptions': {
                        'renderType': 'mini-line',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-line示例1': [np.random.rand() for i in range(25)],
                    'mini-line示例2': [np.random.rand() for i in range(25)],
                    '自定义颜色示例': [np.random.rand() for i in range(25)],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-line Example 1',
                    'dataIndex': 'mini-line Example 1',
                    'renderOptions': {'renderType': 'mini-line'},
                },
                {
                    'title': 'mini-line Example 2',
                    'dataIndex': 'mini-line Example 2',
                    'renderOptions': {
                        'renderType': 'mini-line',
                        'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
                    },
                },
                {
                    'title': 'Custom Color Example',
                    'dataIndex': 'Custom Color Example',
                    'renderOptions': {
                        'renderType': 'mini-line',
                        'miniChartColor': '#ff7875',
                    },
                },
            ],
            data=[
                {
                    'mini-line Example 1': [
                        np.random.rand() for i in range(25)
                    ],
                    'mini-line Example 2': [
                        np.random.rand() for i in range(25)
                    ],
                    'Custom Color Example': [
                        np.random.rand() for i in range(25)
                    ],
                }
            ]
            * 3,
            bordered=True,
            tableLayout='fixed',
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdTable(
    columns=[
        {
            'title': 'mini-line示例1',
            'dataIndex': 'mini-line示例1',
            'renderOptions': {'renderType': 'mini-line'},
        },
        {
            'title': 'mini-line示例2',
            'dataIndex': 'mini-line示例2',
            'renderOptions': {
                'renderType': 'mini-line',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-line',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-line示例1': [np.random.rand() for i in range(25)],
            'mini-line示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-line Example 1',
            'dataIndex': 'mini-line Example 1',
            'renderOptions': {'renderType': 'mini-line'},
        },
        {
            'title': 'mini-line Example 2',
            'dataIndex': 'mini-line Example 2',
            'renderOptions': {
                'renderType': 'mini-line',
                'tooltipCustomContent': """(x, data) => `Value: ${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': 'Custom Color Example',
            'dataIndex': 'Custom Color Example',
            'renderOptions': {
                'renderType': 'mini-line',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-line Example 1': [np.random.rand() for i in range(25)],
            'mini-line Example 2': [np.random.rand() for i in range(25)],
            'Custom Color Example': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
'''
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_color.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例1',
                    'dataIndex': 'mini-progress示例1',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressColor': '#f08c00',
                    },
                },
                {
                    'title': 'mini-progress示例2',
                    'dataIndex': 'mini-progress示例2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressColor': {
                            'from': '#4c83ff',
                            'to': '#2afadf',
                        },
                    },
                },
            ],
            data=[
                {'mini-progress示例1': x, 'mini-progress示例2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example 1',
                    'dataIndex': 'mini-progress Example 1',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressColor': '#f08c00',
                    },
                },
                {
                    'title': 'mini-progress Example 2',
                    'dataIndex': 'mini-progress Example 2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressColor': {
                            'from': '#4c83ff',
                            'to': '#2afadf',
                        },
                    },
                },
            ],
            data=[
                {'mini-progress Example 1': x, 'mini-progress Example 2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': '#f08c00',
            },
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': {
                    'from': '#4c83ff',
                    'to': '#2afadf',
                },
            },
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example 1',
            'dataIndex': 'mini-progress Example 1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': '#f08c00',
            },
        },
        {
            'title': 'mini-progress Example 2',
            'dataIndex': 'mini-progress Example 2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': {
                    'from': '#4c83ff',
                    'to': '#2afadf',
                },
            },
        },
    ],
    data=[
        {'mini-progress Example 1': x, 'mini-progress Example 2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例1',
                    'dataIndex': 'mini-progress示例1',
                    'renderOptions': {'renderType': 'mini-progress'},
                    'width': '50%',
                },
                {
                    'title': 'mini-progress示例2',
                    'dataIndex': 'mini-progress示例2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressOneHundredPercentColor': '#f08c00',
                    },
                    'width': '50%',
                },
            ],
            data=[
                {'mini-progress示例1': x, 'mini-progress示例2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            style={'width': 300},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example 1',
                    'dataIndex': 'mini-progress Example 1',
                    'renderOptions': {'renderType': 'mini-progress'},
                    'width': '50%',
                },
                {
                    'title': 'mini-progress Example 2',
                    'dataIndex': 'mini-progress Example 2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressOneHundredPercentColor': '#f08c00',
                    },
                    'width': '50%',
                },
            ],
            data=[
                {'mini-progress Example 1': x, 'mini-progress Example 2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            style={'width': 300},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {'renderType': 'mini-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressOneHundredPercentColor': '#f08c00',
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example 1',
            'dataIndex': 'mini-progress Example 1',
            'renderOptions': {'renderType': 'mini-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-progress Example 2',
            'dataIndex': 'mini-progress Example 2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressOneHundredPercentColor': '#f08c00',
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-progress Example 1': x, 'mini-progress Example 2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_percent_position.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        'align:',
                        fac.AntdRadioGroup(
                            id='table-mini-progress-percent-position-demo-align',
                            options=['start', 'center', 'end'],
                            value='end',
                        ),
                    ]
                ),
                fac.AntdSpace(
                    [
                        'type:',
                        fac.AntdRadioGroup(
                            id='table-mini-progress-percent-position-demo-type',
                            options=['inner', 'outer'],
                            value='inner',
                        ),
                    ]
                ),
                fac.AntdTable(
                    id='table-mini-progress-percent-position-demo',
                    columns=[
                        {
                            'dataIndex': 'mini-progress示例',
                            'title': 'mini-progress示例',
                            'renderOptions': {
                                'renderType': 'mini-progress',
                                'progressShowPercent': True,
                                'progressPercentPosition': {
                                    'align': 'end',
                                    'type': 'inner',
                                },
                            },
                        },
                    ],
                    data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
                    bordered=True,
                ),
            ],
            direction='vertical',
            size='small',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        'align:',
                        fac.AntdRadioGroup(
                            id='table-mini-progress-percent-position-demo-align',
                            options=['start', 'center', 'end'],
                            value='end',
                        ),
                    ]
                ),
                fac.AntdSpace(
                    [
                        'type:',
                        fac.AntdRadioGroup(
                            id='table-mini-progress-percent-position-demo-type',
                            options=['inner', 'outer'],
                            value='inner',
                        ),
                    ]
                ),
                fac.AntdTable(
                    id='table-mini-progress-percent-position-demo',
                    locale='en-us',
                    columns=[
                        {
                            'dataIndex': 'mini-progress Example',
                            'title': 'mini-progress Example',
                            'renderOptions': {
                                'renderType': 'mini-progress',
                                'progressShowPercent': True,
                                'progressPercentPosition': {
                                    'align': 'end',
                                    'type': 'inner',
                                },
                            },
                        },
                    ],
                    data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
                    bordered=True,
                ),
            ],
            direction='vertical',
            size='small',
            style={'width': '100%'},
        )

    return demo_contents


app.clientside_callback(
    """
(align, type) => {
    return [
        {
            'dataIndex': 'mini-progress示例',
            'title': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': true,
                'progressPercentPosition': {
                    'align': align,
                    'type': type,
                },
            },
        },
    ];
}
""",
    Output('table-mini-progress-percent-position-demo', 'columns'),
    [
        Input('table-mini-progress-percent-position-demo-align', 'value'),
        Input('table-mini-progress-percent-position-demo-type', 'value'),
    ],
    prevent_initial_call=True,
)


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                'align:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-align',
                    options=['start', 'center', 'end'],
                    value='end',
                ),
            ]
        ),
        fac.AntdSpace(
            [
                'type:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-type',
                    options=['inner', 'outer'],
                    value='inner',
                ),
            ]
        ),
        fac.AntdTable(
            id='table-mini-progress-percent-position-demo',
            columns=[
                {
                    'dataIndex': 'mini-progress示例',
                    'title': 'mini-progress示例',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressPercentPosition': {
                            'align': 'end',
                            'type': 'inner',
                        },
                    },
                },
            ],
            data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
            bordered=True,
        ),
    ],
    direction='vertical',
    size='small',
    style={'width': '100%'},
)

...

app.clientside_callback(
    \"""
(align, type) => {
    return [
        {
            'dataIndex': 'mini-progress示例',
            'title': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': true,
                'progressPercentPosition': {
                    'align': align,
                    'type': type,
                },
            },
        },
    ];
}
\""",
    Output('table-mini-progress-percent-position-demo', 'columns'),
    [
        Input('table-mini-progress-percent-position-demo-align', 'value'),
        Input('table-mini-progress-percent-position-demo-type', 'value'),
    ],
    prevent_initial_call=True,
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
        fac.AntdSpace(
            [
                'align:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-align',
                    options=['start', 'center', 'end'],
                    value='end',
                ),
            ]
        ),
        fac.AntdSpace(
            [
                'type:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-type',
                    options=['inner', 'outer'],
                    value='inner',
                ),
            ]
        ),
        fac.AntdTable(
            id='table-mini-progress-percent-position-demo',
            locale="en-us",
            columns=[
                {
                    'dataIndex': 'mini-progress Example',
                    'title': 'mini-progress Example',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressPercentPosition': {
                            'align': 'end',
                            'type': 'inner',
                        },
                    },
                },
            ],
            data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
            bordered=True,
        ),
    ],
    direction='vertical',
    size='small',
    style={'width': '100%'},
)

...

app.clientside_callback(
    \"""
(align, type) => {
    return [
        {
            'dataIndex': 'mini-progress Example',
            'title': 'mini-progress Example',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': true,
                'progressPercentPosition': {
                    'align': align,
                    'type': type,
                },
            },
        },
    ];
}
\""",
    Output('table-mini-progress-percent-position-demo', 'columns'),
    [
        Input('table-mini-progress-percent-position-demo-align', 'value'),
        Input('table-mini-progress-percent-position-demo-type', 'value'),
    ],
    prevent_initial_call=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_percent_precision.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例',
                    'dataIndex': 'mini-progress示例',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressPercentPrecision': 1,
                    },
                }
            ],
            data=[{'mini-progress示例': x} for x in [0, 0.5678, 0.6789, 1]],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example',
                    'dataIndex': 'mini-progress Example',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressPercentPrecision': 1,
                    },
                }
            ],
            data=[{'mini-progress Example': x} for x in [0, 0.5678, 0.6789, 1]],
            bordered=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressPercentPrecision': 1,
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.5678, 0.6789, 1]],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example',
            'dataIndex': 'mini-progress Example',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressPercentPrecision': 1,
            },
        }
    ],
    data=[{'mini-progress Example': x} for x in [0, 0.5678, 0.6789, 1]],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_round.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例',
                    'dataIndex': 'mini-progress示例',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressStrokeLinecap': 'round',
                    },
                }
            ],
            data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example',
                    'dataIndex': 'mini-progress Example',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressStrokeLinecap': 'round',
                    },
                }
            ],
            data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
            bordered=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressStrokeLinecap': 'round',
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example',
            'dataIndex': 'mini-progress Example',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressStrokeLinecap': 'round',
            },
        }
    ],
    data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_show_percent.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例',
                    'dataIndex': 'mini-progress示例',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                    },
                }
            ],
            data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example',
                    'dataIndex': 'mini-progress Example',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                    },
                }
            ],
            data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
            bordered=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example',
            'dataIndex': 'mini-progress Example',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
            },
        }
    ],
    data=[{'mini-progress Example': x} for x in [0, 0.66, 1]],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_progress_size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-progress示例1',
                    'dataIndex': 'mini-progress示例1',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressSize': 24,
                    },
                },
                {
                    'title': 'mini-progress示例2',
                    'dataIndex': 'mini-progress示例2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressStrokeLinecap': 'round',
                        'progressSize': 24,
                    },
                },
            ],
            data=[
                {'mini-progress示例1': x, 'mini-progress示例2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-progress Example 1',
                    'dataIndex': 'mini-progress Example 1',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressSize': 24,
                    },
                },
                {
                    'title': 'mini-progress Example 2',
                    'dataIndex': 'mini-progress Example 2',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressStrokeLinecap': 'round',
                        'progressSize': 24,
                    },
                },
            ],
            data=[
                {'mini-progress Example 1': x, 'mini-progress Example 2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            tableLayout='fixed',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressSize': 24,
            },
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressStrokeLinecap': 'round',
                'progressSize': 24,
            },
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-progress Example 1',
            'dataIndex': 'mini-progress Example 1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressSize': 24,
            },
        },
        {
            'title': 'mini-progress Example 2',
            'dataIndex': 'mini-progress Example 2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressStrokeLinecap': 'round',
                'progressSize': 24,
            },
        },
    ],
    data=[
        {'mini-progress Example 1': x, 'mini-progress Example 2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/mini_ring_progress_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'mini-ring-progress示例1',
                    'dataIndex': 'mini-ring-progress示例1',
                    'renderOptions': {'renderType': 'mini-ring-progress'},
                    'width': '50%',
                },
                {
                    'title': 'mini-ring-progress示例2',
                    'dataIndex': 'mini-ring-progress示例2',
                    'renderOptions': {
                        'renderType': 'mini-ring-progress',
                        'progressOneHundredPercentColor': '#f08c00',
                        'ringProgressFontSize': 8,
                    },
                    'width': '50%',
                },
            ],
            data=[
                {'mini-ring-progress示例1': x, 'mini-ring-progress示例2': x}
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            miniChartHeight=75,
            style={'width': 300},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'mini-ring-progress Example 1',
                    'dataIndex': 'mini-ring-progress Example 1',
                    'renderOptions': {'renderType': 'mini-ring-progress'},
                    'width': '50%',
                },
                {
                    'title': 'mini-ring-progress Example 2',
                    'dataIndex': 'mini-ring-progress Example 2',
                    'renderOptions': {
                        'renderType': 'mini-ring-progress',
                        'progressOneHundredPercentColor': '#f08c00',
                        'ringProgressFontSize': 8,
                    },
                    'width': '50%',
                },
            ],
            data=[
                {
                    'mini-ring-progress Example 1': x,
                    'mini-ring-progress Example 2': x,
                }
                for x in [0, 0.66, 1]
            ],
            bordered=True,
            miniChartHeight=75,
            style={'width': 300},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'mini-ring-progress示例1',
            'dataIndex': 'mini-ring-progress示例1',
            'renderOptions': {'renderType': 'mini-ring-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-ring-progress示例2',
            'dataIndex': 'mini-ring-progress示例2',
            'renderOptions': {
                'renderType': 'mini-ring-progress',
                'progressOneHundredPercentColor': '#f08c00',
                'ringProgressFontSize': 8,
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-ring-progress示例1': x, 'mini-ring-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    miniChartHeight=75,
    style={'width': 300},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'mini-ring-progress Example 1',
            'dataIndex': 'mini-ring-progress Example 1',
            'renderOptions': {'renderType': 'mini-ring-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-ring-progress Example 2',
            'dataIndex': 'mini-ring-progress Example 2',
            'renderOptions': {
                'renderType': 'mini-ring-progress',
                'progressOneHundredPercentColor': '#f08c00',
                'ringProgressFontSize': 8,
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-ring-progress Example 1': x, 'mini-ring-progress Example 2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    miniChartHeight=75,
    style={'width': 300},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/row_merge_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'row-merge示例1',
                    'dataIndex': 'row-merge示例1',
                    'renderOptions': {'renderType': 'row-merge'},
                    'width': '50%',
                },
                {
                    'title': 'row-merge示例2',
                    'dataIndex': 'row-merge示例2',
                    'renderOptions': {'renderType': 'row-merge'},
                    'width': '50%',
                },
            ],
            data=[
                {
                    'row-merge示例1': {'content': '示例1-1', 'rowSpan': 1},
                    'row-merge示例2': {'content': '示例2-1', 'rowSpan': 2},
                },
                {
                    'row-merge示例1': {'content': '示例1-2', 'rowSpan': 2},
                    'row-merge示例2': {'rowSpan': 0},
                },
                {
                    'row-merge示例1': {'rowSpan': 0},
                    'row-merge示例2': {'content': '示例2-2', 'rowSpan': 1},
                },
            ],
            bordered=True,
            style={'width': 300},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'row-merge Example 1',
                    'dataIndex': 'row-merge Example 1',
                    'renderOptions': {'renderType': 'row-merge'},
                    'width': '50%',
                },
                {
                    'title': 'row-merge Example 2',
                    'dataIndex': 'row-merge Example 2',
                    'renderOptions': {'renderType': 'row-merge'},
                    'width': '50%',
                },
            ],
            data=[
                {
                    'row-merge Example 1': {
                        'content': 'Example 1-1',
                        'rowSpan': 1,
                    },
                    'row-merge Example 2': {
                        'content': 'Example 2-1',
                        'rowSpan': 2,
                    },
                },
                {
                    'row-merge Example 1': {
                        'content': 'Example 1-2',
                        'rowSpan': 2,
                    },
                    'row-merge Example 2': {'rowSpan': 0},
                },
                {
                    'row-merge Example 1': {'rowSpan': 0},
                    'row-merge Example 2': {
                        'content': 'Example 2-2',
                        'rowSpan': 1,
                    },
                },
            ],
            bordered=True,
            style={'width': 300},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'row-merge示例1',
            'dataIndex': 'row-merge示例1',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
        {
            'title': 'row-merge示例2',
            'dataIndex': 'row-merge示例2',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
    ],
    data=[
        {
            'row-merge示例1': {'content': '示例1-1', 'rowSpan': 1},
            'row-merge示例2': {'content': '示例2-1', 'rowSpan': 2},
        },
        {
            'row-merge示例1': {'content': '示例1-2', 'rowSpan': 2},
            'row-merge示例2': {'rowSpan': 0},
        },
        {
            'row-merge示例1': {'rowSpan': 0},
            'row-merge示例2': {'content': '示例2-2', 'rowSpan': 1},
        },
    ],
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'row-merge Example 1',
            'dataIndex': 'row-merge Example 1',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
        {
            'title': 'row-merge Example 2',
            'dataIndex': 'row-merge Example 2',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
    ],
    data=[
        {
            'row-merge Example 1': {'content': 'Example 1-1', 'rowSpan': 1},
            'row-merge Example 2': {'content': 'Example 2-1', 'rowSpan': 2},
        },
        {
            'row-merge Example 1': {'content': 'Example 1-2', 'rowSpan': 2},
            'row-merge Example 2': {'rowSpan': 0},
        },
        {
            'row-merge Example 1': {'rowSpan': 0},
            'row-merge Example 2': {'content': 'Example 2-2', 'rowSpan': 1},
        },
    ],
    bordered=True,
    style={'width': 300},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/select_mode_and_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-select-demo',
                columns=[
                    {
                        'title': 'select示例1',
                        'dataIndex': 'select示例1',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                    {
                        'title': 'select示例2',
                        'dataIndex': 'select示例2',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                    {
                        'title': 'select示例3',
                        'dataIndex': 'select示例3',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                ],
                data=[
                    {
                        'select示例1': {
                            'options': [
                                {'label': f'选项{j}', 'value': f'选项{j}'}
                                for j in range(5)
                            ],
                            'allowClear': True,
                            'placeholder': '请选择',
                        },
                        'select示例2': {
                            'options': [
                                {'label': f'选项{j}', 'value': f'选项{j}'}
                                for j in range(5)
                            ],
                            'mode': 'multiple',
                            'allowClear': True,
                            'placeholder': '请选择',
                        },
                        'select示例3': {
                            'options': [
                                {'label': f'选项{j}', 'value': f'选项{j}'}
                                for j in range(5)
                            ],
                            'mode': 'tags',
                            'allowClear': True,
                            'placeholder': '请选择',
                        },
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 600},
            ),
            html.Pre(id='table-rerender-select-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-select-demo',
                locale='en-us',
                columns=[
                    {
                        'title': 'select Example 1',
                        'dataIndex': 'select Example 1',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                    {
                        'title': 'select Example 2',
                        'dataIndex': 'select Example 2',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                    {
                        'title': 'select Example 3',
                        'dataIndex': 'select Example 3',
                        'renderOptions': {'renderType': 'select'},
                        'width': 'calc(100% / 3)',
                    },
                ],
                data=[
                    {
                        'select Example 1': {
                            'options': [
                                {'label': f'Option {j}', 'value': f'Option {j}'}
                                for j in range(5)
                            ],
                            'allowClear': True,
                            'placeholder': 'Please select',
                        },
                        'select Example 2': {
                            'options': [
                                {'label': f'Option {j}', 'value': f'Option {j}'}
                                for j in range(5)
                            ],
                            'mode': 'multiple',
                            'allowClear': True,
                            'placeholder': 'Please select',
                        },
                        'select Example 3': {
                            'options': [
                                {'label': f'Option {j}', 'value': f'Option {j}'}
                                for j in range(5)
                            ],
                            'mode': 'tags',
                            'allowClear': True,
                            'placeholder': 'Please select',
                        },
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 600},
            ),
            html.Pre(id='table-rerender-select-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-rerender-select-demo-output', 'children'),
    [
        Input('table-rerender-select-demo', 'recentlySelectRow'),
        Input('table-rerender-select-demo', 'recentlySelectDataIndex'),
        Input('table-rerender-select-demo', 'recentlySelectValue'),
    ],
    prevent_initial_call=True,
)
def table_rerender_select_demo(
    recentlySelectRow, recentlySelectDataIndex, recentlySelectValue
):
    return json.dumps(
        dict(
            recentlySelectRow=recentlySelectRow,
            recentlySelectDataIndex=recentlySelectDataIndex,
            recentlySelectValue=recentlySelectValue,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-select-demo',
        columns=[
            {
                'title': 'select示例1',
                'dataIndex': 'select示例1',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select示例2',
                'dataIndex': 'select示例2',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select示例3',
                'dataIndex': 'select示例3',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
        ],
        data=[
            {
                'select示例1': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'allowClear': True,
                    'placeholder': '请选择',
                },
                'select示例2': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'mode': 'multiple',
                    'allowClear': True,
                    'placeholder': '请选择',
                },
                'select示例3': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'mode': 'tags',
                    'allowClear': True,
                    'placeholder': '请选择',
                },
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 600},
    ),
    html.Pre(id='table-rerender-select-demo-output'),
]

...

@app.callback(
    Output('table-rerender-select-demo-output', 'children'),
    [
        Input('table-rerender-select-demo', 'recentlySelectRow'),
        Input('table-rerender-select-demo', 'recentlySelectDataIndex'),
        Input('table-rerender-select-demo', 'recentlySelectValue'),
    ],
    prevent_initial_call=True,
)
def table_rerender_select_demo(
    recentlySelectRow, recentlySelectDataIndex, recentlySelectValue
):
    return json.dumps(
        dict(
            recentlySelectRow=recentlySelectRow,
            recentlySelectDataIndex=recentlySelectDataIndex,
            recentlySelectValue=recentlySelectValue,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-select-demo',
        locale="en-us",
        columns=[
            {
                'title': 'select Example 1',
                'dataIndex': 'select Example 1',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select Example 2',
                'dataIndex': 'select Example 2',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select Example 3',
                'dataIndex': 'select Example 3',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
        ],
        data=[
            {
                'select Example 1': {
                    'options': [
                        {'label': f'Option {j}', 'value': f'Option {j}'}
                        for j in range(5)
                    ],
                    'allowClear': True,
                    'placeholder': 'Please select',
                },
                'select Example 2': {
                    'options': [
                        {'label': f'Option {j}', 'value': f'Option {j}'}
                        for j in range(5)
                    ],
                    'mode': 'multiple',
                    'allowClear': True,
                    'placeholder': 'Please select',
                },
                'select Example 3': {
                    'options': [
                        {'label': f'Option {j}', 'value': f'Option {j}'}
                        for j in range(5)
                    ],
                    'mode': 'tags',
                    'allowClear': True,
                    'placeholder': 'Please select',
                },
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 600},
    ),
    html.Pre(id='table-rerender-select-demo-output'),
]

...

@app.callback(
    Output('table-rerender-select-demo-output', 'children'),
    [
        Input('table-rerender-select-demo', 'recentlySelectRow'),
        Input('table-rerender-select-demo', 'recentlySelectDataIndex'),
        Input('table-rerender-select-demo', 'recentlySelectValue'),
    ],
    prevent_initial_call=True,
)
def table_rerender_select_demo(
    recentlySelectRow, recentlySelectDataIndex, recentlySelectValue
):
    return json.dumps(
        dict(
            recentlySelectRow=recentlySelectRow,
            recentlySelectDataIndex=recentlySelectDataIndex,
            recentlySelectValue=recentlySelectValue,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableRerender/demos/status_badge_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': '状态徽标示例',
                    'dataIndex': '状态徽标示例',
                    'renderOptions': {'renderType': 'status-badge'},
                }
            ],
            data=[
                {
                    'key': i,
                    '状态徽标示例': {
                        'status': status,
                        'text': status + '状态示例',
                    },
                }
                for i, status in enumerate(
                    ['success', 'processing', 'default', 'error', 'warning']
                )
            ],
            style={'width': '250px'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Status Badge Example',
                    'dataIndex': 'Status Badge Example',
                    'renderOptions': {'renderType': 'status-badge'},
                }
            ],
            data=[
                {
                    'key': i,
                    'Status Badge Example': {
                        'status': status,
                        'text': status.capitalize() + ' status example',
                    },
                }
                for i, status in enumerate(
                    ['success', 'processing', 'default', 'error', 'warning']
                )
            ],
            style={'width': '250px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': '状态徽标示例',
            'dataIndex': '状态徽标示例',
            'renderOptions': {'renderType': 'status-badge'},
        }
    ],
    data=[
        {
            'key': i,
            '状态徽标示例': {'status': status, 'text': status + '状态示例'},
        }
        for i, status in enumerate(
            ['success', 'processing', 'default', 'error', 'warning']
        )
    ],
    style={'width': '250px'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'Status Badge Example',
            'dataIndex': 'Status Badge Example',
            'renderOptions': {'renderType': 'status-badge'},
        }
    ],
    data=[
        {
            'key': i,
            'Status Badge Example': {
                'status': status,
                'text': status.capitalize() + ' status example',
            },
        }
        for i, status in enumerate(
            ['success', 'processing', 'default', 'error', 'warning']
        )
    ],
    style={'width': '250px'},
)
"""
            }
        ]

```

### `views/AntdTableRerender/demos/switch_mode_and_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-switch-demo',
                columns=[
                    {
                        'title': 'switch示例',
                        'dataIndex': 'switch示例',
                        'renderOptions': {'renderType': 'switch'},
                    }
                ],
                data=[
                    {
                        'switch示例': {
                            'checked': i % 2 == 0,
                            'checkedChildren': '开',
                            'unCheckedChildren': '关',
                            'custom': 'balabalabalabala',
                        }
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-switch-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-rerender-switch-demo',
                locale='en-us',
                columns=[
                    {
                        'title': 'Switch Example',
                        'dataIndex': 'Switch Example',
                        'renderOptions': {'renderType': 'switch'},
                    }
                ],
                data=[
                    {
                        'Switch Example': {
                            'checked': i % 2 == 0,
                            'checkedChildren': 'On',
                            'unCheckedChildren': 'Off',
                            'custom': 'balabalabalabala',
                        }
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                style={'width': 200},
            ),
            html.Pre(id='table-rerender-switch-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-rerender-switch-demo-output', 'children'),
    [
        Input('table-rerender-switch-demo', 'recentlySwitchDataIndex'),
        Input('table-rerender-switch-demo', 'recentlySwitchStatus'),
        Input('table-rerender-switch-demo', 'recentlySwitchRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_switch_demo(
    recentlySwitchDataIndex, recentlySwitchStatus, recentlySwitchRow
):
    return json.dumps(
        dict(
            recentlySwitchDataIndex=recentlySwitchDataIndex,
            recentlySwitchStatus=recentlySwitchStatus,
            recentlySwitchRow=recentlySwitchRow,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-switch-demo',
        columns=[
            {
                'title': 'switch示例',
                'dataIndex': 'switch示例',
                'renderOptions': {'renderType': 'switch'},
            }
        ],
        data=[
            {
                'switch示例': {
                    'checked': i % 2 == 0,
                    'checkedChildren': '开',
                    'unCheckedChildren': '关',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-switch-demo-output'),
]

...

@app.callback(
    Output('table-rerender-switch-demo-output', 'children'),
    [
        Input('table-rerender-switch-demo', 'recentlySwitchDataIndex'),
        Input('table-rerender-switch-demo', 'recentlySwitchStatus'),
        Input('table-rerender-switch-demo', 'recentlySwitchRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_switch_demo(
    recentlySwitchDataIndex, recentlySwitchStatus, recentlySwitchRow
):
    return json.dumps(
        dict(
            recentlySwitchDataIndex=recentlySwitchDataIndex,
            recentlySwitchStatus=recentlySwitchStatus,
            recentlySwitchRow=recentlySwitchRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-rerender-switch-demo',
        locale="en-us",
        columns=[
            {
                'title': 'Switch Example',
                'dataIndex': 'Switch Example',
                'renderOptions': {'renderType': 'switch'},
            }
        ],
        data=[
            {
                'Switch Example': {
                    'checked': i % 2 == 0,
                    'checkedChildren': 'On',
                    'unCheckedChildren': 'Off',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-switch-demo-output'),
]

...

@app.callback(
    Output('table-rerender-switch-demo-output', 'children'),
    [
        Input('table-rerender-switch-demo', 'recentlySwitchDataIndex'),
        Input('table-rerender-switch-demo', 'recentlySwitchStatus'),
        Input('table-rerender-switch-demo', 'recentlySwitchRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_switch_demo(
    recentlySwitchDataIndex, recentlySwitchStatus, recentlySwitchRow
):
    return json.dumps(
        dict(
            recentlySwitchDataIndex=recentlySwitchDataIndex,
            recentlySwitchStatus=recentlySwitchStatus,
            recentlySwitchRow=recentlySwitchRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableRerender/demos/tags_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'tags示例1',
                    'dataIndex': 'tags示例1',
                    'renderOptions': {'renderType': 'tags'},
                },
                {
                    'title': 'tags示例2',
                    'dataIndex': 'tags示例2',
                    'renderOptions': {'renderType': 'tags'},
                },
            ],
            data=[
                {
                    'tags示例1': {'tag': f'标签{i}', 'color': 'cyan'},
                    'tags示例2': [
                        {'tag': f'标签{i}-{j}', 'color': color}
                        for j, color in zip(
                            range(1, 4), ['volcano', 'blue', 'geekblue']
                        )
                    ],
                }
                for i in range(1, 4)
            ],
            bordered=True,
            style={'width': 400},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            locale='en-us',
            columns=[
                {
                    'title': 'Tags Example 1',
                    'dataIndex': 'Tags Example 1',
                    'renderOptions': {'renderType': 'tags'},
                },
                {
                    'title': 'Tags Example 2',
                    'dataIndex': 'Tags Example 2',
                    'renderOptions': {'renderType': 'tags'},
                },
            ],
            data=[
                {
                    'Tags Example 1': {'tag': f'Tag {i}', 'color': 'cyan'},
                    'Tags Example 2': [
                        {'tag': f'Tag {i}-{j}', 'color': color}
                        for j, color in zip(
                            range(1, 4), ['volcano', 'blue', 'geekblue']
                        )
                    ],
                }
                for i in range(1, 4)
            ],
            bordered=True,
            style={'width': 400},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'tags示例1',
            'dataIndex': 'tags示例1',
            'renderOptions': {'renderType': 'tags'},
        },
        {
            'title': 'tags示例2',
            'dataIndex': 'tags示例2',
            'renderOptions': {'renderType': 'tags'},
        },
    ],
    data=[
        {
            'tags示例1': {'tag': f'标签{i}', 'color': 'cyan'},
            'tags示例2': [
                {'tag': f'标签{i}-{j}', 'color': color}
                for j, color in zip(
                    range(1, 4), ['volcano', 'blue', 'geekblue']
                )
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    locale="en-us",
    columns=[
        {
            'title': 'Tags Example 1',
            'dataIndex': 'Tags Example 1',
            'renderOptions': {'renderType': 'tags'},
        },
        {
            'title': 'Tags Example 2',
            'dataIndex': 'Tags Example 2',
            'renderOptions': {'renderType': 'tags'},
        },
    ],
    data=[
        {
            'Tags Example 1': {'tag': f'Tag {i}', 'color': 'cyan'},
            'Tags Example 2': [
                {'tag': f'Tag {i}-{j}', 'color': color}
                for j, color in zip(
                    range(1, 4), ['volcano', 'blue', 'geekblue']
                )
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
    style={'width': 400},
)
"""
            }
        ]

```
