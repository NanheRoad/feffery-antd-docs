# AntdSkeleton

## 简介源码：`views/AntdSkeleton/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '反馈'},
                {'title': '骨架屏'},
                {'title': 'AntdSkeleton 骨架屏'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSkeleton 骨架屏', level=2),
        fac.AntdParagraph('用于为正在加载中的内容添加骨架屏加载动画。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### active

- 说明：演示 active 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='skeleton-active-demo-trigger',
        style={'marginBottom': 10},
    ),
    fac.AntdSkeleton(
        fac.AntdParagraph(id='skeleton-active-demo-output'), active=True
    ),
]

...

@app.callback(
    Output('skeleton-active-demo-output', 'children'),
    Input('skeleton-active-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_active_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='skeleton-basic-demo-trigger',
        style={'marginBottom': 10},
    ),
    fac.AntdSkeleton(fac.AntdParagraph(id='skeleton-basic-demo-output')),
]

...

@app.callback(
    Output('skeleton-basic-demo-output', 'children'),
    Input('skeleton-basic-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_basic_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### custom_widgets

- 说明：演示 custom_widgets 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='skeleton-custom-demo-trigger',
        style={'marginBottom': 10},
    ),
    fac.AntdSkeleton(
        fac.AntdParagraph(id='skeleton-custom-demo-output'),
        active=True,
        avatar={'size': 'large', 'shape': 'square'},
        paragraph={'rows': 10, 'width': '20%'},
        title={'width': '4rem'},
    ),
]

...

@app.callback(
    Output('skeleton-custom-demo-output', 'children'),
    Input('skeleton-custom-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_custom_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### exclude_mode

- 说明：演示 exclude_mode 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdButton('按钮1', id='skeleton-exclude-demo-trigger1'),
            fac.AntdButton('按钮2', id='skeleton-exclude-demo-trigger2'),
        ],
        style={'width': '100%', 'marginBottom': 10},
    ),
    fac.AntdSkeleton(
        [
            fac.AntdParagraph(id='skeleton-exclude-demo-output1'),
            fac.AntdParagraph(id='skeleton-exclude-demo-output2'),
        ],
        active=True,
        listenPropsMode='exclude',
        excludeProps=['skeleton-exclude-demo-output1.children'],
    ),
]

...

@app.callback(
    Output('skeleton-exclude-demo-output1', 'children'),
    Input('skeleton-exclude-demo-trigger1', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_exclude_demo1(nClicks):
    time.sleep(1)

    return f'按钮1: {nClicks}'


@app.callback(
    Output('skeleton-exclude-demo-output2', 'children'),
    Input('skeleton-exclude-demo-trigger2', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_exclude_demo2(nClicks):
    time.sleep(1)

    return f'按钮2: {nClicks}'
```

### include_mode

- 说明：演示 include_mode 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdButton('按钮1', id='skeleton-include-demo-trigger1'),
            fac.AntdButton('按钮2', id='skeleton-include-demo-trigger2'),
        ],
        style={'width': '100%', 'marginBottom': 10},
    ),
    fac.AntdSkeleton(
        [
            fac.AntdParagraph(id='skeleton-include-demo-output1'),
            fac.AntdParagraph(id='skeleton-include-demo-output2'),
        ],
        active=True,
        listenPropsMode='include',
        includeProps=['skeleton-include-demo-output1.children'],
    ),
]

...

@app.callback(
    Output('skeleton-include-demo-output1', 'children'),
    Input('skeleton-include-demo-trigger1', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_include_demo1(nClicks):
    time.sleep(1)

    return f'按钮1: {nClicks}'


@app.callback(
    Output('skeleton-include-demo-output2', 'children'),
    Input('skeleton-include-demo-trigger2', 'nClicks'),
    prevent_initial_call=True,
)
def skeleton_include_demo2(nClicks):
    time.sleep(1)

    return f'按钮2: {nClicks}'
```
