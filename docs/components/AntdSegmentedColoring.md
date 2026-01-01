# AntdSegmentedColoring

## 简介源码：`views/AntdSegmentedColoring/intro.py`
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
                {'title': 'AntdSegmentedColoring 分段着色'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSegmentedColoring 分段着色', level=2),
        fac.AntdParagraph(
            '用于配合数据可视化进行分段着色控制，或作为静态的图例进行展示。'
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### auxiliary_button

- 说明：演示 auxiliary_button 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            fac.AntdText('controls=True', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
        fac.AntdDivider(
            fac.AntdText('controls=False', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
            controls=False,
        ),
    ],
    direction='vertical',
)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSegmentedColoring(
    id='segmented-coloring-demo2',
    size='small',
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=["#deecf9", "#71afe5",
            "#2b88d8", "#0078d4",
            "#106ebe"]
),

fac.AntdParagraph(
    [
        fac.AntdText('breakpoints: ', strong=True),
        fac.AntdText(
            id='segmented-coloring-demo2-output'
        )
    ]
)

...

@app.callback(
    Output('segmented-coloring-demo2-output', 'children'),
    Input('segmented-coloring-demo2', 'breakpoints')
)
def segmented_coloring_demo2_callback(breakpoints):
    return str(breakpoints)
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSegmentedColoring(
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
)
```

### border

- 说明：演示 border 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            fac.AntdText('bordered=True', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
        fac.AntdDivider(
            fac.AntdText('bordered=False', code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
            bordered=False
        ),
    ],
    direction='vertical',
)
```

### color_block_click_event

- 说明：演示 color_block_click_event 的用法。

#### 代码
```python
[
    fac.AntdSegmentedColoring(
        id='segmented-coloring-color-block-click-event-demo',
        size='small',
        min=-10,
        max=10,
        breakpoints=[0, 1, 2, 3, 4, 5],
        colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    ),
    html.Pre(id='segmented-coloring-color-block-click-event-demo-output'),
]

...

@app.callback(
    Output(
        'segmented-coloring-color-block-click-event-demo-output', 'children'
    ),
    Input(
        'segmented-coloring-color-block-click-event-demo',
        'colorBlockClickEvent',
    ),
    prevent_initial_call=True,
)
def show_color_block_click_event(colorBlockClickEvent):
    return json.dumps(colorBlockClickEvent, indent=4, ensure_ascii=False)
```

### color_block_position

- 说明：演示 color_block_position 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            fac.AntdText("colorBlockPosition='left'", code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
            colorBlockPosition='left',
        ),
        fac.AntdDivider(
            fac.AntdText("colorBlockPosition='right'", code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
            colorBlockPosition='right',
        ),
    ],
    direction='vertical',
)
```

### disabled_status

- 说明：演示 disabled_status 的用法。

#### 代码
```python
fac.AntdSegmentedColoring(
    size='small',
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    disabled=True,
)
```

### read_only_status

- 说明：演示 read_only_status 的用法。

#### 代码
```python
fac.AntdSegmentedColoring(
    size='small',
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    readOnly=True,
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            fac.AntdText("size='small", code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
        fac.AntdDivider(
            fac.AntdText("size='middle", code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
        fac.AntdDivider(
            fac.AntdText("size='large", code=True),
            innerTextOrientation='left',
        ),
        fac.AntdSegmentedColoring(
            size='large',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
    ],
    direction='vertical',
)
```
