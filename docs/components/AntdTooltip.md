# AntdTooltip

## 简介源码：`views/AntdTooltip/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdTooltip 信息提示'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTooltip 信息提示', level=2),
        fac.AntdParagraph('用于为指定元素添加额外信息提示。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例'
)
```

### color

- 说明：演示 color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='tooltip-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-color-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('tooltip-color-demo', 'color'),
        Output('tooltip-color-demo', 'title'),
    ],
    Input('tooltip-color-demo-input', 'color'),
)
def tooltip_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]
```

### control_open

- 说明：演示 control_open 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSwitch(id='tooltip-open-switch', checked=False),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-open-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    Output('tooltip-open-demo', 'open'),
    Input('tooltip-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_tooltip_open(checked):
    return checked
```

### custom_style

- 说明：演示 custom_style 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点示例'),
    title='内容示例' * 50,
    styles={
        'root': {'width': 250},
        'body': {'maxHeight': 150, 'overflowY': 'auto'},
    },
)
```

### hide_arrow

- 说明：演示 hide_arrow 的用法。

#### 代码
```python
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例', arrow='hide'
)
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTooltip(
            fac.AntdButton(placement),
            title='信息提示示例',
            placement=placement,
        )
        for placement in [
            'top',
            'left',
            'right',
            'bottom',
            'topLeft',
            'topRight',
            'bottomLeft',
            'bottomRight',
        ]
    ],
    wrap=True,
)
```

### question_with_absolute_position

- 说明：演示 question_with_absolute_position 的用法。

#### 代码
```python
html.Div(
    [
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例1', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'left': 15, 'bottom': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例2', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'top': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例3', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'bottom': 15},
        ),
    ],
    style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，文字提示挂载目标.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素（包含箭头、内容元素）css样式.

    - body (dict; optional):
        内容元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素（包含箭头、内容元素）css类名.

    - body (string; optional):
        内容元素css类名.

- title (a list of or a singular dash component, string or number; optional):
    组件型，文字提示内容.

- placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight'; default 'top'):
    文字提示弹出方向，可选项有`'top'`、`'left'`、`'right'`、`'bottom'`、`'topLeft'`、`'topRight'`、`'bottomLeft'`、`'bottomRight'`、`'leftTop'`、`'leftBottom'`、`'rightTop'`、`'rightBottom'`
    默认值：`'top'`.

- color (string; optional):
    背景颜色.

- mouseEnterDelay (number; default 0.1):
    鼠标移入到文字提示弹出延时，单位：秒  默认值：`0.1`.

- mouseLeaveDelay (number; default 0.1):
    鼠标移出到文字提示消失延时，单位：秒  默认值：`0.1`.

- trigger (a value equal to: 'hover', 'focus', 'click' | list of a value equal to: 'hover', 'focus', 'click's; default 'hover'):
    触发方式，可选项有`'hover'`、`'focus'`、`'click'`，可多选  默认值：`'hover'`.

- zIndex (number; optional):
    文字提示卡片z-index.

- arrow (a value equal to: 'show', 'hide', 'center'; default 'show'):
    文字提示卡片附带箭头显示形式，可选项有`'show'`、`'hide'`、`'center'`  默认值：`'show'`.

- fresh (boolean; default False):
    是否始终保持更新内容  默认值：`False`.

- open (boolean; default False):
    监听或设置当前文字提示卡片的展开状态  默认值：`False`.

- permanent (boolean; default False):
    是否保持文字提示卡片处于`open`对应状态不变  默认值：`False`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    文字提示卡片展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
