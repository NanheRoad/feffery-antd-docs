# AntdDrawer

## 简介源码：`views/AntdDrawer/intro.py`
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
                {'title': 'AntdDrawer 抽屉'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDrawer 抽屉', level=2),
        fac.AntdParagraph('从页面指定方位弹出可交互的额外容器。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '打开示例抽屉', id='drawer-basic-demo-open', type='primary'
    ),
    fac.AntdDrawer(
        '示例内容', title='基础抽屉示例', id='drawer-basic-demo'
    ),
]

...

@app.callback(
    Output('drawer-basic-demo', 'visible'),
    Input('drawer-basic-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_basic_demo(nCLicks):
    return True
```

### extra

- 说明：演示 extra 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '打开示例抽屉', id='drawer-extra-demo-open', type='primary'
    ),
    fac.AntdDrawer(
        '示例内容',
        id='drawer-extra-demo',
        title='抽屉示例',
        width='50vw',
        extra=fac.AntdSpace(
            [
                fac.AntdButton('操作1', type='primary'),
                fac.AntdButton('操作2', type='primary', danger=True),
            ],
            size='small',
        ),
    ),
]

...

@app.callback(
    Output('drawer-extra-demo', 'visible'),
    Input('drawer-extra-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_extra_demo(nClicks):
    return True
```

### footer

- 说明：演示 footer 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '打开示例抽屉', id='drawer-footer-demo-open', type='primary'
    ),
    fac.AntdDrawer(
        html.Div('示例内容', style={'height': 10000}),
        id='drawer-footer-demo',
        title='抽屉示例',
        footer=fac.AntdButton('页脚内容示例', type='primary'),
    ),
]

...

@app.callback(
    Output('drawer-footer-demo', 'visible'),
    Input('drawer-footer-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_footer_demo(nClicks):
    return True
```

### loading

- 说明：演示 loading 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '打开示例抽屉', id='drawer-loading-demo-open', type='primary'
    ),
    fac.AntdDrawer(
        '示例内容',
        title='加载状态示例',
        id='drawer-loading-demo',
        loading=True,
    ),
]

...

@app.callback(
    Output('drawer-loading-demo', 'visible'),
    Input('drawer-loading-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_loading_demo(nCLicks):
    return True
```

### local_container

- 说明：演示 local_container 的用法。

#### 代码
```python
html.Div(
    [
        fac.AntdButton(
            '打开示例抽屉', id='drawer-local-demo-open', type='primary'
        ),
        fac.AntdDrawer(
            '示例内容',
            id='drawer-local-demo',
            title='局部容器抽屉示例',
            containerId='drawer-local-container',
        ),
    ],
    id='drawer-local-container',
    style={
        'height': 400,
        'border': '1px solid #e9ecef',
        'position': 'relative',
        'padding': 25,
        'overflowX': 'hidden',
    },
)

...

@app.callback(
    Output('drawer-local-demo', 'visible'),
    Input('drawer-local-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_local_demo(nClicks):
    return True
```

### local_container_selector

- 说明：演示 local_container_selector 的用法。

#### 代码
```python
html.Div(
    [
        fac.AntdButton(
            '打开示例抽屉', id='drawer-free-local-demo-open', type='primary'
        ),
        fac.AntdDrawer(
            '示例内容',
            id='drawer-free-local-demo',
            title='局部容器抽屉示例',
            containerSelector="document.querySelector('.drawer-free-local-container')",
        ),
    ],
    className='drawer-free-local-container',
    style={
        'height': 400,
        'border': '1px solid #e9ecef',
        'position': 'relative',
        'padding': 25,
        'overflowX': 'hidden',
    },
)

...

@app.callback(
    Output('drawer-free-local-demo', 'visible'),
    Input('drawer-free-local-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def drawer_free_local_demo(nClicks):
    return True
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdRadioGroup(
                id='drawer-placement-demo-placement',
                options=[
                    {'label': placement, 'value': placement}
                    for placement in ['left', 'top', 'right', 'bottom']
                ],
                defaultValue='right',
            ),
            fac.AntdButton(
                '打开示例抽屉',
                id='drawer-placement-demo-open',
                type='primary',
            ),
        ],
        direction='vertical',
    ),
    fac.AntdDrawer('示例内容', id='drawer-placement-demo'),
]

...

@app.callback(
    [
        Output('drawer-placement-demo', 'title'),
        Output('drawer-placement-demo', 'placement'),
    ],
    Input('drawer-placement-demo-placement', 'value'),
)
def update_drawer_placement_and_title_dmeo(value):
    return [f'placement="{value}"', value]


@app.callback(
    Output('drawer-placement-demo', 'visible'),
    Input('drawer-placement-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def draw_placement_demo(nClicks):
    return True
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

- classNames (dict; optional):
    配置各子元素的css类名.

    `classNames` is a dict with keys:

    - header (string; optional):
        头部元素css类名.

    - body (string; optional):
        内容元素css类名.

    - footer (string; optional):
        底部元素css类名.

    - mask (string; optional):
        遮罩层元素css类名.

    - content (string; optional):
        抽屉容器元素css类名.

- styles (dict; optional):
    配置各子元素的css样式.

    `styles` is a dict with keys:

    - header (dict; optional):
        头部元素css样式.

    - body (dict; optional):
        内容元素css样式.

    - footer (dict; optional):
        底部元素css样式.

    - mask (dict; optional):
        遮罩层元素css样式.

    - content (dict; optional):
        抽屉容器元素css样式.

- rootStyle (dict; optional):
    抽屉根节点css样式（包含遮罩层），特殊的，当设置了`containerId`或`containerSelector`时，该参数会自动设置`position`为`absolute`.

- visible (boolean; default False):
    监听或设置抽屉是否可见  默认值：`False`.

- title (a list of or a singular dash component, string or number; optional):
    组件型，抽屉标题内容.

- placement (a value equal to: 'left', 'right', 'top', 'bottom'; default 'right'):
    抽屉弹出位置，可选项有`'left'`、`'right'`、`'top'`、`'bottom'`  默认值：`'right'`.

- closable (boolean; default True):
    是否显示关闭按钮  默认值：`True`.

- forceRender (boolean; default False):
    是否对抽屉内的子元素进行预渲染  默认值：`False`.

- destroyOnClose (boolean; default False):
    是否在关闭时销毁抽屉内的子元素  默认值：`False`.

- width (number | string; default 256):
    抽屉像素宽度，`placement`为`'left'`、`'right'`时有效  默认值：`256`.

- height (number | string; default 256):
    抽屉像素高度，`placement`为`'top'`、`'bottom'`时有效  默认值：`256`.

- mask (boolean; default True):
    是否显示遮罩层  默认值：`True`.

- maskClosable (boolean; default True):
    是否允许点击遮罩区域关闭抽屉  默认值：`True`.

- zIndex (number; default 1000):
    抽屉整体`z-index`  默认值：`1000`.

- loading (boolean; default False):
    是否渲染为加载中状态  默认值：`False`.

- extra (a list of or a singular dash component, string or number; optional):
    组件型，额外操作区元素.

- footer (a list of or a singular dash component, string or number; optional):
    组件型，底部元素.

- containerId (string; optional):
    用于设置`position`为`relative`的局部容器id.

- containerSelector (string; optional):
    当目标容器定位较为复杂时，可传入获取元素对应的js代码字符串，优先级低于`containerId`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
