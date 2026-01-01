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

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
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
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
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
```

### block

- 说明：演示 block 的用法。

#### 代码
```python
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
```

### button_mode

- 说明：演示 button_mode 的用法。

#### 代码
```python
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
```

### component_label

- 说明：演示 component_label 的用法。

#### 代码
```python
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
```

### direction

- 说明：演示 direction 的用法。

#### 代码
```python
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
```

### disabled_status

- 说明：演示 disabled_status 的用法。

#### 代码
```python
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
```

### fast_options

- 说明：演示 fast_options 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(options=list(range(10))),
        fac.AntdRadioGroup(options=[f'选项{i}' for i in range(10)]),
    ],
    direction='vertical',
)
```

### read_only_status

- 说明：演示 read_only_status 的用法。

#### 代码
```python
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
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
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
```
