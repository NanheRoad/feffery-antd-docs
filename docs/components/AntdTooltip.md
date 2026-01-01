# AntdTooltip

## 简介源码：`views/AntdTooltip/intro.py`
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
                {'title': 'AntdTooltip 信息提示'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTooltip 信息提示', level=2),
        fac.AntdParagraph('用于为指定元素添加额外信息提示。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例'
)
```

### color

- 说明：演示 color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='tooltip-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-color-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('tooltip-color-demo', 'color'),
        Output('tooltip-color-demo', 'title'),
    ],
    Input('tooltip-color-demo-input', 'color'),
)
def tooltip_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]
```

### control_open

- 说明：演示 control_open 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSwitch(id='tooltip-open-switch', checked=False),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-open-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    Output('tooltip-open-demo', 'open'),
    Input('tooltip-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_tooltip_open(checked):
    return checked
```

### custom_style

- 说明：演示 custom_style 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点示例'),
    title='内容示例' * 50,
    styles={
        'root': {'width': 250},
        'body': {'maxHeight': 150, 'overflowY': 'auto'},
    },
)
```

### hide_arrow

- 说明：演示 hide_arrow 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例', arrow='hide'
)
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTooltip(
            fac.AntdButton(placement),
            title='信息提示示例',
            placement=placement,
        )
        for placement in [
            'top',
            'left',
            'right',
            'bottom',
            'topLeft',
            'topRight',
            'bottomLeft',
            'bottomRight',
        ]
    ],
    wrap=True,
)
```

### question_with_absolute_position

- 说明：演示 question_with_absolute_position 的用法。

#### 代码
```python
html.Div(
    [
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例1', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'left': 15, 'bottom': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例2', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'top': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例3', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'bottom': 15},
        ),
    ],
    style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
)
```
