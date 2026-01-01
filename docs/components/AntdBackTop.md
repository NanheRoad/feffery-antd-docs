# AntdBackTop

## 简介源码：`views/AntdBackTop/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '其他'},
                {'title': 'AntdBackTop 回到顶部'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdBackTop 回到顶部', level=2),
        fac.AntdParagraph('用于帮助用户在长页面中快速回到顶部。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callback

- 说明：演示 basic_callback 的用法。

#### 代码
```python
fac.AntdText(id='back-top-demo-text'),
html.Div(
    [
        fac.AntdBackTop(
            id='back-top-callback-demo',
            containerId='back-top-container-callback-demo',
            duration=1,
        ),
        fac.AntdTitle('向下滚动一段距离并点击BackTop按钮', level=4),
    ]
    + [html.Div([i if i % 2 == 0 else html.Br() for i in range(200)])],
    id='back-top-container-callback-demo',
    style={
        'maxHeight': '500px',
        'overflowY': 'auto',
        'position': 'relative',
        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
        'border': '1px solid #f0f0f0',
        'padding': '20px',
    },
)


@app.callback(
    Output('back-top-demo-text', 'children'),
    Input('back-top-callback-demo', 'nClicks'),
)
def back_top_demo_text(nClicks):
    if nClicks is not None:
        return f'nClicks: {nClicks}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
html.Div(
    [
        fac.AntdBackTop(containerId='back-top-container-demo', duration=1),
        fac.AntdTitle('向下滚动一段距离', level=4),
    ]
    + [html.Div([i if i % 2 == 0 else html.Br() for i in range(200)])],
    id='back-top-container-demo',
    style={
        'maxHeight': '500px',
        'overflowY': 'auto',
        'position': 'relative',
        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
        'border': '1px solid #f0f0f0',
        'padding': '20px',
    },
)
```

### container

- 说明：演示 container 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        html.Div(
            [
                fac.AntdBackTop(id='back-top-backtop-demo', duration=1),
                fac.AntdSwitch(
                    id='back-top-container-switch-demo',
                    checkedChildren='containerId',
                    unCheckedChildren='containerSelector',
                    checked=True,
                ),
            ],
            style={'marginBottom': '20px'},
        ),
        fac.AntdSpace(
            [
                html.Div(
                    [fac.AntdTitle('选择方法：containerId', level=4)]
                    + [i if i % 2 == 0 else html.Br() for i in range(200)],
                    id='back-top-container-container-id-demo',
                    style={
                        'maxHeight': '500px',
                        'overflowY': 'auto',
                        'position': 'relative',
                        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
                        'border': '1px solid #f0f0f0',
                        'padding': '20px',
                    },
                ),
                html.Div(
                    [fac.AntdTitle('选择方法：containerSelector', level=4)]
                    + [i if i % 2 == 0 else html.Br() for i in range(200)],
                    id='back-top-container-container-selector-demo',
                    style={
                        'maxHeight': '500px',
                        'overflowY': 'auto',
                        'position': 'relative',
                        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
                        'border': '1px solid #f0f0f0',
                        'padding': '20px',
                    },
                ),
            ],
            style={
                'justifyContent': 'space-between',
                'width': '100%',
            },
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)


@app.callback(
    [
        Output('back-top-backtop-demo', 'containerId'),
        Output('back-top-backtop-demo', 'containerSelector'),
    ],
    Input('back-top-container-switch-demo', 'checked'),
)
def back_top_container_id_demo(checked):
    if checked:
        return 'back-top-container-container-id-demo', None
    else:
        return (
            None,
            'document.querySelector("#back-top-container-container-selector-demo")',
        )
```

### duration

- 说明：演示 duration 的用法。

#### 代码
```python
html.Div(
    [
        fac.AntdDivider('设置duration', innerTextOrientation='left'),
        fac.AntdSlider(
            id='back-top-duration-slider-demo',
            value=1,
            min=0.1,
            max=5,
            step=0.1,
        ),
        fac.AntdBackTop(
            id='back-top-duration-demo',
            containerId='back-top-container-duration-demo',
            duration=3,
        ),
        fac.AntdTitle(id='back-top-duration-title-demo', level=4),
    ]
    + [html.Div([i if i % 2 == 0 else html.Br() for i in range(200)])],
    id='back-top-container-duration-demo',
    style={
        'maxHeight': '500px',
        'overflowY': 'auto',
        'position': 'relative',
        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
        'border': '1px solid #f0f0f0',
        'padding': '20px',
    },
)


@app.callback(
    [
        Output('back-top-duration-demo', 'duration'),
        Output('back-top-duration-title-demo', 'children'),
    ],
    Input('back-top-duration-slider-demo', 'value'),
)
def update_duration(value):
    return value, f'向下滚动一段距离，点击按钮后{value}秒内滚动回顶部'
```

### visibility_height

- 说明：演示 visibility_height 的用法。

#### 代码
```python
html.Div(
    [
        fac.AntdDivider(
            '设置visibilityHeight', innerTextOrientation='left'
        ),
        fac.AntdSlider(
            id='back-top-visibility-height-slider-demo',
            value=200,
            min=50,
            max=1500,
            step=1,
        ),
        fac.AntdBackTop(
            id='back-top-visibility-height-demo',
            containerId='back-top-container-visibility-height-demo',
        ),
        fac.AntdTitle(
            id='back-top-visibility-height-title-demo', level=4
        ),
    ]
    + [
        fac.AntdSpace(
            [
                f'已滚动{(i - 4)*(22.5+8) if i > 4 else 0}px'
                for i in range(200)
            ],
            direction='vertical',
        )
    ],
    id='back-top-container-visibility-height-demo',
    style={
        'maxHeight': '500px',
        'overflowY': 'auto',
        'position': 'relative',
        'backgroundColor': 'rgba(240, 240, 240, 0.2)',
        'border': '1px solid #f0f0f0',
        'padding': '20px',
    },
)


@app.callback(
    [
        Output('back-top-visibility-height-demo', 'visibilityHeight'),
        Output('back-top-visibility-height-title-demo', 'children'),
    ],
    Input('back-top-visibility-height-slider-demo', 'value'),
)
def update_duration(value):
    return value, f'向下滚动{value}px出现按钮'
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- duration (number; default 0.45):
    回到顶部过程耗时，单位：秒  默认值：`0.45`.

- visibilityHeight (number; default 400):
    回到顶部按钮显示时对应的页面滚动像素高度阈值  默认值：`400`.

- containerId (string; optional):
    滚动事件监听的特定目标容器id.

- containerSelector (string; optional):
    滚动事件监听的特定目标容器js选择代码，优先级低于containerId.

- nClicks (number; default 0):
    监听回到顶部按钮累计被点击次数  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
