# AntdPopupCard

## 简介源码：`views/AntdPopupCard/intro.py`
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
                {'title': 'AntdPopupCard 弹出式卡片'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdPopupCard 弹出式卡片', level=2),
        fac.AntdParagraph('用于以弹出式卡片的形式展现内容。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton('点击触发', id='popup-card-basic-demo-trigger'),
    fac.AntdPopupCard(
        fac.AntdParagraph('内容示例' * 20),
        id='popup-card-basic-demo',
        title='弹出式卡片示例',
        visible=False,
    ),
]

...

@app.callback(
    Output('popup-card-basic-demo', 'visible'),
    Input('popup-card-basic-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_basic_demo(nClicks):
    return True
```

### close_icon_type

- 说明：演示 close_icon_type 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdSelect(
                id='popup-card-close-icon-type-demo-select',
                defaultValue='default',
                allowClear=False,
                options=[
                    {'label': closeIconType, 'value': closeIconType}
                    for closeIconType in ['default', 'outlined', 'two-tone']
                ],
                style={'width': 200},
            ),
            fac.AntdButton(
                '点击触发', id='popup-card-close-icon-type-demo-trigger'
            ),
        ]
    ),
    fac.AntdPopupCard(
        fac.AntdParagraph('内容示例' * 20),
        id='popup-card-close-icon-type-demo',
        title='弹出式卡片示例',
        visible=False,
    ),
]

...

@app.callback(
    Output('popup-card-close-icon-type-demo', 'closeIconType'),
    Input('popup-card-close-icon-type-demo-select', 'value'),
)
def popup_card_close_icon_type_demo(value):
    return value


@app.callback(
    Output('popup-card-close-icon-type-demo', 'visible'),
    Input('popup-card-close-icon-type-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_close_icon_type_demo_visible(nClicks):
    return True
```

### draggable

- 说明：演示 draggable 的用法。

#### 代码
```python
[
    fac.AntdButton('点击触发', id='popup-card-draggable-demo-trigger'),
    fac.AntdPopupCard(
        fac.AntdParagraph('内容示例' * 20),
        id='popup-card-draggable-demo',
        title='弹出式卡片示例',
        visible=False,
        draggable=True,
    ),
]

...

@app.callback(
    Output('popup-card-draggable-demo', 'visible'),
    Input('popup-card-draggable-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_draggable_demo(nClicks):
    return True
```

### set_default_position

- 说明：演示 set_default_position 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '点击触发', id='popup-card-custom-position-demo-trigger'
    ),
    fac.AntdPopupCard(
        fac.AntdParagraph('内容示例' * 20),
        id='popup-card-custom-position-demo',
        title='弹出式卡片示例',
        visible=False,
        style={
            'bottom': 25,
            'left': 25,
            'position': 'fixed',
            'top': 'auto',  # 用于覆盖默认的top: 100px设定
        },
    ),
]

...

@app.callback(
    Output('popup-card-custom-position-demo', 'visible'),
    Input('popup-card-custom-position-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_custom_position_demo(nClicks):
    return True
```

### transition_type

- 说明：演示 transition_type 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdSelect(
                id='popup-card-transition-type-demo-select',
                defaultValue='fade',
                allowClear=False,
                options=[
                    {'label': transitionType, 'value': transitionType}
                    for transitionType in [
                        'none',
                        'fade',
                        'zoom',
                        'zoom-big',
                        'zoom-big-fast',
                        'slide-up',
                        'slide-down',
                        'slide-left',
                        'slide-right',
                        'move-up',
                        'move-down',
                        'move-left',
                        'move-right',
                    ]
                ],
                style={'width': 200},
            ),
            fac.AntdButton(
                '点击触发', id='popup-card-transition-type-demo-trigger'
            ),
        ]
    ),
    fac.AntdPopupCard(
        fac.AntdParagraph('内容示例' * 20),
        id='popup-card-transition-type-demo',
        title='弹出式卡片示例',
        visible=False,
    ),
]

...

@app.callback(
    Output('popup-card-transition-type-demo', 'transitionType'),
    Input('popup-card-transition-type-demo-select', 'value'),
)
def popup_card_transition_type_demo(value):
    return value


@app.callback(
    Output('popup-card-transition-type-demo', 'visible'),
    Input('popup-card-transition-type-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_transition_type_demo_visible(nClicks):
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

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - mask (dict; optional):
        遮罩层元素css样式.

    - content (dict; optional):
        容器元素css样式.

    - wrapper (dict; optional):
        包裹层元素css样式.

    - header (dict; optional):
        头部元素css样式.

    - body (dict; optional):
        内容元素css样式.

    - footer (dict; optional):
        底部元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - mask (string; optional):
        遮罩层元素css类名.

    - content (string; optional):
        容器元素css类名.

    - wrapper (string; optional):
        包裹层元素css类名.

    - header (string; optional):
        头部元素css类名.

    - body (string; optional):
        内容元素css类名.

    - footer (string; optional):
        底部元素css类名.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- visible (boolean; default True):
    设置或监听当前弹出式卡片是否显示  默认值：`True`.

- width (number | string; optional):
    弹出式卡片像素宽度.

- transitionType (a value equal to: 'none', 'fade', 'zoom', 'zoom-big', 'zoom-big-fast', 'slide-up', 'slide-down', 'slide-left', 'slide-right', 'move-up', 'move-down', 'move-left', 'move-right'; default 'fade'):
    卡片显隐动画类型，可选项有`'none'`、`'fade'`、`'zoom'`、`'zoom-big'`、`'zoom-big-fast'`、`'slide-up'`、`'slide-down'`、`'slide-left'`、`'slide-right'`、`'move-up'`、`'move-down'`、`'move-left'`、`'move-right'`
    默认值：`'zoom'`.

- forceRender (boolean; default False):
    是否在初始化卡片未显示时，强制渲染卡片内部元素  默认值：`False`.

- destroyOnClose (boolean; default True):
    是否在卡片关闭后自动销毁内部元素  默认值：`True`.

- closable (boolean; default True):
    是否显示右上角的关闭按钮  默认值：`True`.

- closeIconType (a value equal to: 'default', 'outlined', 'two-tone'; default 'default'):
    关闭按钮类型，可选项有`'default'`、`'outlined'`、`'two-tone'`  默认值：`'default'`.

- draggable (boolean; default False):
    是否可拖拽  默认值：`False`.

- dragClassName (string | dict; optional):
    顶部可拖拽区域css类名.

- zIndex (number; default 1000):
    弹出式卡片z-index  默认值：`1000`.

- loading (boolean; default False):
    是否整体渲染为加载中状态  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
