# AntdRate

## 简介源码：`views/AntdRate/intro.py`
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
                {'title': 'AntdRate 评分'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRate 评分', level=2),
        fac.AntdParagraph('用于为用户提供美观的星级打分功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdRate(
    id='rate-demo',
    count=10,
    allowHalf=True,
    defaultValue=1
),

fac.AntdParagraph(
    id='rate-demo-output'
)

...

@app.callback(
    Output('rate-demo-output', 'children'),
    Input('rate-demo', 'value')
)
def rate_demo(value):

    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdRate(), fac.AntdRate(count=10, defaultValue=5)],
    direction='vertical',
)
```

### clear

- 说明：演示 clear 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=True, defaultValue=3),
                fac.AntdText('allowClear：True'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=False, defaultValue=3),
                fac.AntdText('allowClear：False'),
            ]
        ),
    ],
    direction='vertical',
)
```

### half_star

- 说明：演示 half_star 的用法。

#### 代码
```python
fac.AntdRate(allowHalf=True, defaultValue=3.5)
```

### read_only_status

- 说明：演示 read_only_status 的用法。

#### 代码
```python
fac.AntdRate(
    count=10, defaultValue=7.5, allowHalf=True, disabled=True
)
```

### star_tooltips

- 说明：演示 star_tooltips 的用法。

#### 代码
```python
fac.AntdRate(
    count=10, tooltips=[f'等级{i + 1}' for i in range(10)]
)
```
