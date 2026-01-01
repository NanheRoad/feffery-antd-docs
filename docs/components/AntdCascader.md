# AntdCascader

## 简介源码：`views/AntdCascader/intro.py`
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
                {'title': translator.t('AntdCascader 级联选择')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCascader 级联选择'), level=2),
        fac.AntdParagraph(
            translator.t('用于为用户提供一组具有层级信息的选项进行选择。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdCascader/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
import json
from dash import html
from dash.dependencies import Component, Input, Output

from server import app
from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = [
            fac.AntdDivider(
                'changeOnSelect=False（默认）', innerTextOrientation='left'
            ),
            fac.AntdSpace(
                [
                    fac.AntdCascader(
                        id='cascader-demo1',
                        placeholder='请选择',
                        options=[
                            {
                                'value': '节点1',
                                'label': '节点1',
                                'children': [
                                    {'value': '节点1-1', 'label': '节点1-1'},
                                    {
                                        'value': '节点1-2',
                                        'label': '节点1-2',
                                        'children': [
                                            {
                                                'value': '节点1-2-1',
                                                'label': '节点1-2-1',
                                            },
                                            {
                                                'value': '节点1-2-2',
                                                'label': '节点1-2-2',
                                            },
                                        ],
                                    },
                                ],
                            },
                            {
                                'value': '节点2',
                                'label': '节点2',
                                'children': [
                                    {'value': '节点2-1', 'label': '节点2-1'},
                                    {'value': '节点2-2', 'label': '节点2-2'},
                                ],
                            },
                        ],
                        style={'width': '200px'},
                    ),
                    fac.AntdText(id='cascader-demo1-output'),
                ]
            ),
            fac.AntdDivider('changeOnSelect=True', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    fac.AntdCascader(
                        id='cascader-demo2',
                        placeholder='请选择',
                        options=[
                            {
                                'value': '节点1',
                                'label': '节点1',
                                'children': [
                                    {'value': '节点1-1', 'label': '节点1-1'},
                                    {
                                        'value': '节点1-2',
                                        'label': '节点1-2',
                                        'children': [
                                            {
                                                'value': '节点1-2-1',
                                                'label': '节点1-2-1',
                                            },
                                            {
                                                'value': '节点1-2-2',
                                                'label': '节点1-2-2',
                                            },
                                        ],
                                    },
                                ],
                            },
                            {
                                'value': '节点2',
                                'label': '节点2',
                                'children': [
                                    {'value': '节点2-1', 'label': '节点2-1'},
                                    {'value': '节点2-2', 'label': '节点2-2'},
                                ],
                            },
                        ],
                        changeOnSelect=True,
                        style={'width': '200px'},
                    ),
                    fac.AntdText(id='cascader-demo2-output'),
                ]
            ),
            fac.AntdDivider('多选模式', innerTextOrientation='left'),
            fac.AntdCascader(
                id='cascader-demo3',
                placeholder='请选择',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                multiple=True,
                placement='topLeft',
                style={'width': '200px'},
            ),
            html.Pre(id='cascader-demo3-output'),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'changeOnSelect=False (default)', innerTextOrientation='left'
            ),
            fac.AntdSpace(
                [
                    fac.AntdCascader(
                        id='cascader-demo1',
                        placeholder='Please select',
                        options=[
                            {
                                'value': 'Node 1',
                                'label': 'Node 1',
                                'children': [
                                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                                    {
                                        'value': 'Node 1-2',
                                        'label': 'Node 1-2',
                                        'children': [
                                            {
                                                'value': 'Node 1-2-1',
                                                'label': 'Node 1-2-1',
                                            },
                                            {
                                                'value': 'Node 1-2-2',
                                                'label': 'Node 1-2-2',
                                            },
                                        ],
                                    },
                                ],
                            },
                            {
                                'value': 'Node 2',
                                'label': 'Node 2',
                                'children': [
                                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                                ],
                            },
                        ],
                        style={'width': '200px'},
                    ),
                    fac.AntdText(id='cascader-demo1-output'),
                ]
            ),
            fac.AntdDivider('changeOnSelect=True', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    fac.AntdCascader(
                        id='cascader-demo2',
                        placeholder='Please select',
                        options=[
                            {
                                'value': 'Node 1',
                                'label': 'Node 1',
                                'children': [
                                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                                    {
                                        'value': 'Node 1-2',
                                        'label': 'Node 1-2',
                                        'children': [
                                            {
                                                'value': 'Node 1-2-1',
                                                'label': 'Node 1-2-1',
                                            },
                                            {
                                                'value': 'Node 1-2-2',
                                                'label': 'Node 1-2-2',
                                            },
                                        ],
                                    },
                                ],
                            },
                            {
                                'value': 'Node 2',
                                'label': 'Node 2',
                                'children': [
                                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                                ],
                            },
                        ],
                        changeOnSelect=True,
                        style={'width': '200px'},
                    ),
                    fac.AntdText(id='cascader-demo2-output'),
                ]
            ),
            fac.AntdDivider(
                'Multiple Selection Mode', innerTextOrientation='left'
            ),
            fac.AntdCascader(
                id='cascader-demo3',
                placeholder='Please select',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                multiple=True,
                placement='topLeft',
                style={'width': '200px'},
            ),
            html.Pre(id='cascader-demo3-output'),
        ]

    return demo_contents


@app.callback(
    Output('cascader-demo1-output', 'children'),
    Input('cascader-demo1', 'value'),
    prevent_initial_call=True,
)
def cascader_demo1(value):
    return str(value)


@app.callback(
    Output('cascader-demo2-output', 'children'),
    Input('cascader-demo2', 'value'),
    prevent_initial_call=True,
)
def cascader_demo2(value):
    return str(value)


@app.callback(
    Output('cascader-demo3-output', 'children'),
    Input('cascader-demo3', 'value'),
    prevent_initial_call=True,
)
def cascader_demo3(value):
    return json.dumps(value, indent=4, ensure_ascii=False)


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDivider(
        'changeOnSelect=False（默认）', innerTextOrientation='left'
    ),
    fac.AntdSpace(
        [
            fac.AntdCascader(
                id='cascader-demo1',
                placeholder='请选择',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                style={'width': '200px'},
            ),
            fac.AntdText(id='cascader-demo1-output'),
        ]
    ),
    fac.AntdDivider('changeOnSelect=True', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            fac.AntdCascader(
                id='cascader-demo2',
                placeholder='请选择',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                changeOnSelect=True,
                style={'width': '200px'},
            ),
            fac.AntdText(id='cascader-demo2-output'),
        ]
    ),
    fac.AntdDivider('多选模式', innerTextOrientation='left'),
    fac.AntdCascader(
        id='cascader-demo3',
        placeholder='请选择',
        options=[
            {
                'value': '节点1',
                'label': '节点1',
                'children': [
                    {'value': '节点1-1', 'label': '节点1-1'},
                    {
                        'value': '节点1-2',
                        'label': '节点1-2',
                        'children': [
                            {
                                'value': '节点1-2-1',
                                'label': '节点1-2-1',
                            },
                            {
                                'value': '节点1-2-2',
                                'label': '节点1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': '节点2',
                'label': '节点2',
                'children': [
                    {'value': '节点2-1', 'label': '节点2-1'},
                    {'value': '节点2-2', 'label': '节点2-2'},
                ],
            },
        ],
        multiple=True,
        placement='topLeft',
        style={'width': '200px'},
    ),
    html.Pre(id='cascader-demo3-output'),
]

...

@app.callback(
    Output('cascader-demo1-output', 'children'),
    Input('cascader-demo1', 'value'),
    prevent_initial_call=True
)
def cascader_demo1(value):

    return str(value)


@app.callback(
    Output('cascader-demo2-output', 'children'),
    Input('cascader-demo2', 'value'),
    prevent_initial_call=True
)
def cascader_demo2(value):

    return str(value)


@app.callback(
    Output('cascader-demo3-output', 'children'),
    Input('cascader-demo3', 'value'),
    prevent_initial_call=True
)
def cascader_demo3(value):

    return json.dumps(
        value,
        indent=4,
        ensure_ascii=False
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider(
        'changeOnSelect=False (default)', innerTextOrientation='left'
    ),
    fac.AntdSpace(
        [
            fac.AntdCascader(
                id='cascader-demo1',
                placeholder='Please select',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                style={'width': '200px'},
            ),
            fac.AntdText(id='cascader-demo1-output'),
        ]
    ),
    fac.AntdDivider('changeOnSelect=True', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            fac.AntdCascader(
                id='cascader-demo2',
                placeholder='Please select',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                changeOnSelect=True,
                style={'width': '200px'},
            ),
            fac.AntdText(id='cascader-demo2-output'),
        ]
    ),
    fac.AntdDivider(
        'Multiple Selection Mode', innerTextOrientation='left'
    ),
    fac.AntdCascader(
        id='cascader-demo3',
        placeholder='Please select',
        options=[
            {
                'value': 'Node 1',
                'label': 'Node 1',
                'children': [
                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                    {
                        'value': 'Node 1-2',
                        'label': 'Node 1-2',
                        'children': [
                            {
                                'value': 'Node 1-2-1',
                                'label': 'Node 1-2-1',
                            },
                            {
                                'value': 'Node 1-2-2',
                                'label': 'Node 1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': 'Node 2',
                'label': 'Node 2',
                'children': [
                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                ],
            },
        ],
        multiple=True,
        placement='topLeft',
        style={'width': '200px'},
    ),
    html.Pre(id='cascader-demo3-output'),
]

...

@app.callback(
    Output('cascader-demo1-output', 'children'),
    Input('cascader-demo1', 'value'),
    prevent_initial_call=True
)
def cascader_demo1(value):

    return str(value)


@app.callback(
    Output('cascader-demo2-output', 'children'),
    Input('cascader-demo2', 'value'),
    prevent_initial_call=True
)
def cascader_demo2(value):

    return str(value)


@app.callback(
    Output('cascader-demo3-output', 'children'),
    Input('cascader-demo3', 'value'),
    prevent_initial_call=True
)
def cascader_demo3(value):

    return json.dumps(
        value,
        indent=4,
        ensure_ascii=False
    )
"""
            }
        ]

```

### `views/AntdCascader/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
)
"""
            }
        ]

```

### `views/AntdCascader/demos/change_on_select.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            changeOnSelect=True,
            style={'width': '200px'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            changeOnSelect=True,
            style={'width': '200px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    changeOnSelect=True,
    style={
        'width': '200px'
    }
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    changeOnSelect=True,
    style={'width': '200px'},
)
"""
            }
        ]

```

### `views/AntdCascader/demos/different_placement.py`
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
                fac.AntdCascader(
                    placeholder=f'placement="{placement}"',
                    options=[
                        {
                            'value': '节点1',
                            'label': '节点1',
                            'children': [
                                {'value': '节点1-1', 'label': '节点1-1'},
                                {
                                    'value': '节点1-2',
                                    'label': '节点1-2',
                                    'children': [
                                        {
                                            'value': '节点1-2-1',
                                            'label': '节点1-2-1',
                                        },
                                        {
                                            'value': '节点1-2-2',
                                            'label': '节点1-2-2',
                                        },
                                    ],
                                },
                            ],
                        }
                    ],
                    placement=placement,
                    style={'width': '200px'},
                )
                for placement in [
                    'bottomLeft',
                    'bottomRight',
                    'topLeft',
                    'topRight',
                ]
            ],
            direction='vertical',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdCascader(
                    placeholder=f'placement="{placement}"',
                    options=[
                        {
                            'value': 'Node 1',
                            'label': 'Node 1',
                            'children': [
                                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                                {
                                    'value': 'Node 1-2',
                                    'label': 'Node 1-2',
                                    'children': [
                                        {
                                            'value': 'Node 1-2-1',
                                            'label': 'Node 1-2-1',
                                        },
                                        {
                                            'value': 'Node 1-2-2',
                                            'label': 'Node 1-2-2',
                                        },
                                    ],
                                },
                            ],
                        }
                    ],
                    placement=placement,
                    style={'width': '200px'},
                )
                for placement in [
                    'bottomLeft',
                    'bottomRight',
                    'topLeft',
                    'topRight',
                ]
            ],
            direction='vertical',
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
        fac.AntdCascader(
            placeholder=f'placement="{placement}"',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {
                            'value': '节点1-1',
                            'label': '节点1-1'
                        },
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {
                                    'value': '节点1-2-1',
                                    'label': '节点1-2-1'
                                },
                                {
                                    'value': '节点1-2-2',
                                    'label': '节点1-2-2'
                                }
                            ]
                        }
                    ]
                }
            ],
            placement=placement,
            style={
                'width': '200px'
            }
        )
        for placement in [
            'bottomLeft', 'bottomRight', 'topLeft', 'topRight'
        ]
    ],
    direction='vertical'
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
        fac.AntdCascader(
            placeholder=f'placement="{placement}"',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {
                                    'value': 'Node 1-2-1',
                                    'label': 'Node 1-2-1',
                                },
                                {
                                    'value': 'Node 1-2-2',
                                    'label': 'Node 1-2-2',
                                },
                            ],
                        },
                    ],
                }
            ],
            placement=placement,
            style={'width': '200px'},
        )
        for placement in [
            'bottomLeft',
            'bottomRight',
            'topLeft',
            'topRight',
        ]
    ],
    direction='vertical',
)
"""
            }
        ]

```

### `views/AntdCascader/demos/disabled_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            disabled=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            disabled=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    disabled=True
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    disabled=True,
)
"""
            }
        ]

```

### `views/AntdCascader/demos/expand_trigger.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                }
            ],
            expandTrigger='hover',
            style={'width': '200px'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                }
            ],
            expandTrigger='hover',
            style={'width': '200px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        }
    ],
    expandTrigger='hover',
    style={
        'width': '200px'
    }
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        }
    ],
    expandTrigger='hover',
    style={'width': '200px'},
)
"""
            }
        ]

```

### `views/AntdCascader/demos/flat_options_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            optionsMode='flat',
            options=[
                {'value': '1', 'label': '节点1', 'key': '1'},
                *[
                    {
                        'value': f'1-{i}',
                        'label': f'节点1-{i}',
                        'key': f'1-{i}',
                        'parent': '1',
                    }
                    for i in range(1, 4)
                ],
                {'value': '2', 'label': '节点2', 'key': '2'},
                {
                    'value': '2-1',
                    'label': '节点2-1',
                    'key': '2-1',
                    'parent': '2',
                },
                {
                    'value': '2-2',
                    'label': '节点2-2',
                    'key': '2-2',
                    'parent': '2',
                },
                *[
                    {
                        'value': f'2-2-{i}',
                        'label': f'节点2-2-{i}',
                        'key': f'2-2-{i}',
                        'parent': '2-2',
                    }
                    for i in range(1, 4)
                ],
            ],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            optionsMode='flat',
            options=[
                {'value': '1', 'label': 'Node 1', 'key': '1'},
                *[
                    {
                        'value': f'1-{i}',
                        'label': f'Node 1-{i}',
                        'key': f'1-{i}',
                        'parent': '1',
                    }
                    for i in range(1, 4)
                ],
                {'value': '2', 'label': 'Node 2', 'key': '2'},
                {
                    'value': '2-1',
                    'label': 'Node 2-1',
                    'key': '2-1',
                    'parent': '2',
                },
                {
                    'value': '2-2',
                    'label': 'Node 2-2',
                    'key': '2-2',
                    'parent': '2',
                },
                *[
                    {
                        'value': f'2-2-{i}',
                        'label': f'Node 2-2-{i}',
                        'key': f'2-2-{i}',
                        'parent': '2-2',
                    }
                    for i in range(1, 4)
                ],
            ],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    optionsMode='flat',
    options=[
        {
            'value': '1',
            'label': '节点1',
            'key': '1'
        },
        *[
            {
                'value': f'1-{i}',
                'label': f'节点1-{i}',
                'key': f'1-{i}',
                'parent': '1'
            }
            for i in range(1, 4)
        ],
        {
            'value': '2',
            'label': '节点2',
            'key': '2'
        },
        {
            'value': '2-1',
            'label': '节点2-1',
            'key': '2-1',
            'parent': '2'
        },
        {
            'value': '2-2',
            'label': '节点2-2',
            'key': '2-2',
            'parent': '2'
        },
        *[
            {
                'value': f'2-2-{i}',
                'label': f'节点2-2-{i}',
                'key': f'2-2-{i}',
                'parent': '2-2'
            }
            for i in range(1, 4)
        ],
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    optionsMode='flat',
    options=[
        {'value': '1', 'label': 'Node 1', 'key': '1'},
        *[
            {
                'value': f'1-{i}',
                'label': f'Node 1-{i}',
                'key': f'1-{i}',
                'parent': '1',
            }
            for i in range(1, 4)
        ],
        {'value': '2', 'label': 'Node 2', 'key': '2'},
        {
            'value': '2-1',
            'label': 'Node 2-1',
            'key': '2-1',
            'parent': '2',
        },
        {
            'value': '2-2',
            'label': 'Node 2-2',
            'key': '2-2',
            'parent': '2',
        },
        *[
            {
                'value': f'2-2-{i}',
                'label': f'Node 2-2-{i}',
                'key': f'2-2-{i}',
                'parent': '2-2',
            }
            for i in range(1, 4)
        ],
    ],
)
"""
            }
        ]

```

### `views/AntdCascader/demos/multiple_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='多选模式：',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            multiple=True,
            style={'width': '200px'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Multiple Selection Mode:',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            multiple=True,
            style={'width': '200px'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='多选模式：',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    multiple=True,
    style={
        'width': '200px'
    }
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Multiple Selection Mode:',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    multiple=True,
    style={'width': '200px'},
)
"""
            }
        ]

```

### `views/AntdCascader/demos/options_node_to_label.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'key': '节点1',
                    'label': '节点1',
                    'children': [
                        {
                            'value': '节点1-1',
                            'key': '节点1-1',
                            'label': '节点1-1',
                        },
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            optionsNodeKeyToLabel={
                '节点1': fac.AntdText('节点1', italic=True),
                '节点1-1': fac.AntdText(
                    '节点1-1', strong=True, style={'color': 'red'}
                ),
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'key': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {
                            'value': 'Node 1-1',
                            'key': 'Node 1-1',
                            'label': 'Node 1-1',
                        },
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            optionsNodeKeyToLabel={
                'Node 1': fac.AntdText('Node 1', italic=True),
                'Node 1-1': fac.AntdText(
                    'Node 1-1', strong=True, style={'color': 'red'}
                ),
            },
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'key': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'key': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    optionsNodeKeyToLabel={
        '节点1': fac.AntdText('节点1', italic=True),
        '节点1-1': fac.AntdText(
            '节点1-1',
            strong=True,
            style={
                'color': 'red'
            }
        )
    }
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'key': 'Node 1',
            'label': 'Node 1',
            'children': [
                {
                    'value': 'Node 1-1',
                    'key': 'Node 1-1',
                    'label': 'Node 1-1',
                },
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    optionsNodeKeyToLabel={
        'Node 1': fac.AntdText('Node 1', italic=True),
        'Node 1-1': fac.AntdText(
            'Node 1-1', strong=True, style={'color': 'red'}
        ),
    },
)
"""
            }
        ]

```

### `views/AntdCascader/demos/panel_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            panelMode=True,
            options=[
                {
                    'label': '四川省',
                    'key': '四川省',
                    'value': '四川省',
                    'children': [
                        {
                            'label': '成都市',
                            'key': '成都市',
                            'value': '成都市',
                        },
                        {
                            'label': '广安市',
                            'key': '广安市',
                            'value': '广安市',
                        },
                    ],
                },
                {
                    'label': '重庆市',
                    'key': '重庆市',
                    'value': '重庆市',
                    'children': [
                        {
                            'label': '渝中区',
                            'key': '渝中区',
                            'value': '渝中区',
                            'children': [
                                {
                                    'label': '解放碑街道',
                                    'key': '解放碑街道',
                                    'value': '解放碑街道',
                                }
                            ],
                        },
                        {
                            'label': '渝北区',
                            'key': '渝北区',
                            'value': '渝北区',
                        },
                    ],
                },
            ],
            placeholder='请选择',
            multiple=True,
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            panelMode=True,
            options=[
                {
                    'label': 'Sichuan Province',
                    'key': 'Sichuan Province',
                    'value': 'Sichuan Province',
                    'children': [
                        {
                            'label': 'Chengdu City',
                            'key': 'Chengdu City',
                            'value': 'Chengdu City',
                        },
                        {
                            'label': "Guang'an City",
                            'key': "Guang'an City",
                            'value': "Guang'an City",
                        },
                    ],
                },
                {
                    'label': 'Chongqing Municipality',
                    'key': 'Chongqing Municipality',
                    'value': 'Chongqing Municipality',
                    'children': [
                        {
                            'label': 'Yuzhong District',
                            'key': 'Yuzhong District',
                            'value': 'Yuzhong District',
                            'children': [
                                {
                                    'label': 'Jiefangbei Sub-district',
                                    'key': 'Jiefangbei Sub-district',
                                    'value': 'Jiefangbei Sub-district',
                                }
                            ],
                        },
                        {
                            'label': 'Yubei District',
                            'key': 'Yubei District',
                            'value': 'Yubei District',
                        },
                    ],
                },
            ],
            placeholder='Please select',
            multiple=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    panelMode=True,
    options=[
        {
            'label': '四川省',
            'key': '四川省',
            'value': '四川省',
            'children': [
                {
                    'label': '成都市',
                    'key': '成都市',
                    'value': '成都市',
                },
                {
                    'label': '广安市',
                    'key': '广安市',
                    'value': '广安市',
                },
            ],
        },
        {
            'label': '重庆市',
            'key': '重庆市',
            'value': '重庆市',
            'children': [
                {
                    'label': '渝中区',
                    'key': '渝中区',
                    'value': '渝中区',
                    'children': [
                        {
                            'label': '解放碑街道',
                            'key': '解放碑街道',
                            'value': '解放碑街道',
                        }
                    ],
                },
                {
                    'label': '渝北区',
                    'key': '渝北区',
                    'value': '渝北区',
                },
            ],
        },
    ],
    placeholder='请选择',
    multiple=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    panelMode=True,
    options=[
        {
            'label': 'Sichuan Province',
            'key': 'Sichuan Province',
            'value': 'Sichuan Province',
            'children': [
                {
                    'label': 'Chengdu City',
                    'key': 'Chengdu City',
                    'value': 'Chengdu City',
                },
                {
                    'label': "Guang'an City",
                    'key': "Guang'an City",
                    'value': "Guang'an City",
                },
            ],
        },
        {
            'label': 'Chongqing Municipality',
            'key': 'Chongqing Municipality',
            'value': 'Chongqing Municipality',
            'children': [
                {
                    'label': 'Yuzhong District',
                    'key': 'Yuzhong District',
                    'value': 'Yuzhong District',
                    'children': [
                        {
                            'label': 'Jiefangbei Sub-district',
                            'key': 'Jiefangbei Sub-district',
                            'value': 'Jiefangbei Sub-district',
                        }
                    ],
                },
                {
                    'label': 'Yubei District',
                    'key': 'Yubei District',
                    'value': 'Yubei District',
                },
            ],
        },
    ],
    placeholder='Please select',
    multiple=True,
)
"""
            }
        ]

```

### `views/AntdCascader/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            value=[['节点1', '节点1-1']],
            prefix=fac.AntdIcon(icon='antd-user'),
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            value=[['Node 1', 'Node 1-1']],
            prefix=fac.AntdIcon(icon='antd-user'),
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    value=[
        ['节点1', '节点1-1']
    ],
    prefix=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    value=[['Node 1', 'Node 1-1']],
    prefix=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]

```

### `views/AntdCascader/demos/read_only_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            readOnly=True,
            value=[['节点1', '节点1-1']],
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            readOnly=True,
            value=[['Node 1', 'Node 1-1']],
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    readOnly=True,
    value=[
        ['节点1', '节点1-1']
    ]
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    readOnly=True,
    value=[['Node 1', 'Node 1-1']],
)
"""
            }
        ]

```

### `views/AntdCascader/demos/render_status.py`
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
                fac.AntdCascader(
                    placeholder=f'status="{status}"',
                    options=[
                        {
                            'value': '节点1',
                            'label': '节点1',
                            'children': [
                                {'value': '节点1-1', 'label': '节点1-1'},
                                {
                                    'value': '节点1-2',
                                    'label': '节点1-2',
                                    'children': [
                                        {
                                            'value': '节点1-2-1',
                                            'label': '节点1-2-1',
                                        },
                                        {
                                            'value': '节点1-2-2',
                                            'label': '节点1-2-2',
                                        },
                                    ],
                                },
                            ],
                        },
                        {
                            'value': '节点2',
                            'label': '节点2',
                            'children': [
                                {'value': '节点2-1', 'label': '节点2-1'},
                                {'value': '节点2-2', 'label': '节点2-2'},
                            ],
                        },
                    ],
                    status=status,
                )
                for status in ['warning', 'error']
            ],
            direction='vertical',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdCascader(
                    placeholder=f'status="{status}"',
                    options=[
                        {
                            'value': 'Node 1',
                            'label': 'Node 1',
                            'children': [
                                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                                {
                                    'value': 'Node 1-2',
                                    'label': 'Node 1-2',
                                    'children': [
                                        {
                                            'value': 'Node 1-2-1',
                                            'label': 'Node 1-2-1',
                                        },
                                        {
                                            'value': 'Node 1-2-2',
                                            'label': 'Node 1-2-2',
                                        },
                                    ],
                                },
                            ],
                        },
                        {
                            'value': 'Node 2',
                            'label': 'Node 2',
                            'children': [
                                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                                {'value': 'Node 2-2', 'label': 'Node 2-2'},
                            ],
                        },
                    ],
                    status=status,
                )
                for status in ['warning', 'error']
            ],
            direction='vertical',
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
        fac.AntdCascader(
            placeholder=f'status="{status}"',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {
                            'value': '节点1-1',
                            'label': '节点1-1'
                        },
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {
                                    'value': '节点1-2-1',
                                    'label': '节点1-2-1'
                                },
                                {
                                    'value': '节点1-2-2',
                                    'label': '节点1-2-2'
                                }
                            ]
                        }
                    ]
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {
                            'value': '节点2-1',
                            'label': '节点2-1'
                        },
                        {
                            'value': '节点2-2',
                            'label': '节点2-2'
                        }
                    ]
                }
            ],
            status=status
        )
        for status in ['warning', 'error']
    ],
    direction='vertical'
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
        fac.AntdCascader(
            placeholder=f'status="{status}"',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {
                                    'value': 'Node 1-2-1',
                                    'label': 'Node 1-2-1',
                                },
                                {
                                    'value': 'Node 1-2-2',
                                    'label': 'Node 1-2-2',
                                },
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            status=status,
        )
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
"""
            }
        ]

```

### `views/AntdCascader/demos/search_keyword.py`
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
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSwitch(
                    id='cascader-demo-search_keyword_switch',
                    checked=True,
                    checkedChildren='label模式',
                    unCheckedChildren='value模式',
                ),
                fac.AntdCascader(
                    id='cascader-demo-search_keyword',
                    options=[
                        {
                            'label': '四川省',
                            'key': '四川省',
                            'value': 'scs',
                            'children': [
                                {
                                    'label': '成都市',
                                    'key': '成都市',
                                    'value': 'cds',
                                },
                                {
                                    'label': '广安市',
                                    'key': '广安市',
                                    'value': 'gas',
                                },
                            ],
                        },
                        {
                            'label': '重庆市',
                            'key': '重庆市',
                            'value': 'cqs',
                            'children': [
                                {
                                    'label': '渝中区',
                                    'key': '渝中区',
                                    'value': 'yzq',
                                    'children': [
                                        {
                                            'label': '解放碑街道',
                                            'key': '解放碑街道',
                                            'value': 'jfbjd',
                                        }
                                    ],
                                },
                                {
                                    'label': '渝北区',
                                    'key': '渝北区',
                                    'value': 'ybq',
                                },
                            ],
                        },
                    ],
                    placeholder='请选择',
                    multiple=True,
                ),
            ],
            direction='vertical',
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSwitch(
                    id='cascader-demo-search_keyword_switch',
                    checked=True,
                    checkedChildren='label mode',
                    unCheckedChildren='value mode',
                ),
                fac.AntdCascader(
                    id='cascader-demo-search_keyword',
                    options=[
                        {
                            'label': 'Sichuan Province',
                            'key': 'Sichuan Province',
                            'value': 'scs',
                            'children': [
                                {
                                    'label': 'Chengdu City',
                                    'key': 'Chengdu City',
                                    'value': 'cds',
                                },
                                {
                                    'label': "Guang'an City",
                                    'key': "Guang'an City",
                                    'value': 'gas',
                                },
                            ],
                        },
                        {
                            'label': 'Chongqing Municipality',
                            'key': 'Chongqing Municipality',
                            'value': 'cqs',
                            'children': [
                                {
                                    'label': 'Yuzhong District',
                                    'key': 'Yuzhong District',
                                    'value': 'yzq',
                                    'children': [
                                        {
                                            'label': 'Jiefangbei Sub-district',
                                            'key': 'Jiefangbei Sub-district',
                                            'value': 'jfbjd',
                                        }
                                    ],
                                },
                                {
                                    'label': 'Yubei District',
                                    'key': 'Yubei District',
                                    'value': 'ybq',
                                },
                            ],
                        },
                    ],
                    placeholder='Please select',
                    multiple=True,
                ),
            ],
            direction='vertical',
        )

    return demo_contents


@app.callback(
    Output('cascader-demo-search_keyword', 'optionFilterProp'),
    Input('cascader-demo-search_keyword_switch', 'checked'),
)
def cascader_search_keyword(checked):
    if checked:
        return 'label'
    return 'value'


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(
            id='cascader-demo-search_keyword_switch',
            checked=True,
            checkedChildren='label',
            unCheckedChildren='value',
        ),
        fac.AntdCascader(
            id='cascader-demo-search_keyword',
            options=[
                {
                    'label': '四川省',
                    'key': '四川省',
                    'value': 'scs',
                    'children': [
                        {
                            'label': '成都市',
                            'key': '成都市',
                            'value': 'cds',
                        },
                        {
                            'label': '广安市',
                            'key': '广安市',
                            'value': 'gas',
                        },
                    ],
                },
                {
                    'label': '重庆市',
                    'key': '重庆市',
                    'value': 'cqs',
                    'children': [
                        {
                            'label': '渝中区',
                            'key': '渝中区',
                            'value': 'yzq',
                            'children': [
                                {
                                    'label': '解放碑街道',
                                    'key': '解放碑街道',
                                    'value': 'jfbjd',
                                }
                            ],
                        },
                        {
                            'label': '渝北区',
                            'key': '渝北区',
                            'value': 'ybq',
                        },
                    ],
                },
            ],
            placeholder='请选择',
            multiple=True,
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('cascader-demo-search_keyword', 'optionFilterProp'),
    Input('cascader-demo-search_keyword_switch', 'checked'),
)
def cascader_search_keyword(checked):
    if checked:
        return 'label'
    return 'value'
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(
            id='cascader-demo-search_keyword_switch',
            checked=True,
            checkedChildren='label mode',
            unCheckedChildren='value mode',
        ),
        fac.AntdCascader(
            id='cascader-demo-search_keyword',
            options=[
                {
                    'label': 'Sichuan Province',
                    'key': 'Sichuan Province',
                    'value': 'scs',
                    'children': [
                        {
                            'label': 'Chengdu City',
                            'key': 'Chengdu City',
                            'value': 'cds',
                        },
                        {
                            'label': "Guang'an City",
                            'key': "Guang'an City",
                            'value': 'gas',
                        },
                    ],
                },
                {
                    'label': 'Chongqing Municipality',
                    'key': 'Chongqing Municipality',
                    'value': 'cqs',
                    'children': [
                        {
                            'label': 'Yuzhong District',
                            'key': 'Yuzhong District',
                            'value': 'yzq',
                            'children': [
                                {
                                    'label': 'Jiefangbei Sub-district',
                                    'key': 'Jiefangbei Sub-district',
                                    'value': 'jfbjd',
                                }
                            ],
                        },
                        {
                            'label': 'Yubei District',
                            'key': 'Yubei District',
                            'value': 'ybq',
                        },
                    ],
                },
            ],
            placeholder='Please select',
            multiple=True,
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('cascader-demo-search_keyword', 'optionFilterProp'),
    Input('cascader-demo-search_keyword_switch', 'checked'),
)
def cascader_search_keyword(checked):
    if checked:
        return 'label'
    return 'value'
"""
            }
        ]

```

### `views/AntdCascader/demos/show_checked_strategy.py`
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
                'showCheckedStrategy="show-parent"（默认）',
                innerTextOrientation='left',
            ),
            fac.AntdCascader(
                placeholder='请选择',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                multiple=True,
            ),
            fac.AntdDivider(
                'showCheckedStrategy="show-child"', innerTextOrientation='left'
            ),
            fac.AntdCascader(
                placeholder='请选择（单选）',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                showCheckedStrategy='show-child',
            ),
            fac.AntdCascader(
                placeholder='请选择',
                options=[
                    {
                        'value': '节点1',
                        'label': '节点1',
                        'children': [
                            {'value': '节点1-1', 'label': '节点1-1'},
                            {
                                'value': '节点1-2',
                                'label': '节点1-2',
                                'children': [
                                    {
                                        'value': '节点1-2-1',
                                        'label': '节点1-2-1',
                                    },
                                    {
                                        'value': '节点1-2-2',
                                        'label': '节点1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': '节点2',
                        'label': '节点2',
                        'children': [
                            {'value': '节点2-1', 'label': '节点2-1'},
                            {'value': '节点2-2', 'label': '节点2-2'},
                        ],
                    },
                ],
                showCheckedStrategy='show-child',
                multiple=True,
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'showCheckedStrategy="show-parent" (default)',
                innerTextOrientation='left',
            ),
            fac.AntdCascader(
                placeholder='Please select',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                multiple=True,
            ),
            fac.AntdDivider(
                'showCheckedStrategy="show-child"', innerTextOrientation='left'
            ),
            fac.AntdCascader(
                placeholder='Please select (single selection)',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                showCheckedStrategy='show-child',
            ),
            fac.AntdCascader(
                placeholder='Please select',
                options=[
                    {
                        'value': 'Node 1',
                        'label': 'Node 1',
                        'children': [
                            {'value': 'Node 1-1', 'label': 'Node 1-1'},
                            {
                                'value': 'Node 1-2',
                                'label': 'Node 1-2',
                                'children': [
                                    {
                                        'value': 'Node 1-2-1',
                                        'label': 'Node 1-2-1',
                                    },
                                    {
                                        'value': 'Node 1-2-2',
                                        'label': 'Node 1-2-2',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        'value': 'Node 2',
                        'label': 'Node 2',
                        'children': [
                            {'value': 'Node 2-1', 'label': 'Node 2-1'},
                            {'value': 'Node 2-2', 'label': 'Node 2-2'},
                        ],
                    },
                ],
                showCheckedStrategy='show-child',
                multiple=True,
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
        'showCheckedStrategy="show-parent"（默认）',
        innerTextOrientation='left',
    ),
    fac.AntdCascader(
        placeholder='请选择',
        options=[
            {
                'value': '节点1',
                'label': '节点1',
                'children': [
                    {'value': '节点1-1', 'label': '节点1-1'},
                    {
                        'value': '节点1-2',
                        'label': '节点1-2',
                        'children': [
                            {
                                'value': '节点1-2-1',
                                'label': '节点1-2-1',
                            },
                            {
                                'value': '节点1-2-2',
                                'label': '节点1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': '节点2',
                'label': '节点2',
                'children': [
                    {'value': '节点2-1', 'label': '节点2-1'},
                    {'value': '节点2-2', 'label': '节点2-2'},
                ],
            },
        ],
        multiple=True,
    ),
    fac.AntdDivider(
        'showCheckedStrategy="show-child"', innerTextOrientation='left'
    ),
    fac.AntdCascader(
        placeholder='请选择（单选）',
        options=[
            {
                'value': '节点1',
                'label': '节点1',
                'children': [
                    {'value': '节点1-1', 'label': '节点1-1'},
                    {
                        'value': '节点1-2',
                        'label': '节点1-2',
                        'children': [
                            {
                                'value': '节点1-2-1',
                                'label': '节点1-2-1',
                            },
                            {
                                'value': '节点1-2-2',
                                'label': '节点1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': '节点2',
                'label': '节点2',
                'children': [
                    {'value': '节点2-1', 'label': '节点2-1'},
                    {'value': '节点2-2', 'label': '节点2-2'},
                ],
            },
        ],
        showCheckedStrategy='show-child',
    ),
    fac.AntdCascader(
        placeholder='请选择',
        options=[
            {
                'value': '节点1',
                'label': '节点1',
                'children': [
                    {'value': '节点1-1', 'label': '节点1-1'},
                    {
                        'value': '节点1-2',
                        'label': '节点1-2',
                        'children': [
                            {
                                'value': '节点1-2-1',
                                'label': '节点1-2-1',
                            },
                            {
                                'value': '节点1-2-2',
                                'label': '节点1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': '节点2',
                'label': '节点2',
                'children': [
                    {'value': '节点2-1', 'label': '节点2-1'},
                    {'value': '节点2-2', 'label': '节点2-2'},
                ],
            },
        ],
        showCheckedStrategy='show-child',
        multiple=True,
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
        'showCheckedStrategy="show-parent" (default)',
        innerTextOrientation='left',
    ),
    fac.AntdCascader(
        placeholder='Please select',
        options=[
            {
                'value': 'Node 1',
                'label': 'Node 1',
                'children': [
                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                    {
                        'value': 'Node 1-2',
                        'label': 'Node 1-2',
                        'children': [
                            {
                                'value': 'Node 1-2-1',
                                'label': 'Node 1-2-1',
                            },
                            {
                                'value': 'Node 1-2-2',
                                'label': 'Node 1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': 'Node 2',
                'label': 'Node 2',
                'children': [
                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                ],
            },
        ],
        multiple=True,
    ),
    fac.AntdDivider(
        'showCheckedStrategy="show-child"', innerTextOrientation='left'
    ),
    fac.AntdCascader(
        placeholder='Please select (single selection)',
        options=[
            {
                'value': 'Node 1',
                'label': 'Node 1',
                'children': [
                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                    {
                        'value': 'Node 1-2',
                        'label': 'Node 1-2',
                        'children': [
                            {
                                'value': 'Node 1-2-1',
                                'label': 'Node 1-2-1',
                            },
                            {
                                'value': 'Node 1-2-2',
                                'label': 'Node 1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': 'Node 2',
                'label': 'Node 2',
                'children': [
                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                ],
            },
        ],
        showCheckedStrategy='show-child',
    ),
    fac.AntdCascader(
        placeholder='Please select',
        options=[
            {
                'value': 'Node 1',
                'label': 'Node 1',
                'children': [
                    {'value': 'Node 1-1', 'label': 'Node 1-1'},
                    {
                        'value': 'Node 1-2',
                        'label': 'Node 1-2',
                        'children': [
                            {
                                'value': 'Node 1-2-1',
                                'label': 'Node 1-2-1',
                            },
                            {
                                'value': 'Node 1-2-2',
                                'label': 'Node 1-2-2',
                            },
                        ],
                    },
                ],
            },
            {
                'value': 'Node 2',
                'label': 'Node 2',
                'children': [
                    {'value': 'Node 2-1', 'label': 'Node 2-1'},
                    {'value': 'Node 2-2', 'label': 'Node 2-2'},
                ],
            },
        ],
        showCheckedStrategy='show-child',
        multiple=True,
    ),
]
"""
            }
        ]

```

### `views/AntdCascader/demos/suffix_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCascader(
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {'value': '节点1-1', 'label': '节点1-1'},
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {'value': '节点1-2-1', 'label': '节点1-2-1'},
                                {'value': '节点1-2-2', 'label': '节点1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {'value': '节点2-1', 'label': '节点2-1'},
                        {'value': '节点2-2', 'label': '节点2-2'},
                    ],
                },
            ],
            value=[['节点1', '节点1-1']],
            suffixIcon=fac.AntdIcon(icon='antd-user'),
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCascader(
            placeholder='Please select',
            options=[
                {
                    'value': 'Node 1',
                    'label': 'Node 1',
                    'children': [
                        {'value': 'Node 1-1', 'label': 'Node 1-1'},
                        {
                            'value': 'Node 1-2',
                            'label': 'Node 1-2',
                            'children': [
                                {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                                {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                            ],
                        },
                    ],
                },
                {
                    'value': 'Node 2',
                    'label': 'Node 2',
                    'children': [
                        {'value': 'Node 2-1', 'label': 'Node 2-1'},
                        {'value': 'Node 2-2', 'label': 'Node 2-2'},
                    ],
                },
            ],
            value=[['Node 1', 'Node 1-1']],
            suffixIcon=fac.AntdIcon(icon='antd-user'),
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='请选择',
    options=[
        {
            'value': '节点1',
            'label': '节点1',
            'children': [
                {
                    'value': '节点1-1',
                    'label': '节点1-1'
                },
                {
                    'value': '节点1-2',
                    'label': '节点1-2',
                    'children': [
                        {
                            'value': '节点1-2-1',
                            'label': '节点1-2-1'
                        },
                        {
                            'value': '节点1-2-2',
                            'label': '节点1-2-2'
                        }
                    ]
                }
            ]
        },
        {
            'value': '节点2',
            'label': '节点2',
            'children': [
                {
                    'value': '节点2-1',
                    'label': '节点2-1'
                },
                {
                    'value': '节点2-2',
                    'label': '节点2-2'
                }
            ]
        }
    ],
    value=[
        ['节点1', '节点1-1']
    ],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCascader(
    placeholder='Please select',
    options=[
        {
            'value': 'Node 1',
            'label': 'Node 1',
            'children': [
                {'value': 'Node 1-1', 'label': 'Node 1-1'},
                {
                    'value': 'Node 1-2',
                    'label': 'Node 1-2',
                    'children': [
                        {'value': 'Node 1-2-1', 'label': 'Node 1-2-1'},
                        {'value': 'Node 1-2-2', 'label': 'Node 1-2-2'},
                    ],
                },
            ],
        },
        {
            'value': 'Node 2',
            'label': 'Node 2',
            'children': [
                {'value': 'Node 2-1', 'label': 'Node 2-1'},
                {'value': 'Node 2-2', 'label': 'Node 2-2'},
            ],
        },
    ],
    value=[['Node 1', 'Node 1-1']],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
"""
            }
        ]

```

## API 文档

- id (string; optional):
    The unique identifier for the component.

- allowClear (boolean; default True):
    Whether to allow one-click clearing of the selected value. Default value: `True`.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- autoFocus (boolean; default False):
    Whether to automatically focus. Default value: `False`.

- batchPropsNames (list of strings; optional):
    A list of property names to include in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):
    Listens to the values of several properties specified in `batchPropsNames`.

- bordered (boolean; default True):
    Whether to display a border, setting it to `True` is equivalent to `variant='outlined'`. Default value: `True`.

- changeOnSelect (boolean; default False):
    Whether to update the selected value when any node in the cascade selection is chosen. Default value: `False`.

- className (string | dict; optional):
    The current component's CSS class name, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- defaultValue (list of string | numbers | list of list of string | numbers; optional):
    The initial selected values.

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- expandTrigger (a value equal to: 'click', 'hover'; default 'click'):
    The trigger method for expanding the selection menu, options include `'click'`, `'hover'`. Default value: `'click'`.

- key (string; optional):
    Updating the `key` value of the current component can force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:
    - component_name (string; optional):
        Holds the name of the component that is loading.
    - is_loading (boolean; optional):
        Determines if the component is loading or not.
    - prop_name (string; optional):
        Holds which property is loading.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    The language of the component's text, options include `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German). Default value: `'zh-cn'`.

- maxTagCount (number | a value equal to: 'responsive'; optional):
    The maximum number of selected values displayed when `multiple=True`.

- multiple (boolean; default False):
    Whether to enable multi-selection mode. Default value: `False`.

- name (string; optional):
    Used in conjunction with the `AntdForm` form batch value collection/control feature, serving as the field name for the current form item, with `id` as the default value.

- optionFilterProp (a value equal to: 'value', 'label'; default 'label'):
    The target field for option keyword search, options include `'value'`, `'label'`. Default value: `'label'`.

- options (list; required):
    Defines the data structure required for constructing cascade selection, consistent with `optionsMode`.

- optionsMode (a value equal to: 'tree', 'flat'; default 'tree'):
    The rendering mode corresponding to the `options` format, options include `'tree'` (tree mode), `'flat'` (flat mode). Default value: `'tree'`.

- optionsNodeKeyToLabel (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    For specified nodes in the cascade structure, defines the component-type content that serves as the title, with higher priority than the corresponding `label` value in `options`.

- panelMode (boolean; default False):
    Whether to enable the embedded panel mode. Default value: `False`.

- persisted_props (list of a value equal to: 'value's; default ['value']):
    The names of several properties that enable attribute persistence, with the option of `'value'`. Default value: `['value']`.

- persistence (boolean | string | number; optional):
    Whether to enable [property persistence](/prop-persistence).

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The storage type for property persistence, options include `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence). Default value: `'local'`.

- placeholder (string; optional):
    The placeholder text content of the input box.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):
    The direction in which the selection menu expands, options include `'bottomLeft'`, `'bottomRight'`, `'topLeft'`, `'topRight'`. Default value: `'bottomLeft'`.

- popupClassName (string; optional):
    The CSS class name of the expanded menu.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    The anchoring strategy for the related expansion layer, options include `'parent'`, `'body'`. Default value: `'body'`.

- readOnly (boolean; optional):
    Whether to render in read-only state. Default value: `False`.

- showCheckedStrategy (a value equal to: 'show-parent', 'show-child'; optional):
    The strategy for filling in the selected options, options include `'show-parent'`, `'show-child'`.

- size (a value equal to: 'small', 'middle', 'large'; optional):
    The size specification of the current component, options include `'small'`, `'middle'`, `'large'`. Default value: `'middle'`.

- status (a value equal to: 'error', 'warning'; optional):
    Controls the validation status, options include `'error'`, `'warning'`.

- style (dict; optional):
    The current component's CSS styles.

- value (list of string | numbers | list of list of string | numbers; optional):
    Listens for or sets the selected values.

- variant (a value equal to: 'outlined', 'borderless', 'filled'; optional):
    The variant type, options include `'outlined'`, `'borderless'`, `'filled'`. Where `'outlined'` is equivalent to `bordered=True`, but has higher priority.


## 补充 API 说明

In the default mode, the `options` parameter allows for free nesting through the `children` field to construct any tree structure, with the following valid parameters for each node:

- label (string; required):

  The title content of the current node.

- key (string; optional):

  The unique identifier for the current node.

- value (string or number; required):

  The unique value of the current node.

- children (list; optional):

  Defines the child nodes for the current node.

- disabled (boolean; default False):

  Whether the current node is disabled.
