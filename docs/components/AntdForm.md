# AntdForm

## 简介源码：`views/AntdForm/intro.py`
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
                {'title': translator.t('表单')},
                {'title': translator.t('AntdForm 表单')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdForm 表单'), level=2),
        fac.AntdParagraph(
            translator.t('通过嵌套若干AntdFormItem的方式构建现代化表单。')
        ),
    ]

```

## 示例源码（demos）

### `views/AntdForm/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='用户名'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='密码'
                    ),
                    fac.AntdFormItem(
                        fac.AntdCheckbox(label='记住密码'),
                        wrapperCol={'offset': 4},
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('登录', type='primary'),
                        wrapperCol={'offset': 4},
                    ),
                ],
                labelCol={'span': 4},
                wrapperCol={'span': 20},
                style={'width': 300},
            )
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='Username'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='Password'
                    ),
                    fac.AntdFormItem(
                        fac.AntdCheckbox(label='Remember Password'),
                        wrapperCol={'offset': 6},
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('Login', type='primary'),
                        wrapperCol={'offset': 6},
                    ),
                ],
                labelCol={'span': 6},
                wrapperCol={'span': 18},
                style={'width': 300},
            )
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='用户名'),
            fac.AntdFormItem(fac.AntdInput(mode='password'), label='密码'),
            fac.AntdFormItem(
                fac.AntdCheckbox(label='记住密码'), wrapperCol={'offset': 4}
            ),
            fac.AntdFormItem(
                fac.AntdButton('登录', type='primary'),
                wrapperCol={'offset': 4},
            ),
        ],
        labelCol={'span': 4},
        wrapperCol={'span': 20},
        style={'width': 300},
    )
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='Username'),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'), label='Password'
            ),
            fac.AntdFormItem(
                fac.AntdCheckbox(label='Remember Password'),
                wrapperCol={'offset': 6},
            ),
            fac.AntdFormItem(
                fac.AntdButton('Login', type='primary'),
                wrapperCol={'offset': 6},
            ),
        ],
        labelCol={'span': 6},
        wrapperCol={'span': 18},
        style={'width': 300},
    )
)
"""
            }
        ]

```

### `views/AntdForm/demos/batch_help.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(fac.AntdInput(), label=f'表单项{i}')
                for i in range(1, 6)
            ],
            id='batch-helps-form-demo',
            enableBatchControl=True,
            layout='vertical',
            helps={
                f'表单项{i}': f'这是表单项{i}的帮助信息' for i in range(1, 6)
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(fac.AntdInput(), label=f'FormItem{i}')
                for i in range(1, 6)
            ],
            id='batch-helps-form-demo',
            enableBatchControl=True,
            layout='vertical',
            helps={
                f'FormItem{i}': f'This is the help information for FormItem{i}'
                for i in range(1, 6)
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
fac.AntdForm(
    [
        fac.AntdFormItem(fac.AntdInput(), label=f'表单项{i}')
        for i in range(1, 6)
    ],
    id='batch-helps-form-demo',
    enableBatchControl=True,
    layout='vertical',
    helps={f'表单项{i}': f'这是表单项{i}的帮助信息' for i in range(1, 6)},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdForm(
    [
        fac.AntdFormItem(fac.AntdInput(), label=f'FormItem{i}')
        for i in range(1, 6)
    ],
    id='batch-helps-form-demo',
    enableBatchControl=True,
    layout='vertical',
    helps={
        f'FormItem{i}': f'This is the help information for FormItem{i}'
        for i in range(1, 6)
    },
)
"""
            }
        ]

```

### `views/AntdForm/demos/batch_validate_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(), label=f'表单项{i}', hasFeedback=True
                )
                for i in range(1, 6)
            ],
            id='batch-validate-status-form-demo',
            enableBatchControl=True,
            layout='vertical',
            validateStatuses={f'表单项{i}': 'error' for i in range(1, 6)},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(), label=f'FormItem{i}', hasFeedback=True
                )
                for i in range(1, 6)
            ],
            id='batch-validate-status-form-demo',
            enableBatchControl=True,
            layout='vertical',
            validateStatuses={f'FormItem{i}': 'error' for i in range(1, 6)},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdForm(
    [
        fac.AntdFormItem(
            fac.AntdInput(), label=f'表单项{i}', hasFeedback=True
        )
        for i in range(1, 6)
    ],
    id='batch-validate-status-form-demo',
    enableBatchControl=True,
    layout='vertical',
    validateStatuses={f'表单项{i}': 'error' for i in range(1, 6)},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdForm(
    [
        fac.AntdFormItem(
            fac.AntdInput(), label=f'FormItem{i}', hasFeedback=True
        )
        for i in range(1, 6)
    ],
    id='batch-validate-status-form-demo',
    enableBatchControl=True,
    layout='vertical',
    validateStatuses={f'FormItem{i}': 'error' for i in range(1, 6)},
)
"""
            }
        ]

```

### `views/AntdForm/demos/batch_value.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(name=f'表单项{i}'), label=f'表单项{i}'
                )
                for i in range(1, 6)
            ],
            id='batch-value-form-demo',
            enableBatchControl=True,
            layout='vertical',
            values={
                f'表单项{i}': f'这是表单项{i}的设定值' for i in range(1, 6)
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(name=f'FormItem{i}'), label=f'FormItem{i}'
                )
                for i in range(1, 6)
            ],
            id='batch-value-form-demo',
            enableBatchControl=True,
            layout='vertical',
            values={
                f'FormItem{i}': f'This is the preset value for FormItem{i}'
                for i in range(1, 6)
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
fac.AntdForm(
    [
        fac.AntdFormItem(
            fac.AntdInput(name=f'表单项{i}'), label=f'表单项{i}'
        )
        for i in range(1, 6)
    ],
    id='batch-value-form-demo',
    enableBatchControl=True,
    layout='vertical',
    values={f'表单项{i}': f'这是表单项{i}的设定值' for i in range(1, 6)},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdForm(
    [
        fac.AntdFormItem(
            fac.AntdInput(name=f'FormItem{i}'), label=f'FormItem{i}'
        )
        for i in range(1, 6)
    ],
    id='batch-value-form-demo',
    enableBatchControl=True,
    layout='vertical',
    values={
        f'FormItem{i}': f'This is the preset value for FormItem{i}'
        for i in range(1, 6)
    },
)
"""
            }
        ]

```

### `views/AntdForm/demos/callback_control_validate.py`
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
        demo_contents = fac.AntdCenter(
            fac.AntdSpace(
                [
                    fac.AntdAlert(
                        message='示例用户名：fac  密码：123456 你可以故意输错用户名或密码来查看不同的校验反馈结果',
                        type='info',
                        showIcon=True,
                        messageRenderMode='marquee',
                        style={'marginBottom': '10px'},
                    ),
                    fac.AntdForm(
                        [
                            fac.AntdFormItem(
                                fac.AntdInput(
                                    id='form-item-validate-demo-username'
                                ),
                                id='form-item-validate-demo-username-container',
                                label='用户名',
                            ),
                            fac.AntdFormItem(
                                fac.AntdInput(
                                    id='form-item-validate-demo-password',
                                    mode='password',
                                ),
                                id='form-item-validate-demo-password-container',
                                label='密码',
                            ),
                            fac.AntdFormItem(
                                fac.AntdButton(
                                    '登录',
                                    id='form-item-validate-demo-submit',
                                    type='primary',
                                )
                            ),
                        ],
                        layout='vertical',
                    ),
                ],
                direction='vertical',
                style={'width': 400},
            ),
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdSpace(
                [
                    fac.AntdAlert(
                        message='Example username: fac Password: 123456 You can intentionally enter the wrong username or password to see different validation feedback results.',
                        type='info',
                        showIcon=True,
                        messageRenderMode='marquee',
                        style={'marginBottom': '10px'},
                    ),
                    fac.AntdForm(
                        [
                            fac.AntdFormItem(
                                fac.AntdInput(
                                    id='form-item-validate-demo-username'
                                ),
                                id='form-item-validate-demo-username-container',
                                label='Username',
                            ),
                            fac.AntdFormItem(
                                fac.AntdInput(
                                    id='form-item-validate-demo-password',
                                    mode='password',
                                ),
                                id='form-item-validate-demo-password-container',
                                label='Password',
                            ),
                            fac.AntdFormItem(
                                fac.AntdButton(
                                    'Login',
                                    id='form-item-validate-demo-submit',
                                    type='primary',
                                )
                            ),
                        ],
                        layout='vertical',
                    ),
                ],
                direction='vertical',
                style={'width': 400},
            ),
        )

    return demo_contents


@app.callback(
    [
        Output('form-item-validate-demo-username-container', 'validateStatus'),
        Output('form-item-validate-demo-password-container', 'validateStatus'),
        Output('form-item-validate-demo-username-container', 'help'),
        Output('form-item-validate-demo-password-container', 'help'),
    ],
    Input('form-item-validate-demo-submit', 'nClicks'),
    [
        State('form-item-validate-demo-username', 'value'),
        State('form-item-validate-demo-password', 'value'),
    ],
    prevent_initial_call=True,
)
def form_item_validate_demo(nClicks, username, password):
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        if username and password:
            return [
                None if username == 'fac' else 'error',
                ('success' if password == '123456' else 'error')
                if username == 'fac'
                else None,
                None if username == 'fac' else '用户不存在！',
                ('密码正确！' if password == '123456' else '密码错误！')
                if username == 'fac'
                else None,
            ]

        return [
            None if username else 'error',
            None if password else 'error',
            None if username else '用户名不能为空！',
            None if password else '密码不能为空！',
        ]

    elif current_locale == 'en-us':
        if username and password:
            return [
                None if username == 'fac' else 'error',
                ('success' if password == '123456' else 'error')
                if username == 'fac'
                else None,
                None if username == 'fac' else 'User does not exist!',
                (
                    'Password correct!'
                    if password == '123456'
                    else 'Password error!'
                )
                if username == 'fac'
                else None,
            ]

        return [
            None if username else 'error',
            None if password else 'error',
            None if username else 'Username cannot be empty!',
            None if password else 'Password cannot be empty!',
        ]


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdSpace(
        [
            fac.AntdAlert(
                message='示例用户名：fac  密码：123456 你可以故意输错用户名或密码来查看不同的校验反馈结果',
                type='info',
                showIcon=True,
                messageRenderMode='marquee',
                style={'marginBottom': '10px'},
            ),
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(
                            id='form-item-validate-demo-username'
                        ),
                        id='form-item-validate-demo-username-container',
                        label='用户名',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(
                            id='form-item-validate-demo-password',
                            mode='password',
                        ),
                        id='form-item-validate-demo-password-container',
                        label='密码',
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton(
                            '登录',
                            id='form-item-validate-demo-submit',
                            type='primary',
                        )
                    ),
                ],
                layout='vertical',
            ),
        ],
        direction='vertical',
        style={'width': 400},
    ),
)

...

@app.callback(
    [
        Output('form-item-validate-demo-username-container', 'validateStatus'),
        Output('form-item-validate-demo-password-container', 'validateStatus'),
        Output('form-item-validate-demo-username-container', 'help'),
        Output('form-item-validate-demo-password-container', 'help'),
    ],
    Input('form-item-validate-demo-submit', 'nClicks'),
    [
        State('form-item-validate-demo-username', 'value'),
        State('form-item-validate-demo-password', 'value'),
    ],
    prevent_initial_call=True,
)
def form_item_validate_demo(nClicks, username, password):
    if username and password:
        return [
            None if username == 'fac' else 'error',
            ('success' if password == '123456' else 'error')
            if username == 'fac'
            else None,
            None if username == 'fac' else '用户不存在！',
            ('密码正确！' if password == '123456' else '密码错误！')
            if username == 'fac'
            else None,
        ]

    return [
        None if username else 'error',
        None if password else 'error',
        None if username else '用户名不能为空！',
        None if password else '密码不能为空！',
    ]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdSpace(
        [
            fac.AntdAlert(
                message='Example username: fac Password: 123456 You can intentionally enter the wrong username or password to see different validation feedback results.',
                type='info',
                showIcon=True,
                messageRenderMode='marquee',
                style={'marginBottom': '10px'},
            ),
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(
                            id='form-item-validate-demo-username'
                        ),
                        id='form-item-validate-demo-username-container',
                        label='Username',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(
                            id='form-item-validate-demo-password',
                            mode='password',
                        ),
                        id='form-item-validate-demo-password-container',
                        label='Password',
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton(
                            'Login',
                            id='form-item-validate-demo-submit',
                            type='primary',
                        )
                    ),
                ],
                layout='vertical',
            ),
        ],
        direction='vertical',
        style={'width': 400},
    ),
)

...

@app.callback(
    [
        Output('form-item-validate-demo-username-container', 'validateStatus'),
        Output('form-item-validate-demo-password-container', 'validateStatus'),
        Output('form-item-validate-demo-username-container', 'help'),
        Output('form-item-validate-demo-password-container', 'help'),
    ],
    Input('form-item-validate-demo-submit', 'nClicks'),
    [
        State('form-item-validate-demo-username', 'value'),
        State('form-item-validate-demo-password', 'value'),
    ],
    prevent_initial_call=True,
)
def form_item_validate_demo(nClicks, username, password):
    if username and password:
        return [
            None if username == 'fac' else 'error',
            ('success' if password == '123456' else 'error')
            if username == 'fac'
            else None,
            None if username == 'fac' else 'User does not exist!',
            (
                'Password correct!'
                if password == '123456'
                else 'Password error!'
            )
            if username == 'fac'
            else None,
        ]

    return [
        None if username else 'error',
        None if password else 'error',
        None if username else 'Username cannot be empty!',
        None if password else 'Password cannot be empty!',
    ]
"""
            }
        ]

```

### `views/AntdForm/demos/callback_listen_values.py`
```python
import json
from dash import html
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
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(name=f'表单项{i}'), label=f'表单项{i}'
                        )
                        for i in range(1, 6)
                    ],
                    id='callback-listen-value-form-demo',
                    enableBatchControl=True,
                    layout='vertical',
                    values={
                        f'表单项{i}': f'这是表单项{i}的设定值'
                        for i in range(1, 6)
                    },
                ),
                html.Pre(id='callback-listen-value-form-demo-output'),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(name=f'FormItem{i}'),
                            label=f'FormItem{i}',
                        )
                        for i in range(1, 6)
                    ],
                    id='callback-listen-value-form-demo',
                    enableBatchControl=True,
                    layout='vertical',
                    values={
                        f'FormItem{i}': f'This is the preset value for FormItem{i}'
                        for i in range(1, 6)
                    },
                ),
                html.Pre(id='callback-listen-value-form-demo-output'),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


@app.callback(
    Output('callback-listen-value-form-demo-output', 'children'),
    Input('callback-listen-value-form-demo', 'values'),
)
def callback_listen_value_demo(values):
    return json.dumps(values, ensure_ascii=False, indent=4)


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(name=f'表单项{i}'), label=f'表单项{i}'
                )
                for i in range(1, 6)
            ],
            id='callback-listen-value-form-demo',
            enableBatchControl=True,
            layout='vertical',
            values={
                f'表单项{i}': f'这是表单项{i}的设定值' for i in range(1, 6)
            },
        ),
        html.Pre(id='callback-listen-value-form-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('callback-listen-value-form-demo-output', 'children'),
    Input('callback-listen-value-form-demo', 'values'),
)
def callback_listen_value_demo(values):
    return json.dumps(values, ensure_ascii=False, indent=4)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(name=f'FormItem{i}'),
                    label=f'FormItem{i}',
                )
                for i in range(1, 6)
            ],
            id='callback-listen-value-form-demo',
            enableBatchControl=True,
            layout='vertical',
            values={
                f'FormItem{i}': f'This is the preset value for FormItem{i}'
                for i in range(1, 6)
            },
        ),
        html.Pre(id='callback-listen-value-form-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('callback-listen-value-form-demo-output', 'children'),
    Input('callback-listen-value-form-demo', 'values'),
)
def callback_listen_value_demo(values):
    return json.dumps(values, ensure_ascii=False, indent=4)
"""
            }
        ]

```

### `views/AntdForm/demos/flex_layout.py`
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
            fac.AntdDivider('AntdForm整体配置', innerTextOrientation='left'),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(), label='表单' + '项' * i
                        )
                        for i in range(1, 4)
                    ],
                    labelCol={'flex': 'none'},
                    wrapperCol={'flex': 'auto'},
                    style={'width': 300},
                )
            ),
            fac.AntdDivider(
                'AntdFormItem独立配置', innerTextOrientation='left'
            ),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(),
                            label='示例1',
                            labelCol={'flex': '1'},
                            wrapperCol={'flex': '1'},
                        ),
                        fac.AntdFormItem(
                            fac.AntdInput(),
                            label='示例2',
                            labelCol={'flex': 'none'},
                            wrapperCol={'flex': 'auto'},
                        ),
                    ],
                    style={'width': 300},
                )
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'AntdForm Global Configuration', innerTextOrientation='left'
            ),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(), label='Form' + ' Item' * i
                        )
                        for i in range(1, 4)
                    ],
                    labelCol={'flex': 'none'},
                    wrapperCol={'flex': 'auto'},
                    style={'width': 300},
                )
            ),
            fac.AntdDivider(
                'AntdFormItem Individual Configuration',
                innerTextOrientation='left',
            ),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(),
                            label='Example 1',
                            labelCol={'flex': '1'},
                            wrapperCol={'flex': '1'},
                        ),
                        fac.AntdFormItem(
                            fac.AntdInput(),
                            label='Example 2',
                            labelCol={'flex': 'none'},
                            wrapperCol={'flex': 'auto'},
                        ),
                    ],
                    style={'width': 300},
                )
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
    fac.AntdDivider('AntdForm整体配置', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(fac.AntdInput(), label='表单' + '项' * i)
                for i in range(1, 4)
            ],
            labelCol={'flex': 'none'},
            wrapperCol={'flex': 'auto'},
            style={'width': 300},
        )
    ),
    fac.AntdDivider('AntdFormItem独立配置', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(),
                    label='示例1',
                    labelCol={'flex': '1'},
                    wrapperCol={'flex': '1'},
                ),
                fac.AntdFormItem(
                    fac.AntdInput(),
                    label='示例2',
                    labelCol={'flex': 'none'},
                    wrapperCol={'flex': 'auto'},
                ),
            ],
            style={'width': 300},
        )
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
        'AntdForm Global Configuration', innerTextOrientation='left'
    ),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(), label='Form' + ' Item' * i
                )
                for i in range(1, 4)
            ],
            labelCol={'flex': 'none'},
            wrapperCol={'flex': 'auto'},
            style={'width': 300},
        )
    ),
    fac.AntdDivider(
        'AntdFormItem Individual Configuration',
        innerTextOrientation='left',
    ),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(),
                    label='Example 1',
                    labelCol={'flex': '1'},
                    wrapperCol={'flex': '1'},
                ),
                fac.AntdFormItem(
                    fac.AntdInput(),
                    label='Example 2',
                    labelCol={'flex': 'none'},
                    wrapperCol={'flex': 'auto'},
                ),
            ],
            style={'width': 300},
        )
    ),
]
"""
            }
        ]

```

### `views/AntdForm/demos/label_align_left.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='用户名'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='密码'
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('登录', type='primary'),
                        wrapperCol={'offset': 4},
                    ),
                ],
                labelCol={'span': 4},
                wrapperCol={'span': 20},
                labelAlign='left',
                style={'width': 300},
            )
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='Username'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='Password'
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('Login', type='primary'),
                        wrapperCol={'offset': 6},
                    ),
                ],
                labelCol={'span': 6},
                wrapperCol={'span': 18},
                labelAlign='left',
                style={'width': 300},
            )
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='用户名'),
            fac.AntdFormItem(fac.AntdInput(mode='password'), label='密码'),
            fac.AntdFormItem(
                fac.AntdButton('登录', type='primary'),
                wrapperCol={'offset': 4},
            ),
        ],
        labelCol={'span': 4},
        wrapperCol={'span': 20},
        labelAlign='left',
        style={'width': 300},
    )
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='Username'),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'), label='Password'
            ),
            fac.AntdFormItem(
                fac.AntdButton('Login', type='primary'),
                wrapperCol={'offset': 6},
            ),
        ],
        labelCol={'span': 6},
        wrapperCol={'span': 18},
        labelAlign='left',
        style={'width': 300},
    )
)
"""
            }
        ]

```

### `views/AntdForm/demos/label_wrap.py`
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
                'labelWrap=False（默认）', innerTextOrientation='left'
            ),
            fac.AntdCenter(
                fac.AntdForm(
                    [fac.AntdFormItem(fac.AntdInput(), label='超长标签' * 2)],
                    labelCol={'span': 6},
                    labelAlign='left',
                    style={'width': 300},
                )
            ),
            fac.AntdDivider('labelWrap=True', innerTextOrientation='left'),
            fac.AntdCenter(
                fac.AntdForm(
                    [fac.AntdFormItem(fac.AntdInput(), label='超长标签' * 2)],
                    labelCol={'span': 6},
                    labelAlign='left',
                    labelWrap=True,
                    style={'width': 300},
                )
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider(
                'labelWrap=False (default)', innerTextOrientation='left'
            ),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(), label=('Extra Long Label')
                        )
                    ],
                    labelCol={'span': 6},
                    labelAlign='left',
                    style={'width': 300},
                )
            ),
            fac.AntdDivider('labelWrap=True', innerTextOrientation='left'),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(
                            fac.AntdInput(), label=('Extra Long Label')
                        )
                    ],
                    labelCol={'span': 6},
                    labelAlign='left',
                    labelWrap=True,
                    style={'width': 300},
                )
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
    fac.AntdDivider('labelWrap=False（默认）', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [fac.AntdFormItem(fac.AntdInput(), label='超长标签' * 2)],
            labelCol={'span': 6},
            labelAlign='left',
            style={'width': 300},
        )
    ),
    fac.AntdDivider('labelWrap=True', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [fac.AntdFormItem(fac.AntdInput(), label='超长标签' * 2)],
            labelCol={'span': 6},
            labelAlign='left',
            labelWrap=True,
            style={'width': 300},
        )
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
        'labelWrap=False (default)', innerTextOrientation='left'
    ),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(), label=('Extra Long Label')
                )
            ],
            labelCol={'span': 6},
            labelAlign='left',
            style={'width': 300},
        )
    ),
    fac.AntdDivider('labelWrap=True', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(), label=('Extra Long Label')
                )
            ],
            labelCol={'span': 6},
            labelAlign='left',
            labelWrap=True,
            style={'width': 300},
        )
    ),
]
"""
            }
        ]

```

### `views/AntdForm/demos/layout.py`
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
            fac.AntdDivider('layout="vertical"', innerTextOrientation='left'),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(fac.AntdInput(), label='用户名'),
                        fac.AntdFormItem(
                            fac.AntdInput(mode='password'), label='密码'
                        ),
                        fac.AntdFormItem(
                            fac.AntdButton('登录', type='primary')
                        ),
                    ],
                    layout='vertical',
                    style={'width': 300},
                )
            ),
            fac.AntdDivider('layout="inline"', innerTextOrientation='left'),
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='用户名'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='密码'
                    ),
                    fac.AntdFormItem(fac.AntdButton('登录', type='primary')),
                ],
                layout='inline',
                style={'justifyContent': 'center'},
            ),
        ]

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = [
            fac.AntdDivider('layout="vertical"', innerTextOrientation='left'),
            fac.AntdCenter(
                fac.AntdForm(
                    [
                        fac.AntdFormItem(fac.AntdInput(), label='Username'),
                        fac.AntdFormItem(
                            fac.AntdInput(mode='password'), label='Password'
                        ),
                        fac.AntdFormItem(
                            fac.AntdButton('Login', type='primary')
                        ),
                    ],
                    layout='vertical',
                    style={'width': 300},
                )
            ),
            fac.AntdDivider('layout="inline"', innerTextOrientation='left'),
            fac.AntdForm(
                [
                    fac.AntdFormItem(fac.AntdInput(), label='Username'),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'), label='Password'
                    ),
                    fac.AntdFormItem(fac.AntdButton('Login', type='primary')),
                ],
                layout='inline',
                style={'justifyContent': 'center'},
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
    fac.AntdDivider('layout="vertical"', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(fac.AntdInput(), label='用户名'),
                fac.AntdFormItem(
                    fac.AntdInput(mode='password'), label='密码'
                ),
                fac.AntdFormItem(fac.AntdButton('登录', type='primary')),
            ],
            layout='vertical',
            style={'width': 300},
        )
    ),
    fac.AntdDivider('layout="inline"', innerTextOrientation='left'),
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='用户名'),
            fac.AntdFormItem(fac.AntdInput(mode='password'), label='密码'),
            fac.AntdFormItem(fac.AntdButton('登录', type='primary')),
        ],
        layout='inline',
        style={'justifyContent': 'center'},
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
    fac.AntdDivider('layout="vertical"', innerTextOrientation='left'),
    fac.AntdCenter(
        fac.AntdForm(
            [
                fac.AntdFormItem(fac.AntdInput(), label='Username'),
                fac.AntdFormItem(
                    fac.AntdInput(mode='password'), label='Password'
                ),
                fac.AntdFormItem(
                    fac.AntdButton('Login', type='primary')
                ),
            ],
            layout='vertical',
            style={'width': 300},
        )
    ),
    fac.AntdDivider('layout="inline"', innerTextOrientation='left'),
    fac.AntdForm(
        [
            fac.AntdFormItem(fac.AntdInput(), label='Username'),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'), label='Password'
            ),
            fac.AntdFormItem(fac.AntdButton('Login', type='primary')),
        ],
        layout='inline',
        style={'justifyContent': 'center'},
    ),
]
"""
            }
        ]

```

### `views/AntdForm/demos/required.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(), label='用户名', required=True
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'),
                        label='密码',
                        required=True,
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('登录', type='primary'),
                        wrapperCol={'offset': 5},
                    ),
                ],
                labelCol={'span': 5},
                wrapperCol={'span': 19},
                style={'width': 300},
            )
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(), label='Username', required=True
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'),
                        label='Password',
                        required=True,
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('Login', type='primary'),
                        wrapperCol={'offset': 7},
                    ),
                ],
                labelCol={'span': 7},
                wrapperCol={'span': 17},
                style={'width': 300},
            )
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdInput(), label='用户名', required=True
            ),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'), label='密码', required=True
            ),
            fac.AntdFormItem(
                fac.AntdButton('登录', type='primary'),
                wrapperCol={'offset': 5},
            ),
        ],
        labelCol={'span': 5},
        wrapperCol={'span': 19},
        style={'width': 300},
    )
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdInput(), label='Username', required=True
            ),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'),
                label='Password',
                required=True,
            ),
            fac.AntdFormItem(
                fac.AntdButton('Login', type='primary'),
                wrapperCol={'offset': 6},
            ),
        ],
        labelCol={'span': 6},
        wrapperCol={'span': 18},
        style={'width': 300},
    )
)
"""
            }
        ]

```

### `views/AntdForm/demos/tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(),
                        label='用户名',
                        tooltip='输入您的用户名信息',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'),
                        label='密码',
                        tooltip='输入您的账户密码信息',
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('登录', type='primary'),
                        wrapperCol={'offset': 6},
                    ),
                ],
                labelCol={'span': 6},
                wrapperCol={'span': 18},
                style={'width': 300},
            )
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInput(),
                        label='Username',
                        tooltip='Enter your username information',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(mode='password'),
                        label='Password',
                        tooltip='Enter your account password information',
                    ),
                    fac.AntdFormItem(
                        fac.AntdButton('Login', type='primary'),
                        wrapperCol={'offset': 8},
                    ),
                ],
                labelCol={'span': 8},
                wrapperCol={'span': 16},
                style={'width': 300},
            )
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdInput(),
                label='用户名',
                tooltip='输入您的用户名信息',
            ),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'),
                label='密码',
                tooltip='输入您的账户密码信息',
            ),
            fac.AntdFormItem(
                fac.AntdButton('登录', type='primary'),
                wrapperCol={'offset': 6},
            ),
        ],
        labelCol={'span': 6},
        wrapperCol={'span': 18},
        style={'width': 300},
    )
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdInput(),
                label='Username',
                tooltip='Enter your username information',
            ),
            fac.AntdFormItem(
                fac.AntdInput(mode='password'),
                label='Password',
                tooltip='Enter your account password information',
            ),
            fac.AntdFormItem(
                fac.AntdButton('Login', type='primary'),
                wrapperCol={'offset': 8},
            ),
        ],
        labelCol={'span': 8},
        wrapperCol={'span': 16},
        style={'width': 300},
    )
)
"""
            }
        ]

```

### `views/AntdForm/demos/validate_status.py`
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
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdRadioGroup(
                            id='form-item-status-switch',
                            options=[
                                {'label': 'None', 'value': 'None'},
                                {
                                    'label': 'success',
                                    'value': 'success',
                                },
                                {
                                    'label': 'warning',
                                    'value': 'warning',
                                },
                                {
                                    'label': 'error',
                                    'value': 'error',
                                },
                                {
                                    'label': 'validating',
                                    'value': 'validating',
                                },
                            ],
                            optionType='button',
                            defaultValue='None',
                        ),
                        label='切换状态',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(),
                        id='form-item-status-demo',
                        label='用户名',
                        hasFeedback=True,
                    ),
                ],
                labelCol={'span': 4},
                wrapperCol={'span': 20},
                style={'width': 500},
            )
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdCenter(
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdRadioGroup(
                            id='form-item-status-switch',
                            options=[
                                {'label': 'None', 'value': 'None'},
                                {
                                    'label': 'success',
                                    'value': 'success',
                                },
                                {
                                    'label': 'warning',
                                    'value': 'warning',
                                },
                                {
                                    'label': 'error',
                                    'value': 'error',
                                },
                                {
                                    'label': 'validating',
                                    'value': 'validating',
                                },
                            ],
                            optionType='button',
                            defaultValue='None',
                        ),
                        label='Switch status',
                    ),
                    fac.AntdFormItem(
                        fac.AntdInput(),
                        id='form-item-status-demo',
                        label='Username',
                        hasFeedback=True,
                    ),
                ],
                labelCol={'span': 5},
                wrapperCol={'span': 19},
                style={'width': 500},
            )
        )

    return demo_contents


@app.callback(
    [
        Output('form-item-status-demo', 'validateStatus'),
        Output('form-item-status-demo', 'help'),
    ],
    Input('form-item-status-switch', 'value'),
)
def form_item_status_demo(value):
    if not value or value == 'None':
        return None, None

    return value, f'validateStatus="{value}"'


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdRadioGroup(
                    id='form-item-status-switch',
                    options=[
                        {'label': 'None', 'value': 'None'},
                        {
                            'label': 'success',
                            'value': 'success',
                        },
                        {
                            'label': 'warning',
                            'value': 'warning',
                        },
                        {
                            'label': 'error',
                            'value': 'error',
                        },
                        {
                            'label': 'validating',
                            'value': 'validating',
                        },
                    ],
                    optionType='button',
                    defaultValue='None',
                ),
                label='切换状态',
            ),
            fac.AntdFormItem(
                fac.AntdInput(),
                id='form-item-status-demo',
                label='用户名',
                hasFeedback=True,
            ),
        ],
        labelCol={'span': 4},
        wrapperCol={'span': 20},
        style={'width': 500},
    )
)

...

@app.callback(
    [
        Output('form-item-status-demo', 'validateStatus'),
        Output('form-item-status-demo', 'help'),
    ],
    Input('form-item-status-switch', 'value'),
)
def form_item_status_demo(value):
    if not value or value == 'None':
        return None, None

    return value, f'validateStatus="{value}"'
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdCenter(
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdRadioGroup(
                    id='form-item-status-switch',
                    options=[
                        {'label': 'None', 'value': 'None'},
                        {
                            'label': 'success',
                            'value': 'success',
                        },
                        {
                            'label': 'warning',
                            'value': 'warning',
                        },
                        {
                            'label': 'error',
                            'value': 'error',
                        },
                        {
                            'label': 'validating',
                            'value': 'validating',
                        },
                    ],
                    optionType='button',
                    defaultValue='None',
                ),
                label='Switch status',
            ),
            fac.AntdFormItem(
                fac.AntdInput(),
                id='form-item-status-demo',
                label='Username',
                hasFeedback=True,
            ),
        ],
        labelCol={'span': 5},
        wrapperCol={'span': 19},
        style={'width': 500},
    )
)

...

@app.callback(
    [
        Output('form-item-status-demo', 'validateStatus'),
        Output('form-item-status-demo', 'help'),
    ],
    Input('form-item-status-switch', 'value'),
)
def form_item_status_demo(value):
    if not value or value == 'None':
        return None, None

    return value, f'validateStatus="{value}"'
"""
            }
        ]

```

## API 文档

- id (string; optional):
    The unique identifier for the component.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the component.

- children (a list of or a singular dash component, string or number; optional):
    The component type, embedding related `AntdFormItem` components or common form input components.

- style (dict; optional):
    The CSS style of the current component.

- className (string | dict; optional):
    The CSS class name of the current component, supporting [dynamic CSS](/advanced-classname).

- layout (a value equal to: 'horizontal', 'vertical', 'inline'; default 'horizontal'):
    The form layout mode, with options `'horizontal'`, `'vertical'`, `'inline'`.
    Default value: `'horizontal'`.

- labelCol (dict; optional):
    Configures the label part of the form item.

    `labelCol` is a dict with keys:

    - span (number; optional):
        The fraction of the total width (total of 24) that the label part occupies.

    - offset (number; optional):
        The fraction of the width that the label part is offset to the right.

    - flex (string | number; optional):
        Similar to the flex property in CSS, used to more flexibly control the width occupied by the label part.

- wrapperCol (dict; optional):
    Configures the control part of the form item.

    `wrapperCol` is a dict with keys:

    - span (number; optional):
        The fraction of the total width (total of 24) that the control part occupies.

    - offset (number; optional):
        The fraction of the width that the control part is offset to the right.

    - flex (string | number; optional):
        Similar to the flex property in CSS, used to more flexibly control the width occupied by the control part.

- colon (boolean; default True):
    When `layout='horizontal'`, controls whether to add a colon at the end of the label part of the form item.

- labelAlign (a value equal to: 'left', 'right'; default 'right'):
    The text alignment of the label part of the form item, with options `'left'`, `'right'`. Default value: `'right'`.

- labelWrap (boolean; default False):
    Whether to allow wrapping for excessively long form item labels. Default value: `False`.

- enableBatchControl (boolean; default False):
    Whether to enable batch control functionality for the form, which may result in some performance loss. Default value: `False`.

- values (dict; optional):
    When `enableBatchControl=True`, can be used to listen to or set the input value changes of internal form input components, after which the `defaultValue`, `value` parameters of the internal form input components will become ineffective.

- validateStatuses (dict with strings as keys and values of type a value equal to: 'success', 'warning', 'error', 'validating'; optional):
    When `enableBatchControl=True`, can be used to uniformly set the `validateStatus` values of internal `AntdFormItem` components, with keys as the `label` values of the corresponding `AntdFormItem` components, with lower priority than the `validateStatus` values of each `AntdFormItem` component.

- helps (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    When `enableBatchControl=True`, can be used to uniformly set the `help` values of internal `AntdFormItem` components, with keys as the `label` values of the corresponding `AntdFormItem` components, with lower priority than the `help` values of each `AntdFormItem` component.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
