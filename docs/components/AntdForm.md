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

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：常规居中与行内居中。

#### 代码
```python
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
```

### 批量控制帮助信息

- 说明：为具有有效`id`的表单设置参数`enableBatchControl=True`后，可通过参数`helps`批量控制内部各表单项的帮助信息。

#### 代码
```python
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
```

### 批量控制校验状态

- 说明：为具有有效`id`的表单设置参数`enableBatchControl=True`后，可通过参数`validateStatuses`批量控制内部各表单项的校验状态。

#### 代码
```python
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
```

### 批量控制表单值

- 说明：为具有有效`id`的表单设置参数`enableBatchControl=True`后，可通过参数`values`批量控制内部各表单项的值。

#### 代码
```python
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
```

### 回调控制表单验证

- 说明：配合回调函数，对表单中的各个表单项进行精细化的验证控制。

#### 代码
```python
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
```

### 回调批量监听表单值

- 说明：配合回调函数，对开启批量值控制的表单值进行快捷监听。

#### 代码
```python
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
```

### 基于flex布局分配宽度

- 说明：基于参数`labelCol`、`wrapperCol`的`flex`子参数，实现对表单标签、控件部分宽度的更灵活分配。

#### 代码
```python
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
```

### 表单项标签左对齐

- 说明：设置参数`labelAlign`控制表单项标签对齐方式。

#### 代码
```python
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
```

### 表单项标签超长换行

- 说明：设置参数`labelWrap`控制表单项标签是否超长换行。

#### 代码
```python
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
```

### 其他布局方式

- 说明：设置参数`layout`控制表单布局方式。

#### 代码
```python
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
```

### 表单项添加必填标识

- 说明：设置参数`required`控制表单项标签是否额外添加必填标识。

#### 代码
```python
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
```

### 表单项额外提示信息

- 说明：设置参数`tooltip`为表单项标签添加额外提示信息。

#### 代码
```python
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
```

### 校验状态

- 说明：设置参数`validateStatus`为表单项设置不同的校验状态。

#### 代码
```python
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
```

## API 参数说明

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
