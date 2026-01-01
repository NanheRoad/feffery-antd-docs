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

## 示例源码（demos）

### `views/AntdSegmentedColoring/demos/auxiliary_button.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdSegmentedColoring(
            id='segmented-coloring-demo2',
            size='small',
            min=-10,
            max=10,
            breakpoints=[0, 1, 2, 3, 4, 5],
            colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        ),
        fac.AntdParagraph(
            [
                fac.AntdText('breakpoints: ', strong=True),
                fac.AntdText(id='segmented-coloring-demo2-output'),
            ]
        ),
    ]

    return demo_contents


@app.callback(
    Output('segmented-coloring-demo2-output', 'children'),
    Input('segmented-coloring-demo2', 'breakpoints'),
)
def segmented_coloring_demo2_callback(breakpoints):
    return str(breakpoints)


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmentedColoring(
        min=-10,
        max=10,
        breakpoints=[0, 1, 2, 3, 4, 5],
        colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmentedColoring(
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
)
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/border.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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
                bordered=False,
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
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/color_block_click_event.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/color_block_position.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/disabled_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmentedColoring(
        size='small',
        min=-10,
        max=10,
        breakpoints=[0, 1, 2, 3, 4, 5],
        colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        disabled=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmentedColoring(
    size='small',
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    disabled=True,
)
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/read_only_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSegmentedColoring(
        size='small',
        min=-10,
        max=10,
        breakpoints=[0, 1, 2, 3, 4, 5],
        colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
        readOnly=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSegmentedColoring(
    size='small',
    min=-10,
    max=10,
    breakpoints=[0, 1, 2, 3, 4, 5],
    colors=['#deecf9', '#71afe5', '#2b88d8', '#0078d4', '#106ebe'],
    readOnly=True,
)
"""
    }
]

```

### `views/AntdSegmentedColoring/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```
