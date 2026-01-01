# AntdSegmented

## 简介源码：`views/AntdSegmented/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdSegmented 分段控制器'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSegmented 分段控制器', level=2),
        fac.AntdParagraph('用于展示多个选项并允许用户选择其中单个选项。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='segmented-demo',
            options=[
                {'label': i, 'value': i}
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            defaultValue='Daily',
        ),
        fac.AntdText(id='segmented-demo-output'),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('segmented-demo-output', 'children'),
    Input('segmented-demo', 'value'),
)
def segmented_demo(value):
    return f'value: {value}
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
)
```

### block

- 说明：演示 block 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=[
        {'label': f'{i}', 'value': i}
        for i in [123, 456, 'longtext-longtext-longtext-longtext']
    ],
    defaultValue=123,
    block=True,
)
```

### custom_render

- 说明：演示 custom_render 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='image',
                                src='https://api.dicebear.com/7.x/miniavs/svg?seed=8',
                            ),
                            html.Div('User 1'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user1',
                },
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='text',
                                text='K',
                                style={
                                    'backgroundColor': '#f56a00',
                                },
                            ),
                            html.Div('User 2'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user2',
                },
                {
                    'label': html.Div(
                        [
                            fac.AntdAvatar(
                                mode='icon',
                                icon='antd-user',
                                style={
                                    'backgroundColor': '#87d068',
                                },
                            ),
                            html.Div('User 3'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'user3',
                },
            ]
        ),
        fac.AntdSegmented(
            options=[
                {
                    'label': html.Div(
                        [
                            html.Div('Spring'),
                            html.Div('Jan-Mar'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'spring',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Summer'),
                            html.Div('Apr-Jun'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'summer',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Autumn'),
                            html.Div('Jul-Sept'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'autumn',
                },
                {
                    'label': html.Div(
                        [
                            html.Div('Winter'),
                            html.Div('Oct-Dec'),
                        ],
                        style={'padding': 4},
                    ),
                    'value': 'winter',
                },
            ]
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {'label': i, 'value': i}
                for i in ['Map', 'Transit', 'Satellite']
            ],
            defaultValue='Map',
            disabled=True,
        ),
        fac.AntdSegmented(
            options=[
                {
                    'label': i,
                    'value': i,
                    'disabled': True
                    if i in ['Weekly', 'Quarterly']
                    else False,
                }
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            defaultValue='Daily',
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
```

### icon

- 说明：演示 icon 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=[
        {'label': f'选项{i}', 'value': i, 'icon': icon}
        for i, icon in enumerate(
            [
                'antd-carry-out',
                'antd-branches',
                'antd-team',
                'antd-send',
                'antd-setting',
            ]
        )
    ],
    defaultValue=0,
)
```

### only_icon

- 说明：演示 only_icon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSegmented(
            options=[
                {'value': i, 'icon': icon}
                for i, icon in enumerate(
                    [
                        'antd-carry-out',
                        'antd-branches',
                        'antd-team',
                        'antd-send',
                        'antd-setting',
                    ]
                )
            ],
            defaultValue=0,
        ),
        fac.AntdSegmented(
            options=[
                {'value': i, 'icon': icon}
                for i, icon in enumerate(
                    [
                        'antd-carry-out',
                        'antd-branches',
                        'antd-team',
                        'antd-send',
                        'antd-setting',
                    ]
                )
            ],
            defaultValue=0,
            vertical=True,
        ),
    ],
    direction='vertical',
)
```

### quickly_set_options

- 说明：演示 quickly_set_options 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly'],
    defaultValue='Daily',
)
```

### shape

- 说明：演示 shape 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
    shape='round',
)
```

### size

- 说明：演示 size 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdSegmented(
            options=[
                {'label': i, 'value': i}
                for i in [
                    'Daily',
                    'Weekly',
                    'Monthly',
                    'Quarterly',
                    'Yearly',
                ]
            ],
            size=size,
            defaultValue='Daily',
        )
        for size in ['small', 'middle', 'large']
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)
```

### vertical

- 说明：演示 vertical 的用法。

#### 代码
```python
fac.AntdSegmented(
    options=[
        {'label': i, 'value': i}
        for i in ['Daily', 'Weekly', 'Monthly', 'Quarterly', 'Yearly']
    ],
    defaultValue='Daily',
    vertical=True,
)
```
