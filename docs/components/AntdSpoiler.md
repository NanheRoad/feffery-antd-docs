# AntdSpoiler

## 简介源码：`views/AntdSpoiler/intro.py`
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
                {'title': 'AntdSpoiler 展开收起'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSpoiler 展开收起', level=2),
        fac.AntdParagraph('用于实现对指定内容的展开收起效果。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100), maxHeight=70
)
```

### label_position

- 说明：演示 label_position 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdSegmented(
            id='spolier-label-position-options',
            options=[
                {'label': 'left', 'value': 'left'},
                {'label': 'right', 'value': 'right'},
            ],
            defaultValue='left',
        ),
        fac.AntdSpoiler(
            fac.AntdParagraph('内容示例' * 100),
            id='spolier-label-position-demo',
            maxHeight=70,
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)

...

@app.callback(
    Output('spolier-label-position-demo', 'labelPosition'),
    Input('spolier-label-position-options', 'value'),
)
def update_spoiler_label_position(value):
    return value
```

### transition_duration

- 说明：演示 transition_duration 的用法。

#### 代码
```python
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100),
    maxHeight=70,
    transitionDuration=0.5,
)
```
