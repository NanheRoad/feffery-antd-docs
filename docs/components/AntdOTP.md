# AntdOTP

## 简介源码：`views/AntdOTP/intro.py`
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
                {'title': 'AntdOTP 一次性密码框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdOTP 一次性密码框', level=2),
        fac.AntdParagraph('用于提供验证码等一次性固定位数密码输入功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdOTP(id='otp-demo'),
        fac.AntdText(id='otp-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('otp-demo-output', 'children'),
    Input('otp-demo', 'value'),
    prevent_initial_call=True,
)
def show_otp_value(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdOTP()
```

### custom_display_character

- 说明：演示 custom_display_character 的用法。

#### 代码
```python
fac.AntdOTP(mask='🔒')
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdOTP(disabled=True)
```

### length

- 说明：演示 length 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdOTP(length=i) for i in range(3, 10)], direction='vertical'
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('size="small"', innerTextOrientation='left'),
        fac.AntdOTP(size='small'),
        fac.AntdDivider(
            'size="middle"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(),
        fac.AntdDivider('size="large"', innerTextOrientation='left'),
        fac.AntdOTP(size='large'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdOTP(status=status) for status in ['warning', 'error']],
    direction='vertical',
)
```

### variant

- 说明：演示 variant 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            'variant="outlined"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='outlined'),
        fac.AntdDivider(
            'variant="borderless"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='borderless'),
        fac.AntdDivider('variant="filled"', innerTextOrientation='left'),
        fac.AntdOTP(variant='filled'),
        fac.AntdDivider(
            'variant="underlined"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='underlined'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
