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
