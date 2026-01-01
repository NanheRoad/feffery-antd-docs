# AntdModal

## 简介源码：`views/AntdModal/intro.py`
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
                {'title': 'AntdModal 对话框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdModal 对话框', level=2),
        fac.AntdParagraph('用于渲染弹出式对话框。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-callback-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-callback-demo',
        title='对话框示例',
        renderFooter=True,
    ),
    html.Pre(id='modal-callback-demo-output'),
]

...

@app.callback(
    Output('modal-callback-demo', 'visible'),
    Input('modal-callback-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def handle_modal_visible(nClicks):
    return True


@app.callback(
    Output('modal-callback-demo-output', 'children'),
    [
        Input('modal-callback-demo', 'okCounts'),
        Input('modal-callback-demo', 'cancelCounts'),
        Input('modal-callback-demo', 'closeCounts'),
    ],
    prevent_initial_call=True,
)
def handle_modal_callback_demo(okCounts, cancelCounts, closeCounts):
    return json.dumps(
        dict(
            okCounts=okCounts,
            cancelCounts=cancelCounts,
            closeCounts=closeCounts,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-basic-demo-open', type='primary'
    ),
    fac.AntdModal('示例内容', id='modal-basic-demo', title='对话框示例'),
]

...

@app.callback(
    Output('modal-basic-demo', 'visible'),
    Input('modal-basic-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_basic_demo(nClicks):
    return True
```

### centered

- 说明：演示 centered 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-centered-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-centered-demo',
        title='对话框示例',
        centered=True,
    ),
]

...

@app.callback(
    Output('modal-centered-demo', 'visible'),
    Input('modal-centered-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_centered_demo(nClicks):
    return True
```

### confirm_loading

- 说明：演示 confirm_loading 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框',
        id='modal-confirm-loading-demo-open',
        type='primary',
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-confirm-loading-demo',
        title='对话框示例',
        confirmAutoSpin=True,
        loadingOkText='运算中',
        okClickClose=False,
        renderFooter=True,
    ),
]

...

@app.callback(
    Output('modal-confirm-loading-demo', 'visible'),
    Input('modal-confirm-loading-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_confirm_loading_demo(nClicks):
    return True


@app.callback(
    Output('modal-confirm-loading-demo', 'confirmLoading'),
    Input('modal-confirm-loading-demo', 'okCounts'),
    prevent_initial_call=True,
)
def modal_confirm_loading_reset(okCounts):
    time.sleep(2)

    return False
```

### custom_footer_button

- 说明：演示 custom_footer_button 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-custom-button-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-custom-button-demo',
        title='对话框示例',
        renderFooter=True,
        okText='Ok',
        cancelText='Cancel',
        cancelButtonProps={'danger': True},
    ),
]

...

@app.callback(
    Output('modal-custom-button-demo', 'visible'),
    Input('modal-custom-button-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_custom_button_demo(nClicks):
    return True
```

### loading

- 说明：演示 loading 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-loading-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-loading-demo',
        title='loading状态示例',
        loading=True,
    ),
]

...

@app.callback(
    Output('modal-loading-demo', 'visible'),
    Input('modal-loading-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_loading_demo(nClicks):
    return True
```

### prevent_close

- 说明：演示 prevent_close 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-prevent-close-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-prevent-close-demo',
        title='对话框示例',
        preventClose=True,
        okClickClose=False,
    ),
    fac.AntdModal(
        '确认要关闭模态框吗',
        id='modal-prevent-close-confirm-demo',
        title='关闭二次确认',
        renderFooter=True,
        zIndex=99999,
    ),
]

...

@app.callback(
    Output('modal-prevent-close-demo', 'visible'),
    Input('modal-prevent-close-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def open_modal_prevent_close(nClicks):
    return True


@app.callback(
    Output('modal-prevent-close-confirm-demo', 'visible'),
    Input('modal-prevent-close-demo', 'cancelCounts'),
    prevent_initial_call=True,
)
def open_modal_prevent_close_confirm(cancelCounts):
    return True


@app.callback(
    Output('modal-prevent-close-demo', 'visible', allow_duplicate=True),
    Input('modal-prevent-close-confirm-demo', 'okCounts'),
    prevent_initial_call=True,
)
def close_modal_prevent_close_confirm(okCounts):
    return False
```

### render_footer

- 说明：演示 render_footer 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-footer-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-footer-demo',
        title='对话框示例',
        renderFooter=True,
    ),
]

...

@app.callback(
    Output('modal-footer-demo', 'visible'),
    Input('modal-footer-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_footer_demo(nClicks):
    return True
```

### responsive_width

- 说明：演示 responsive_width 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框',
        id='modal-responsive-width-demo-open',
        type='primary',
    ),
    fac.AntdModal(
        '示例内容',
        id='modal-responsive-width-demo',
        title='对话框示例',
        width={
            'xs': '100vw',
            'sm': '100vw',
            'md': '100vw',
            'lg': '60vw',
            'xl': '60vw',
            'xxl': '60vw',
        },
    ),
]

...

@app.callback(
    Output('modal-responsive-width-demo', 'visible'),
    Input('modal-responsive-width-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_responsive_width_demo(nClicks):
    return True
```

### width

- 说明：演示 width 的用法。

#### 代码
```python
[
    fac.AntdButton(
        '触发示例对话框', id='modal-width-demo-open', type='primary'
    ),
    fac.AntdModal(
        '示例内容', id='modal-width-demo', title='对话框示例', width='75vw'
    ),
]

...

@app.callback(
    Output('modal-width-demo', 'visible'),
    Input('modal-width-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_width_demo(nClicks):
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

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- visible (boolean; default False):
    监听或设置对话框是否可见  默认值：`False`.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- renderFooter (boolean; default False):
    是否渲染底部操作按钮  默认值：`False`.

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

- width (dict; default 520):
    对话框像素宽度  默认值：`520`.

    `width` is a number | string | dict with keys:

    - xs (number | string; optional):
        对应页面宽度<576px的响应式断点.

    - sm (number | string; optional):
        对应页面宽度≥576px的响应式断点.

    - md (number | string; optional):
        对应页面宽度≥768px的响应式断点.

    - lg (number | string; optional):
        对应页面宽度≥992px的响应式断点.

    - xl (number | string; optional):
        对应页面宽度≥1200px的响应式断点.

    - xxl (number | string; optional):
        对应页面宽度≥1600px的响应式断点.

- centered (boolean; default False):
    是否垂直居中显示对话框  默认值：`False`.

- keyboard (boolean; default True):
    是否支持键盘esc关闭对话框  默认值：`True`.

- closable (boolean; default True):
    是否显示右上角的关闭按钮  默认值：`True`.

- mask (boolean; default True):
    是否显示背景遮罩  默认值：`True`.

- maskClosable (boolean; default True):
    是否允许点击遮罩层关闭对话框  默认值：`True`.

- okClickClose (boolean; default True):
    是否点击确认按钮触发对话框关闭  默认值：`True`.

- preventClose (boolean; default False):
    是否阻止通过点击关闭图标、点击遮罩层区域、点击取消、按下ESC等方式自动触发的对话框关闭行为  默认值：`False`.

- zIndex (number; default 1000):
    模态框z-index  默认值：`1000`.

- okCounts (number; default 0):
    监听确认按钮累计点击次数  默认值：`0`.

- cancelCounts (number; default 0):
    监听取消按钮累计点击次数  默认值：`0`.

- closeCounts (number; default 0):
    监听关闭按钮累计点击次数  默认值：`0`.

- confirmAutoSpin (boolean; default False):
    是否在每次确认按钮点击之后，自动更新`confirmLoading=True`  默认值：`False`.

- loadingOkText (a list of or a singular dash component, string or number; optional):
    组件型，`confirmLoading=True`时，确认按钮的内容.

- confirmLoading (boolean; default False):
    底部确认按钮是否处于加载中状态  默认值：`False`.

- transitionType (a value equal to: 'none', 'fade', 'zoom', 'zoom-big', 'zoom-big-fast', 'slide-up', 'slide-down', 'slide-left', 'slide-right', 'move-up', 'move-down', 'move-left', 'move-right'; default 'zoom'):
    模态框显隐动画类型，可选项有`'none'`、`'fade'`、`'zoom'`、`'zoom-big'`、`'zoom-big-fast'`、`'slide-up'`、`'slide-down'`、`'slide-left'`、`'slide-right'`、`'move-up'`、`'move-down'`、`'move-left'`、`'move-right'`
    默认值：`'zoom'`.

- forceRender (boolean; default False):
    是否在初始化模态框未显示时，强制渲染模态框内部元素  默认值：`False`.

- destroyOnClose (boolean; default True):
    是否在模态框关闭后自动销毁内部元素  默认值：`True`.

- loading (boolean; default False):
    是否整体渲染为加载中状态  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
