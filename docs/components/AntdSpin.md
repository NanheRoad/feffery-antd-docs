# AntdSpin

## 简介源码：`views/AntdSpin/intro.py`
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
                {'title': 'AntdSpin 加载动画'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSpin 加载动画', level=2),
        fac.AntdParagraph('用于为正在加载中的内容添加加载动画。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例', id='spin-basic-demo-trigger', style={'marginBottom': 10}
    ),
    fac.AntdSpin(fac.AntdText(id='spin-basic-demo-output'), text='回调中'),
]

...

@app.callback(
    Output('spin-basic-demo-output', 'children'),
    Input('spin-basic-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def spin_basic_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### custom_indicator

- 说明：演示 custom_indicator 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='spin-custom-demo-trigger',
        style={'marginBottom': 10},
    ),
    fac.AntdSpin(
        fac.AntdText('nClicks: 0', id='spin-custom-demo-output'),
        indicator=fuc.FefferyExtraSpinner(type='heart'),
    ),
]

...

@app.callback(
    Output('spin-custom-demo-output', 'children'),
    Input('spin-custom-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def spin_custom_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### custom_wrapper_css

- 说明：演示 custom_wrapper_css 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='spin-custom-wrapper-demo-trigger',
        style={'marginBottom': 10},
    ),
    # 动态注入css片段
    fuc.FefferyStyle(
        rawStyle="""
.spin-custom-wrapper {
    height: 100%;
}
"""
    ),
    html.Div(
        fac.AntdSpin(
            fac.AntdText(id='spin-custom-wrapper-demo-output'),
            text='回调中',
            wrapperClassName='spin-custom-wrapper',
        ),
        style={'height': 500, 'border': '1px dashed #bae7ff'},
    ),
]

...

@app.callback(
    Output('spin-custom-wrapper-demo-output', 'children'),
    Input('spin-custom-wrapper-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def spin_custom_wrapper_demo(nClicks):
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
            fac.AntdButton('按钮1', id='spin-exclude-demo-trigger1'),
            fac.AntdButton('按钮2', id='spin-exclude-demo-trigger2'),
        ],
        style={'width': '100%', 'marginBottom': 10},
    ),
    fac.AntdSpin(
        [
            fac.AntdParagraph(id='spin-exclude-demo-output1'),
            fac.AntdParagraph(id='spin-exclude-demo-output2'),
        ],
        text='回调中',
        listenPropsMode='exclude',
        excludeProps=['spin-exclude-demo-output1.children'],
    ),
]

...

@app.callback(
    Output('spin-exclude-demo-output1', 'children'),
    Input('spin-exclude-demo-trigger1', 'nClicks'),
    prevent_initial_call=True,
)
def spin_exclude_demo1(nClicks):
    time.sleep(1)

    return f'按钮1: {nClicks}'


@app.callback(
    Output('spin-exclude-demo-output2', 'children'),
    Input('spin-exclude-demo-trigger2', 'nClicks'),
    prevent_initial_call=True,
)
def spin_exclude_demo2(nClicks):
    time.sleep(1)

    return f'按钮2: {nClicks}'
```

### fullscreen

- 说明：演示 fullscreen 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '触发示例',
            id='spin-fullscreen-demo-trigger',
            style={'marginBottom': 10},
        ),
        fac.AntdSpin(
            fac.AntdText(id='spin-fullscreen-demo-output'), fullscreen=True
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('spin-fullscreen-demo-output', 'children'),
    Input('spin-fullscreen-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def spin_fullscreen_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
```

### include_mode

- 说明：演示 include_mode 的用法。

#### 代码
```python
[
    fac.AntdSpace(
        [
            fac.AntdButton('按钮1', id='spin-include-demo-trigger1'),
            fac.AntdButton('按钮2', id='spin-include-demo-trigger2'),
        ],
        style={'width': '100%', 'marginBottom': 10},
    ),
    fac.AntdSpin(
        [
            fac.AntdParagraph(id='spin-include-demo-output1'),
            fac.AntdParagraph(id='spin-include-demo-output2'),
        ],
        text='回调中',
        listenPropsMode='include',
        includeProps=['spin-include-demo-output1.children'],
    ),
]

...

@app.callback(
    Output('spin-include-demo-output1', 'children'),
    Input('spin-include-demo-trigger1', 'nClicks'),
    prevent_initial_call=True,
)
def spin_include_demo1(nClicks):
    time.sleep(1)

    return f'按钮1: {nClicks}'


@app.callback(
    Output('spin-include-demo-output2', 'children'),
    Input('spin-include-demo-trigger2', 'nClicks'),
    prevent_initial_call=True,
)
def spin_include_demo2(nClicks):
    time.sleep(1)

    return f'按钮2: {nClicks}'
```

### percent

- 说明：演示 percent 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例',
        id='spin-percent-demo-trigger',
        style={'marginBottom': 10},
    ),
    fac.AntdSpin(
        fac.AntdText(id='spin-percent-demo-output'),
        percent='auto',
    ),
]

...

@app.callback(
    Output('spin-percent-demo-output', 'children'),
    Input('spin-percent-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def spin_percent_demo(nClicks):
    time.sleep(2)

    return f'nClicks: {nClicks}'
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

- wrapperClassName (string | dict; optional):
    外层容器css类名.

- spinning (boolean; default False):
    是否处于加载中状态.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    默认加载状态图标的尺寸，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- delay (number; optional):
    加载动画渲染延时，单位：毫秒  默认值：`0`.

- text (string; optional):
    加载动画提示文字.

- fullscreen (boolean; default False):
    是否开启全屏模式  默认值：`False`.

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

- indicator (a list of or a singular dash component, string or number; optional):
    组件型，自定义加载状态图标.

- manual (boolean; default False):
    是否开启手动控制模式，开启后是否处于加载状态将由`spinning`参数控制，与内部元素参与的回调状态无关
    默认值：`False`.

- percent (number | a value equal to: 'auto'; optional):
    控制加载中状态下的环状进度渲染形式，传入0到100之间数值型时表示实际进度，传入`'auto'`时会预估一个永远不会停止的进度.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
