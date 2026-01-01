# AntdRadioGroup

## 简介源码：`views/AntdRadioGroup/intro.py`
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
                {'title': 'AntdRadioGroup 单选框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRadioGroup 单选框', level=2),
        fac.AntdParagraph('用于供用户在一组选项中进行唯一项选择。'),
    ]

```

## 示例源码（demos）

### `views/AntdRadioGroup/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdRadioGroup(
            id='radio-group-demo',
            options=[{'label': f'选项{c}', 'value': c} for c in list('abcdef')],
            defaultValue='a',
        ),
        fac.AntdParagraph(id='radio-group-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('radio-group-demo-output', 'children'),
    Input('radio-group-demo', 'value'),
)
def radio_group_demo(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdRadioGroup(
    id='radio-group-demo',
    options=[
        {
            'label': f'选项{c}',
            'value': c
        }
        for c in list('abcdef')
    ],
    defaultValue='a'
),

fac.AntdParagraph(
    id='radio-group-demo-output'
)

...

@app.callback(
    Output('radio-group-demo-output', 'children'),
    Input('radio-group-demo', 'value')
)
def radio_group_demo(value):

    return f'value: {value}'
"""
    }
]

```

### `views/AntdRadioGroup/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdRadioGroup(
        options=[{'label': f'选项{c}', 'value': c} for c in list('abcdef')],
        defaultValue='a',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdRadioGroup(
    options=[
        {
            'label': f'选项{c}',
            'value': c
        }
        for c in list('abcdef')
    ],
    defaultValue='a'
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/block.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                block=True,
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
                block=True,
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
                buttonStyle='solid',
                block=True,
            ),
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
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            block=True,
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            block=True,
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            buttonStyle='solid',
            block=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/button_mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider(
                [fac.AntdText("'outline'", code=True), '风格'],
                innerTextOrientation='left',
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
            ),
            fac.AntdDivider(
                [fac.AntdText("'solid'", code=True), '风格'],
                innerTextOrientation='left',
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
                buttonStyle='solid',
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider(
            [fac.AntdText("'outline'", code=True), '风格'],
            innerTextOrientation='left',
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
        ),
        fac.AntdDivider(
            [fac.AntdText("'solid'", code=True), '风格'],
            innerTextOrientation='left',
        ),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            buttonStyle='solid',
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/component_label.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdRadioGroup(
        options=[
            {
                'label': fac.AntdText([fac.AntdIcon(icon=icon), f'选项{i}']),
                'value': f'选项{i}',
            }
            for i, icon in enumerate(
                ['antd-carry-out', 'antd-car', 'antd-bulb', 'antd-build']
            )
        ],
        defaultValue='选项1',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdRadioGroup(
    options=[
        {
            'label': fac.AntdText([fac.AntdIcon(icon=icon), f'选项{i}']),
            'value': f'选项{i}',
        }
        for i, icon in enumerate(
            ['antd-carry-out', 'antd-car', 'antd-bulb', 'antd-build']
        )
    ],
    defaultValue='选项1',
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/direction.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('水平排列', innerTextOrientation='left'),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
            ),
            fac.AntdDivider('竖直排列', innerTextOrientation='left'),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                direction='vertical',
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider('水平排列', innerTextOrientation='left'),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
        ),
        fac.AntdDivider('竖直排列', innerTextOrientation='left'),
        fac.AntdRadioGroup(
            options=[
                {'label': f'选项{c}', 'value': c} for c in list('abcdef')
            ],
            defaultValue='a',
            direction='vertical',
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/disabled_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                disabled=True,
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
                disabled=True,
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            disabled=True
        ),

        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            disabled=True
        )
    ],
    direction='vertical'
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/fast_options.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(options=list(range(10))),
            fac.AntdRadioGroup(options=[f'选项{i}' for i in range(10)]),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(options=list(range(10))),
        fac.AntdRadioGroup(options=[f'选项{i}' for i in range(10)]),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/read_only_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='c',
                readOnly=True,
            ),
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='c',
                optionType='button',
                readOnly=True,
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='c',
            readOnly=True
        ),

        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='c',
            optionType='button',
            readOnly=True
        )
    ],
    direction='vertical'
)
"""
    }
]

```

### `views/AntdRadioGroup/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                options=[
                    {'label': f'选项{c}', 'value': c} for c in list('abcdef')
                ],
                defaultValue='a',
                optionType='button',
                size=size,
            )
            for size in ['small', 'middle', 'large']
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            optionType='button',
            size=size
        )
        for size in [
            'small', 'middle', 'large'
        ]
    ],
    direction='vertical'
)
"""
    }
]

```
