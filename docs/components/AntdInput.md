# AntdInput

## 简介源码：`views/AntdInput/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdInput 输入框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdInput 输入框', level=2),
        fac.AntdParagraph('为用户提供不同形式的文本信息录入功能。'),
    ]

```

## 示例源码（demos）

### `views/AntdInput/demos/addon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                addonBefore='前缀元素示例',
                addonAfter='后缀元素示例',
            ),
            fac.AntdInput(
                addonBefore=fac.AntdSelect(
                    defaultValue='http://',
                    options=[
                        {'label': option, 'value': option}
                        for option in ['http://', 'https://']
                    ],
                    allowClear=False,
                ),
                addonAfter=fac.AntdSelect(
                    defaultValue='.com',
                    options=[
                        {'label': option, 'value': option}
                        for option in ['.com', '.cn']
                    ],
                    allowClear=False,
                ),
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            addonBefore='前缀元素示例',
            addonAfter='后缀元素示例',
        ),
        fac.AntdInput(
            addonBefore=fac.AntdSelect(
                defaultValue='http://',
                options=[
                    {'label': option, 'value': option}
                    for option in ['http://', 'https://']
                ],
                allowClear=False,
            ),
            addonAfter=fac.AntdSelect(
                defaultValue='.com',
                options=[
                    {'label': option, 'value': option}
                    for option in ['.com', '.cn']
                ],
                allowClear=False,
            ),
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
    }
]

```

### `views/AntdInput/demos/allow_clear.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                value='内容',
                placeholder='mode="default"（默认）',
                allowClear=True,
            ),
            fac.AntdInput(
                value='内容',
                placeholder='mode="search"',
                mode='search',
                allowClear=True,
            ),
            fac.AntdInput(
                value='内容',
                placeholder='mode="text-area"',
                mode='text-area',
                allowClear=True,
            ),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            value='内容',
            placeholder='mode="default"（默认）',
            allowClear=True,
        ),
        fac.AntdInput(
            value='内容',
            placeholder='mode="search"',
            mode='search',
            allowClear=True,
        ),
        fac.AntdInput(
            value='内容',
            placeholder='mode="text-area"',
            mode='text-area',
            allowClear=True,
        ),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/auto_size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider(
                'autoSize=False（默认）', innerTextOrientation='left'
            ),
            fac.AntdInput(
                mode='text-area',
                defaultValue='示例内容' * 20,
                style={'width': 350},
            ),
            fac.AntdDivider(
                'autoSize=True（跟随行数扩展高度）', innerTextOrientation='left'
            ),
            fac.AntdInput(
                mode='text-area',
                defaultValue='示例内容' * 20,
                autoSize=True,
                style={'width': 350},
            ),
            fac.AntdDivider(
                '配置minRows、maxRows参数',
                innerTextOrientation='left',
            ),
            fac.AntdInput(
                mode='text-area',
                defaultValue='示例内容' * 20,
                autoSize={'minRows': 2, 'maxRows': 3},
                style={'width': 350},
            ),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider(
            'autoSize=False（默认）', innerTextOrientation='left'
        ),
        fac.AntdInput(
            mode='text-area',
            defaultValue='示例内容' * 20,
            style={'width': 350},
        ),
        fac.AntdDivider(
            'autoSize=True（跟随行数扩展高度）', innerTextOrientation='left'
        ),
        fac.AntdInput(
            mode='text-area',
            defaultValue='示例内容' * 20,
            autoSize=True,
            style={'width': 350},
        ),
        fac.AntdDivider(
            '配置minRows、maxRows参数',
            innerTextOrientation='left',
        ),
        fac.AntdInput(
            mode='text-area',
            defaultValue='示例内容' * 20,
            autoSize={'minRows': 2, 'maxRows': 3},
            style={'width': 350},
        ),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdInput(
                        id=f'input-{mode}-mode-demo',
                        placeholder=f'mode="{mode}"{"（默认）" if mode == "default" else ""}',
                        mode=mode,
                    )
                    for mode in ['default', 'search', 'text-area', 'password']
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            fac.AntdCard(
                id='input-demo-output', styles={'header': {'display': 'none'}}
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


@app.callback(
    Output('input-demo-output', 'children'),
    [
        Input(f'input-{mode}-mode-demo', 'value')
        for mode in ['default', 'search', 'text-area', 'password']
    ],
)
def input_mode_demo(*value_list):
    return fac.AntdSpace(
        [
            fac.AntdText(f'{mode}模式value：{value_list[i]}')
            for i, mode in enumerate(
                ['default', 'search', 'text-area', 'password']
            )
        ],
        direction='vertical',
    )


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdInput(
                    id=f'input-{mode}-mode-demo',
                    placeholder=f'mode="{mode}"{"（默认）" if mode == "default" else ""}',
                    mode=mode,
                )
                for mode in ['default', 'search', 'text-area', 'password']
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        fac.AntdCard(
            id='input-demo-output', styles={'header': {'display': 'none'}}
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

@app.callback(
    Output('input-demo-output', 'children'),
    [
        Input(f'input-{mode}-mode-demo', 'value')
        for mode in ['default', 'search', 'text-area', 'password']
    ],
)
def input_mode_demo(*value_list):
    return fac.AntdSpace(
        [
            fac.AntdText(f'{mode}模式value：{value_list[i]}')
            for i, mode in enumerate(
                ['default', 'search', 'text-area', 'password']
            )
        ],
        direction='vertical',
    )
"""
    }
]

```

### `views/AntdInput/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(placeholder='mode="default"（默认）'),
            fac.AntdInput(placeholder='mode="search"', mode='search'),
            fac.AntdInput(placeholder='mode="text-area"', mode='text-area'),
            fac.AntdInput(placeholder='mode="password"', mode='password'),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(placeholder='mode="default"（默认）'),
        fac.AntdInput(placeholder='mode="search"', mode='search'),
        fac.AntdInput(placeholder='mode="text-area"', mode='text-area'),
        fac.AntdInput(placeholder='mode="password"', mode='password'),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/border.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(bordered=True, placeholder='bordered=True（默认）'),
            fac.AntdInput(bordered=False, placeholder='bordered=False'),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(bordered=True, placeholder='bordered=True（默认）'),
        fac.AntdInput(bordered=False, placeholder='bordered=False'),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/count_format.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                mode='text-area',
                showCount=True,
                placeholder='仅匹配连续的大小写字母（单词）为1个字符',
                countFormat='[a-zA-Z]+',
                style={'width': 350},
            ),
            fac.AntdInput(
                mode='text-area',
                showCount=True,
                placeholder='仅计数汉字',
                countFormat='[\u4e00-\u9fff]',
                style={'width': 350},
            ),
        ],
        direction='vertical',
        size='large',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            mode='text-area',
            showCount=True,
            placeholder='仅匹配连续的大小写字母（单词）为1个字符',
            countFormat='[a-zA-Z]+',
            style={'width': 350},
        ),
        fac.AntdInput(
            mode='text-area',
            showCount=True,
            placeholder='仅计数汉字',
            countFormat='[\u4e00-\u9fff]',
            style={'width': 350},
        ),
    ],
    direction='vertical',
    size='large',
)
"""
    }
]

```

### `views/AntdInput/demos/debounce_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app
from dash import html


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdText('当前debounceWait(单位：ms)：'),
                    fac.AntdInputNumber(
                        id='input-debounce-wait-demo',
                        value=500,
                        min=0,
                        precision=0,
                    ),
                ],
                style={
                    'justify-content': 'space-between',
                    'width': '100%',
                },
            ),
            fac.AntdInput(
                id='input-debounce-demo',
                placeholder='请输入内容',
                maxLength=10,
            ),
            fac.AntdCard(
                [
                    html.Div(id='input-not-debounce-demo-output'),
                    html.Div(id='input-debounce-demo-output'),
                ],
                styles={
                    'header': {'display': 'none'},
                    'body': {'flexDirection': 'column'},
                },
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


# 通过AntdInputNumber回调设定input的debounceWait数值
@app.callback(
    Output('input-debounce-demo', 'debounceWait'),
    Input('input-debounce-wait-demo', 'value'),
)
def set_debounce_wait(value):
    return value


@app.callback(
    Output('input-not-debounce-demo-output', 'children'),
    Input('input-debounce-demo', 'value'),
)
def input_demo(value):
    return f'value: {value}'


@app.callback(
    Output('input-debounce-demo-output', 'children'),
    Input('input-debounce-demo', 'debounceValue'),
)
def input_debounce_demo(debounceValue):
    return f'debounceValue: {debounceValue}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('当前debounceWait(单位：ms)：'),
                fac.AntdInputNumber(
                    id='input-debounce-wait-demo',
                    value=500,
                    min=0,
                    precision=0,
                ),
            ],
            style={
                'justify-content': 'space-between',
                'width': '100%',
            },
        ),
        fac.AntdInput(
            id='input-debounce-demo',
            placeholder='请输入内容',
            maxLength=10,
        ),
        fac.AntdCard(
            [
                html.Div(id='input-not-debounce-demo-output'),
                html.Div(id='input-debounce-demo-output'),
            ],
            styles={
                'header': {'display': 'none'},
                'body': {'flexDirection': 'column'},
            },
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

# 通过AntdInputNumber回调设定input的debounceWait数值
@app.callback(
    Output('input-debounce-demo', 'debounceWait'),
    Input('input-debounce-wait-demo', 'value'),
)
def set_debounce_wait(value):
    return value


@app.callback(
    Output('input-not-debounce-demo-output', 'children'),
    Input('input-debounce-demo', 'value'),
)
def input_demo(value):
    return f'value: {value}'


@app.callback(
    Output('input-debounce-demo-output', 'children'),
    Input('input-debounce-demo', 'debounceValue'),
)
def input_debounce_demo(debounceValue):
    return f'debounceValue: {debounceValue}'
"""
    }
]

```

### `views/AntdInput/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(disabled=True),
            fac.AntdInput(disabled=True, mode='search'),
            fac.AntdInput(disabled=True, mode='text-area'),
            fac.AntdInput(disabled=True, mode='password'),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(disabled=True),
        fac.AntdInput(disabled=True, mode='search'),
        fac.AntdInput(disabled=True, mode='text-area'),
        fac.AntdInput(disabled=True, mode='password'),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/empty_as_none.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdText('emptyAsNone:'),
                    fac.AntdSwitch(
                        checked=True,
                        checkedChildren='True',
                        unCheckedChildren='False',
                        id='input-empty-as-none-demo-switch',
                    ),
                ]
            ),
            fac.AntdInput(
                placeholder='尝试输入后清空内容，观察回调输出',
                allowClear=True,
                emptyAsNone=True,
                id='input-empty-as-none-demo',
            ),
            fac.AntdCard(
                id='input-empty-as-none-demo-output',
                styles={'header': {'display': 'none'}},
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


# switch切换emptyAsNone状态
@app.callback(
    Output('input-empty-as-none-demo', 'emptyAsNone'),
    Input('input-empty-as-none-demo-switch', 'checked'),
)
def input_empty_as_none_demo_switch(checked):
    return checked


# 回调显示当前输入框内容
@app.callback(
    Output('input-empty-as-none-demo-output', 'children'),
    Input('input-empty-as-none-demo', 'value'),
)
def input_empty_as_none_demo_output(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('emptyAsNone:'),
                fac.AntdSwitch(
                    checked=True,
                    checkedChildren='True',
                    unCheckedChildren='False',
                    id='input-empty-as-none-demo-switch',
                ),
            ]
        ),
        fac.AntdInput(
            placeholder='尝试输入后清空内容，观察回调输出',
            allowClear=True,
            emptyAsNone=True,
            id='input-empty-as-none-demo',
        ),
        fac.AntdCard(
            id='input-empty-as-none-demo-output',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

# switch切换emptyAsNone状态
@app.callback(
    Output('input-empty-as-none-demo', 'emptyAsNone'),
    Input('input-empty-as-none-demo-switch', 'checked'),
)
def input_empty_as_none_demo_switch(checked):
    return checked


# 回调显示当前输入框内容
@app.callback(
    Output('input-empty-as-none-demo-output', 'children'),
    Input('input-empty-as-none-demo', 'value'),
)
def input_empty_as_none_demo_output(value):
    return f'value: {value}'
"""
    }
]

```

### `views/AntdInput/demos/focusing_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                id='input-focusing-demo',
                placeholder='尝试聚焦于此输入框',
            ),
            fac.AntdCard(
                id='input-focusing-demo-output',
                styles={'header': {'display': 'none'}},
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


@app.callback(
    Output('input-focusing-demo-output', 'children'),
    Input('input-focusing-demo', 'focusing'),
)
def input_focusing_dmeo(focusing):
    return f'focusing: {focusing}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            id='input-focusing-demo',
            placeholder='尝试聚焦于此输入框',
        ),
        fac.AntdCard(
            id='input-focusing-demo-output', 
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

@app.callback(
    Output('input-focusing-demo-output', 'children'),
    Input('input-focusing-demo', 'focusing'),
)
def input_focusing_dmeo(focusing):
    return f'focusing: {focusing}'
"""
    }
]

```

### `views/AntdInput/demos/max_length.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                mode=mode,
                maxLength=10,
                showCount=True if mode == 'text-area' else False,
                placeholder='请输入'
                if mode != 'text-area'
                else '请输入字符并注意下方计数',
                style={'width': 350},
            )
            for mode in [
                'default',
                'search',
                'password',
                'text-area',
            ]
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            mode=mode,
            maxLength=10,
            showCount=True if mode == 'text-area' else False,
            placeholder='请输入'
            if mode != 'text-area'
            else '请输入字符并注意下方计数',
            style={'width': 350},
        )
        for mode in [
            'default',
            'search',
            'password',
            'text-area',
        ]
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdInput/demos/md5_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app
from dash import html


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                id='input-md5-demo',
                placeholder='请输入密码',
                mode='password',
                passwordUseMd5=True,
                maxLength=10,
            ),
            fac.AntdCard(
                [
                    html.Div(id='input-not-md5-demo-output'),
                    html.Div(id='input-md5-demo-output'),
                ],
                styles={
                    'header': {'display': 'none'},
                    'body': {'flexDirection': 'column'},
                },
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


@app.callback(
    Output('input-not-md5-demo-output', 'children'),
    Input('input-md5-demo', 'value'),
)
def input_demo(value):
    return f'value: {value}'


@app.callback(
    Output('input-md5-demo-output', 'children'),
    Input('input-md5-demo', 'md5Value'),
)
def input_debounce_demo(md5Value):
    return f'md5Value: {md5Value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            id='input-md5-demo',
            placeholder='请输入密码',
            mode='password',
            passwordUseMd5=True,
            maxLength=10,
        ),
        fac.AntdCard(
            [
                html.Div(id='input-not-md5-demo-output'),
                html.Div(id='input-md5-demo-output'),
            ],
            styles={
                'header': {'display': 'none'},
                'body': {'flexDirection': 'column'},
            },
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

@app.callback(
    Output('input-not-md5-demo-output', 'children'),
    Input('input-md5-demo', 'value'),
)
def input_demo(value):
    return f'value: {value}'


@app.callback(
    Output('input-md5-demo-output', 'children'),
    Input('input-md5-demo', 'md5Value'),
)
def input_debounce_demo(md5Value):
    return f'md5Value: {md5Value}'
"""
    }
]

```

### `views/AntdInput/demos/n_click_search_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                id='input-search-demo',
                placeholder='按下搜索按钮',
                mode='search',
            ),
            fac.AntdCard(
                id='input-search-demo-output',
                styles={'header': {'display': 'none'}},
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


@app.callback(
    Output('input-search-demo-output', 'children'),
    Input('input-search-demo', 'nClicksSearch'),
)
def input_search_dmeo(nClicksSearch):
    return f'nClicksSearch: {nClicksSearch}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            id='input-search-demo',
            placeholder='按下搜索按钮',
            mode='search',
        ),
        fac.AntdCard(
            id='input-search-demo-output',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

@app.callback(
    Output('input-search-demo-output', 'children'),
    Input('input-search-demo', 'nClicksSearch'),
)
def input_search_dmeo(nClicksSearch):
    return f'nClicksSearch: {nClicksSearch}'
"""
    }
]

```

### `views/AntdInput/demos/n_submit_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('基本示例', innerTextOrientation='left'),
            fac.AntdInput(
                id='input-enter-demo',
                placeholder='聚焦于此后按下enter',
            ),
            fac.AntdCard(
                id='input-enter-demo-output',
                styles={'header': {'display': 'none'}},
            ),
            fac.AntdDivider('模拟登录示例', innerTextOrientation='left'),
            fac.AntdCard(
                fac.AntdSpace(
                    [
                        fac.AntdAlert(
                            message='聚焦于以下输入框后按下enter键，会得到和点击登录按钮相同的效果。',
                            type='info',
                            showIcon=True,
                            messageRenderMode='marquee',
                        ),
                        fac.AntdInput(
                            id='input-enter-demo-login',
                            placeholder='请输入用户名',
                            prefix=fac.AntdIcon(icon='antd-user'),
                        ),
                        fac.AntdInput(
                            id='input-enter-demo-password',
                            placeholder='请输入密码',
                            prefix=fac.AntdIcon(icon='antd-key'),
                            mode='password',
                        ),
                        fac.AntdCenter(
                            [
                                fac.AntdButton(
                                    '登录',
                                    type='primary',
                                    id='input-enter-demo-login-btn',
                                ),
                                fac.AntdButton(
                                    '取消',
                                    type='default',
                                    id='input-enter-demo-cancel-btn',
                                ),
                            ],
                            style={'gap': 10},
                        ),
                        fac.AntdText(
                            id='input-enter-demo-login-output',
                            style={'marginTop': 10},
                        ),
                    ],
                    direction='vertical',
                    style={'width': '100%'},
                ),
                styles={'header': {'display': 'none'}},
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


# 基本示例nSubmit回调函数
@app.callback(
    Output('input-enter-demo-output', 'children'),
    Input('input-enter-demo', 'nSubmit'),
)
def input_enter_dmeo(nSubmit):
    return f'nSubmit: {nSubmit}'


# 模拟登录示例nSubmit回调函数
@app.callback(
    Output('input-enter-demo-login-output', 'children'),
    [
        Input('input-enter-demo-login-btn', 'nClicks'),
        Input('input-enter-demo-login', 'nSubmit'),
        Input('input-enter-demo-password', 'nSubmit'),
    ],
    prevent_initial_call=True,
)
def input_enter_dmeo_login(nClicks1, nSubmit1, nSubmit2):
    if nClicks1 is None:
        nClicks1 = 0
    if nSubmit1 is None:
        nSubmit1 = 0
    if nSubmit2 is None:
        nSubmit2 = 0

    return f'登录次数：{nClicks1 + nSubmit1 + nSubmit2}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider('基本示例', innerTextOrientation='left'),
        fac.AntdInput(
            id='input-enter-demo',
            placeholder='聚焦于此后按下enter',
        ),
        fac.AntdCard(
            id='input-enter-demo-output',
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider('模拟登录示例', innerTextOrientation='left'),
        fac.AntdCard(
            fac.AntdSpace(
                [
                    fac.AntdAlert(
                        message='聚焦于以下输入框后按下enter键，会得到和点击登录按钮相同的效果。',
                        type='info',
                        showIcon=True,
                        messageRenderMode='marquee',
                    ),
                    fac.AntdInput(
                        id='input-enter-demo-login',
                        placeholder='请输入用户名',
                        prefix=fac.AntdIcon(icon='antd-user'),
                    ),
                    fac.AntdInput(
                        id='input-enter-demo-password',
                        placeholder='请输入密码',
                        prefix=fac.AntdIcon(icon='antd-key'),
                        mode='password',
                    ),
                    fac.AntdCenter(
                        [
                            fac.AntdButton(
                                '登录',
                                type='primary',
                                id='input-enter-demo-login-btn',
                            ),
                            fac.AntdButton(
                                '取消',
                                type='default',
                                id='input-enter-demo-cancel-btn',
                            ),
                        ],
                        style={'gap': 10},
                    ),
                    fac.AntdText(
                        id='input-enter-demo-login-output',
                        style={'marginTop': 10},
                    ),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 350},
)

...

# 基本示例nSubmit回调函数
@app.callback(
    Output('input-enter-demo-output', 'children'),
    Input('input-enter-demo', 'nSubmit'),
)
def input_enter_dmeo(nSubmit):
    return f'nSubmit: {nSubmit}'


# 模拟登录示例nSubmit回调函数
@app.callback(
    Output('input-enter-demo-login-output', 'children'),
    [
        Input('input-enter-demo-login-btn', 'nClicks'),
        Input('input-enter-demo-login', 'nSubmit'),
        Input('input-enter-demo-password', 'nSubmit'),
    ],
    prevent_initial_call=True,
)
def input_enter_dmeo_login(nClicks1, nSubmit1, nSubmit2):
    if nClicks1 is None:
        nClicks1 = 0
    if nSubmit1 is None:
        nSubmit1 = 0
    if nSubmit2 is None:
        nSubmit2 = 0

    return f'登录次数：{nClicks1+nSubmit1+nSubmit2}'
"""
    }
]

```

### `views/AntdInput/demos/prefix_and_suffix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                prefix=fac.AntdIcon(icon='antd-user'),
                placeholder='请输入用户名',
            ),
            fac.AntdInput(
                suffix=fac.AntdIcon(icon='antd-lock'),
                placeholder='请输入密码',
            ),
            fac.AntdInput(
                prefix=fac.AntdIcon(icon='antd-user'),
                mode='password',
                placeholder='请输入密码',
            ),
        ],
        direction='vertical',
        style={'width': 350},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            prefix=fac.AntdIcon(icon='antd-user'),
            placeholder='请输入用户名',
        ),
        fac.AntdInput(
            suffix=fac.AntdIcon(icon='antd-lock'),
            placeholder='请输入密码',
        ),
        fac.AntdInput(
            prefix=fac.AntdIcon(icon='antd-user'),
            mode='password',
            placeholder='请输入密码',
        ),
    ],
    direction='vertical',
    style={'width': 350},
)
"""
    }
]

```

### `views/AntdInput/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(value='This is a read-only input.', readOnly=True),
            fac.AntdInput(
                value='This is a read-only input.', readOnly=True, mode='search'
            ),
            fac.AntdInput(
                value='This is a read-only input.',
                readOnly=True,
                mode='text-area',
            ),
            fac.AntdInput(
                value='This is a read-only input.',
                readOnly=True,
                mode='password',
            ),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(value='This is a read-only input.', readOnly=True),
        fac.AntdInput(
            value='This is a read-only input.', readOnly=True, mode='search'
        ),
        fac.AntdInput(
            value='This is a read-only input.',
            readOnly=True,
            mode='text-area',
        ),
        fac.AntdInput(
            value='This is a read-only input.',
            readOnly=True,
            mode='password',
        ),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/show_count.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                mode='text-area',
                showCount=True,
                style={'width': 350},
            ),
            fac.AntdInput(
                mode='text-area',
                maxLength=10,
                showCount=True,
                placeholder='设置maxLength后，字符数将显示上限',
                style={'width': 350},
            ),
        ],
        direction='vertical',
        size='large',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            mode='text-area',
            showCount=True,
            style={'width': 350},
        ),
        fac.AntdInput(
            mode='text-area',
            maxLength=10,
            showCount=True,
            placeholder='设置maxLength后，字符数将显示上限',
            style={'width': 350},
        ),
    ],
    direction='vertical',
    size='large',
)
"""
    }
]

```

### `views/AntdInput/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(size='small', placeholder='size="small"'),
            fac.AntdInput(
                size='middle',
                placeholder='size="middle"（默认）',
            ),
            fac.AntdInput(size='large', placeholder='size="large"'),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(size='small', placeholder='size="small"'),
        fac.AntdInput(
            size='middle',
            placeholder='size="middle"（默认）',
        ),
        fac.AntdInput(size='large', placeholder='size="large"'),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('status="warning"', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    fac.AntdInput(
                        mode=mode,
                        prefix=fac.AntdIcon(icon='antd-home'),
                        addonBefore=fac.AntdIcon(icon='antd-user'),
                        status='warning',
                        style={'width': 350},
                    )
                    for mode in ['default', 'search', 'text-area', 'password']
                ],
                direction='vertical',
            ),
            fac.AntdDivider('status="error"', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    fac.AntdInput(
                        mode=mode,
                        suffix=fac.AntdIcon(icon='antd-home'),
                        addonAfter=fac.AntdIcon(icon='antd-user'),
                        status='error',
                        style={'width': 350},
                    )
                    for mode in ['default', 'search', 'text-area', 'password']
                ],
                direction='vertical',
            ),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider('status="warning"', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdInput(
                    mode=mode,
                    prefix=fac.AntdIcon(icon='antd-home'),
                    addonBefore=fac.AntdIcon(icon='antd-user'),
                    status='warning',
                    style={'width': 350},
                )
                for mode in ['default', 'search', 'text-area', 'password']
            ],
            direction='vertical',
        ),
        fac.AntdDivider('status="error"', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdInput(
                    mode=mode,
                    suffix=fac.AntdIcon(icon='antd-home'),
                    addonAfter=fac.AntdIcon(icon='antd-user'),
                    status='error',
                    style={'width': 350},
                )
                for mode in ['default', 'search', 'text-area', 'password']
            ],
            direction='vertical',
        ),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```

### `views/AntdInput/demos/variant.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdInput(
                variant='outlined', placeholder='variant="outlined"（默认）'
            ),
            fac.AntdInput(variant='filled', placeholder='variant="filled"'),
            fac.AntdInput(
                variant='borderless', placeholder='variant="borderless"'
            ),
            fac.AntdInput(
                variant='underlined', placeholder='variant="underlined"'
            ),
        ],
        direction='vertical',
        style={'width': '350px'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdInput(
            variant='outlined', placeholder='variant="outlined"（默认）'
        ),
        fac.AntdInput(variant='filled', placeholder='variant="filled"'),
        fac.AntdInput(
            variant='borderless', placeholder='variant="borderless"'
        ),
        fac.AntdInput(
            variant='underlined', placeholder='variant="underlined"'
        ),
    ],
    direction='vertical',
    style={'width': '350px'},
)
"""
    }
]

```
