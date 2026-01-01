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

## 示例源码（demos）

### `views/AntdPopupCard/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdButton('点击触发', id='popup-card-basic-demo-trigger'),
        fac.AntdPopupCard(
            fac.AntdParagraph('内容示例' * 20),
            id='popup-card-basic-demo',
            title='弹出式卡片示例',
            visible=False,
        ),
    ]

    return demo_contents


@app.callback(
    Output('popup-card-basic-demo', 'visible'),
    Input('popup-card-basic-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_basic_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdPopupCard/demos/close_icon_type.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdPopupCard/demos/draggable.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdButton('点击触发', id='popup-card-draggable-demo-trigger'),
        fac.AntdPopupCard(
            fac.AntdParagraph('内容示例' * 20),
            id='popup-card-draggable-demo',
            title='弹出式卡片示例',
            visible=False,
            draggable=True,
        ),
    ]

    return demo_contents


@app.callback(
    Output('popup-card-draggable-demo', 'visible'),
    Input('popup-card-draggable-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_draggable_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdPopupCard/demos/set_default_position.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('popup-card-custom-position-demo', 'visible'),
    Input('popup-card-custom-position-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def popup_card_custom_position_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdPopupCard/demos/transition_type.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```
