# AntdInputNumber

## 简介源码：`views/AntdInputNumber/intro.py`
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
                {'title': 'AntdInputNumber 数值输入框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdInputNumber 数值输入框', level=2),
        fac.AntdParagraph('专门提供数值输入功能的输入框。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### addon

- 说明：演示 addon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            addonBefore='前缀元素',
            addonAfter='后缀元素',
            style={'width': 300},
        ),
        fac.AntdInputNumber(
            addonBefore=fac.AntdSelect(
                defaultValue='a',
                options=[
                    {'label': option, 'value': option}
                    for option in ['a', 'b']
                ],
                allowClear=False,
            ),
            addonAfter=fac.AntdSelect(
                defaultValue='m',
                options=[
                    {'label': option, 'value': option}
                    for option in ['mm', 'cm', 'dm', 'm']
                ],
                allowClear=False,
            ),
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(id='input-number-demo', style={'width': 200}),
        fac.AntdText(id='input-number-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('input-number-demo-output', 'children'),
    Input('input-number-demo', 'value'),
    prevent_initial_call=True,
)
def show_input_number_value(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdInputNumber(
    placeholder='请输入数值', style={'width': 100}
)
```

### debounce_callbacks

- 说明：演示 debounce_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            id='input-number-debounce-demo',
            debounceWait=500,
            style={'width': 200},
        ),
        fac.AntdText(id='input-number-debounce-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('input-number-debounce-demo-output', 'children'),
    Input('input-number-debounce-demo', 'debounceValue'),
    prevent_initial_call=True,
)
def show_input_number_debounce_value(debounceValue):
    return f'debounceValue: {debounceValue}'
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdInputNumber(disabled=True, style={'width': 100})
```

### limit_min_max

- 说明：演示 limit_min_max 的用法。

#### 代码
```python
fac.AntdInputNumber(
    min=0,
    max=100,
    placeholder='请尝试输入0~100以外的数值查看效果',
    style={'width': 275},
)
```

### precision

- 说明：演示 precision 的用法。

#### 代码
```python
fac.AntdInputNumber(
    precision=5, placeholder='precision=5', style={'width': 150}
)
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdInputNumber(
    prefix=fac.AntdIcon(icon='antd-control'), style={'width': 200}
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdInputNumber(
    value=3.1415, readOnly=True, style={'width': 100}
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            placeholder=f'size="{size}"', size=size, style={'width': 150}
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdInputNumber(status=status) for status in ['warning', 'error']],
    direction='vertical',
)
```

### step

- 说明：演示 step 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            step=0.1, defaultValue=0, placeholder='step=0.1'
        ),
        fac.AntdInputNumber(
            step=0.001, defaultValue=0, placeholder='step=0.001'
        ),
    ],
    direction='vertical',
)
```

### string_mode

- 说明：演示 string_mode 的用法。

#### 代码
```python
fac.AntdInputNumber(
    stringMode=True,
    defaultValue='0.1312312314124123124124123123123312312321312312312312',
    style={'width': '100%'},
)
```

### suffix

- 说明：演示 suffix 的用法。

#### 代码
```python
fac.AntdInputNumber(
    suffix=fac.AntdIcon(icon='antd-account-book'), style={'width': 200}
)
```

### variant

- 说明：演示 variant 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInputNumber(
            variant=variant,
            placeholder=f'variant="{variant}"',
            style={'width': 200},
        )
        for variant in ['outlined', 'borderless', 'filled', 'underlined']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
