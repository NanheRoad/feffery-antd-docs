# AntdPopconfirm

## 简介源码：`views/AntdPopconfirm/intro.py`
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
                {'title': 'AntdPopconfirm 气泡确认框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdPopconfirm 气泡确认框', level=2),
        fac.AntdParagraph('用于实现二次确认功能，相较于对话框更加简便。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdPopconfirm(
            fac.AntdButton('触发'), id='popconfirm-demo', title='确认继续'
        ),
        html.Pre(id='popconfirm-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('popconfirm-demo-output', 'children'),
    Input('popconfirm-demo', 'confirmCounts'),
    Input('popconfirm-demo', 'cancelCounts'),
    prevent_initial_call=True,
)
def popconfirm_callback_demo(confirmCounts, cancelCounts):
    return json.dumps(
        {'confirmCounts': confirmCounts, 'cancelCounts': cancelCounts}, indent=4
    )
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdPopconfirm(fac.AntdButton('触发'), title='确认继续')
```

### color

- 说明：演示 color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='popover-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdPopover(
            fac.AntdButton('锚点示例'),
            id='popover-color-demo',
            title='气泡卡片示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('popover-color-demo', 'color'),
        Output('popover-color-demo', 'content'),
    ],
    Input('popover-color-demo-input', 'color'),
)
def popover_color_demo(color):
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
        fac.AntdSwitch(id='popconfirm-open-switch', checked=False),
        fac.AntdPopconfirm(
            fac.AntdButton('触发'),
            id='popconfirm-open-demo',
            title='确认继续',
        ),
    ]
)

...

@app.callback(
    Output('popconfirm-open-demo', 'open'),
    Input('popconfirm-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_popconfirm_open(checked):
    return checked
```

### custom_description

- 说明：演示 custom_description 的用法。

#### 代码
```python
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', description='描述信息示例'
)
```

### custom_icon

- 说明：演示 custom_icon 的用法。

#### 代码
```python
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', icon='🤔'
)
```

### custom_style

- 说明：演示 custom_style 的用法。

#### 代码
```python
fac.AntdPopconfirm(
    fac.AntdButton('触发'),
    title='确认继续',
    description='内容示例' * 10,
    styles={'root': {'width': 400}},
)
```

### hide_arrow

- 说明：演示 hide_arrow 的用法。

#### 代码
```python
fac.AntdPopconfirm(
    fac.AntdButton('触发'), title='确认继续', arrow='hide'
)
```

### placement

- 说明：演示 placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdPopconfirm(
            fac.AntdButton(placement),
            title='确认继续',
            description=f'placement="{placement}"',
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
            'leftTop',
            'leftBottom',
            'rightTop',
            'rightBottom',
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
            fac.AntdPopconfirm(
                fac.AntdButton('示例1', type='primary'),
                title='示例',
            ),
            style={'position': 'absolute', 'left': 15, 'bottom': 15},
        ),
        html.Span(
            fac.AntdPopconfirm(
                fac.AntdButton('示例2', type='primary'),
                title='示例',
            ),
            style={'position': 'absolute', 'right': 15, 'top': 15},
        ),
        html.Span(
            fac.AntdPopconfirm(
                fac.AntdButton('示例3', type='primary'),
                title='示例',
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
    组件型，气泡确认框挂载元素.

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

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- icon (a list of or a singular dash component, string or number; optional):
    组件型，提示图标.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- description (a list of or a singular dash component, string or number; optional):
    组件型，描述内容.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight', 'leftTop', 'leftBottom', 'rightTop', 'rightBottom'; default 'top'):
    气泡确认框弹出位置，可选项有`'top'`、`'left'`、`'right'`、`'bottom'`、`'topLeft'`、`'topRight'`、`'bottomLeft'`、`'bottomRight'`、`'leftTop'`、`'leftBottom'`、`'rightTop'`、`'rightBottom'`
    默认值：`'top'`.

- mouseEnterDelay (number; default 0.1):
    从鼠标移入挂载元素，到气泡确认框显示的延时，单位：秒  默认值：`0.1`.

- mouseLeaveDelay (number; default 0.1):
    从鼠标移出挂载元素，到气泡确认框消失的延时，单位：秒  默认值：`0.1`.

- okText (a list of or a singular dash component, string or number; optional):
    组件型，确认按钮内容.

- okButtonProps (dict; optional):
    配置确认按钮相关参数.

    `okButtonProps` is a dict with keys:

    - size (a value equal to: 'small', 'middle', 'large'; optional):
        按钮尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

    - type (a value equal to: 'primary', 'ghost', 'dashed', 'link', 'text', 'default'; optional):
        按钮类型，可选项有`'default'`、`'primary'`、`'ghost'`、`'dashed'`、`'link'`、`'text'`
        默认值：`'default'`.

    - danger (boolean; optional):
        按钮是否呈现危险样式  默认值：`False`.

    - disabled (boolean; optional):
        按钮是否呈现禁用状态  默认值：`False`.

    - shape (a value equal to: 'circle', 'round'; optional):
        按钮形状，可选项有`'default'`、`'circle'`、`'round'`  默认值：`'default'`.

    - style (dict; optional):
        按钮css样式.

    - className (string; optional):
        按钮css类名.

- cancelText (a list of or a singular dash component, string or number; optional):
    组件型，取消按钮内容.

- cancelButtonProps (dict; optional):
    配置取消按钮相关参数.

    `cancelButtonProps` is a dict with keys:

    - size (a value equal to: 'small', 'middle', 'large'; optional):
        按钮尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

    - type (a value equal to: 'primary', 'ghost', 'dashed', 'link', 'text', 'default'; optional):
        按钮类型，可选项有`'default'`、`'primary'`、`'ghost'`、`'dashed'`、`'link'`、`'text'`
        默认值：`'default'`.

    - danger (boolean; optional):
        按钮是否呈现危险样式  默认值：`False`.

    - disabled (boolean; optional):
        按钮是否呈现禁用状态  默认值：`False`.

    - shape (a value equal to: 'circle', 'round'; optional):
        按钮形状，可选项有`'default'`、`'circle'`、`'round'`  默认值：`'default'`.

    - style (dict; optional):
        按钮css样式.

    - className (string; optional):
        按钮css类名.

- showCancel (boolean; default True):
    是否显示取消按钮  默认值：`True`.

- confirmCounts (number; default 0):
    监听确认按钮累计点击次数  默认值：`0`.

- cancelCounts (number; default 0):
    监听取消按钮累计点击次数  默认值：`0`.

- trigger (a value equal to: 'hover', 'focus', 'click' | list of a value equal to: 'hover', 'focus', 'click's; default 'click'):
    气泡确认框触发行为，可选项有`'hover'`、`'focus'`、`'click'`，可多选组合  默认值：`'click'`.

- zIndex (number; optional):
    气泡确认框z-index.

- arrow (a value equal to: 'show', 'hide', 'center'; default 'show'):
    指示箭头显示形式，可选项有`'show'`、`'hide'`、`'center'`  默认值：`'show'`.

- fresh (boolean; default False):
    是否保持内容更新  默认值：`False`.

- open (boolean; default False):
    监听或设置气泡确认框的显示状态  默认值：`False`.

- permanent (boolean; default False):
    是否保持气泡确认框显示/隐藏  默认值：`False`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    悬浮层渲染挂载父节点策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

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
