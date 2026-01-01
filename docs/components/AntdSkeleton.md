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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- loading (boolean; default False):
    是否处于加载中状态.

- active (boolean; default False):
    是否显示动画  默认值：`False`.

- delay (number; default 0):
    加载动画渲染延时，单位：毫秒  默认值：`0`.

- avatar (dict; default False):
    配置头像占位图相关参数，设置为`False`时不显示  默认值：`True`.

    `avatar` is a boolean | dict with keys:

    - active (boolean; optional):
        头像占位图是否显示动画  默认值：`False`.

    - shape (a value equal to: 'circle', 'square'; optional):
        头像占位图形状，可选项有`'circle'`、`'square'`.

    - size (number | a value equal to: 'large', 'small', 'default'; optional):
        头像占位图尺寸，传入数值型表示像素尺寸，也可传入预设的尺寸规格，可选项有`'large'`、`'small'`、`'default'`
        默认值：`'default'`.

- paragraph (dict; default True):
    配置段落占位图相关参数，设置为`False`时不显示  默认值：`True`.

    `paragraph` is a boolean | dict with keys:

    - rows (number; optional):
        段落占位图行数.

    - width (number | string | list of number | strings; optional):
        段落占位图宽度，当传入*int*或*string*型时，用于设置段落占位图最后一行的宽度，当传入*list*型时，用于逐行设置宽度.

- title (dict; default True):
    是否显示标题占位图  默认值：`True`.

    `title` is a boolean | dict with keys:

    - width (number | string; optional):
        标题占位图宽度.

- round (boolean; default False):
    段落、标题占位图是否渲染圆角  默认值：`False`.

- debug (boolean; default False):
    是否开启debug模式，开启后，每次动画加载都会在开发者工具的控制台打印相关`prop`信息  默认值：`False`.

- listenPropsMode (a value equal to: 'default', 'exclude', 'include'; default 'default'):
    监听模式，可选项有`'default'`、`'exclude'`、`'include'`  默认值：`'default'`.

- excludeProps (list of strings; optional):
    `listenPropsMode='exclude'`时，设置需要排除监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- includeProps (list of strings; optional):
    `listenPropsMode='include'`时，设置需要包含监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- manual (boolean; default False):
    是否开启手动控制模式，开启后是否处于加载状态将由`loading`参数控制，与内部元素参与的回调状态无关  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
