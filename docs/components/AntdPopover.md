# AntdPopover

## 简介源码：`views/AntdPopover/intro.py`
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
                {'title': 'AntdPopover 气泡卡片'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdPopover 气泡卡片', level=2),
        fac.AntdParagraph('用于为指定元素添加额外说明信息。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdPopover(
    fac.AntdButton('锚点元素'), title='气泡卡片示例', content='内容示例'
)
```

### color

- 说明：演示 color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='popover-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdPopover(
            fac.AntdButton('锚点示例'),
            id='popover-color-demo',
            title='气泡卡片示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('popover-color-demo', 'color'),
        Output('popover-color-demo', 'content'),
    ],
    Input('popover-color-demo-input', 'color'),
)
def popover_color_demo(color):
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
        fac.AntdSwitch(id='popover-open-switch', checked=False),
        fac.AntdPopover(
            fac.AntdButton('锚点示例'),
            id='popover-open-demo',
            title='气泡卡片示例',
            content='内容示例',
        ),
    ]
)

...

@app.callback(
    Output('popover-open-demo', 'open'),
    Input('popover-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_popover_open(checked):
    return checked
```

### custom_style

- 说明：演示 custom_style 的用法。

#### 代码
```python
fac.AntdPopover(
    fac.AntdButton('锚点示例'),
    title='气泡卡片示例',
    content='内容示例' * 50,
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
fac.AntdPopover(
    fac.AntdButton('锚点元素'),
    title='气泡卡片示例',
    content='内容示例',
    arrow='hide',
)
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdPopover(
            fac.AntdButton(placement),
            title='气泡卡片示例',
            content=f'placement="{placement}"',
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
            'leftTop',
            'leftBottom',
            'rightTop',
            'rightBottom',
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
            fac.AntdPopover(
                fac.AntdButton(
                    '示例1',
                    type='primary'
                ),
                title='示例',
                content='示例内容'
            ),
            style={
                'position': 'absolute',
                'left': 15,
                'bottom': 15
            }
        ),
        html.Span(
            fac.AntdPopover(
                fac.AntdButton(
                    '示例2',
                    type='primary'
                ),
                title='示例',
                content='示例内容'
            ),
            style={
                'position': 'absolute',
                'right': 15,
                'top': 15
            }
        ),
        html.Span(
            fac.AntdPopover(
                fac.AntdButton(
                    '示例3',
                    type='primary'
                ),
                title='示例',
                content='示例内容'
            ),
            style={
                'position': 'absolute',
                'right': 15,
                'bottom': 15
            }
        )
    ],
    style={
        'position': 'relative',
        'height': 300,
        'background': '#dee2e6'
    }
)
```
