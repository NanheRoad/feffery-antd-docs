# AntdQRCode

## 简介源码：`views/AntdQRCode/intro.py`
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
                {'title': 'AntdQRCode 二维码'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdQRCode 二维码', level=2),
        fac.AntdParagraph(
            '能够将文本转换生成二维码的组件，支持自定义配色和 Logo 配置。'
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### auto_spin

- 说明：演示 auto_spin 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdQRCode(
            id='auto-spin-qrcode-demo',
            value='https://fac.feffery.tech/',
            autoSpin=True
        ),
        fac.AntdButton(
            '重新生成',
            id='auto-spin-qrcode-demo-button',
            type='primary'
        ),
    ],
    direction='vertical',
    align='center',
)

...

@app.callback(
    Output('auto-spin-qrcode-demo', 'value'),
    Input('auto-spin-qrcode-demo-button', 'nClicks'),
    State('auto-spin-qrcode-demo', 'value'),
    prevent_initial_call=True,
)
def auto_spin_qrcode_demo_input_callback(nClicks, value):
    if nClicks:
        time.sleep(1)
        if value == 'https://fac.feffery.tech/':
            return 'https://ant.design/'
        elif value == 'https://ant.design/':
            return 'https://fac.feffery.tech/'
    
    return dash.no_update
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdQRCode(
            id='qrcode-callbacks',
            value='https://fac.feffery.tech/',
            status='expired',
        ),
        html.Div(id='qrcode-callbacks-demo-output'),
        dcc.Interval(id='qrcode-callbacks-demo-interval', interval=3000),
    ],
    direction='vertical',
)

...

@app.callback(
    [
        Output('qrcode-callbacks-demo-output', 'children'),
        Output('qrcode-callbacks', 'status'),
    ],
    Input('qrcode-callbacks', 'refreshClicks'),
    prevent_initial_call=True,
)
def qrcode_callback_demo(refreshClicks):
    if refreshClicks:
        return [f'refreshClicks: {refreshClicks}', 'active']


@app.callback(
    Output('qrcode-callbacks', 'status', allow_duplicate=True),
    Input('qrcode-callbacks-demo-interval', 'n_intervals'),
    State('qrcode-callbacks', 'status'),
    prevent_initial_call=True,
)
def qrcode_callback_demo_interval(n_intervals, status):
    if n_intervals and status == 'active':
        return 'expired'

    return dash.no_update
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdQRCode(
            id='basic-qrcode-demo',
        ),
        fac.AntdInput(
            id='basic-qrcode-demo-input',
            placeholder='-',
            maxLength=60,
            value='https://fac.feffery.tech/',
        ),
    ],
    direction='vertical',
    align='center',
)

...

@app.callback(
    Output('basic-qrcode-demo', 'value'),
    Input('basic-qrcode-demo-input', 'value'),
)
def basic_qrcode_demo_input_callback(input_value):
    if input_value:
        return input_value
    return '-'
```

### border

- 说明：演示 border 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdQRCode(value='https://fac.feffery.tech/', bordered=True),
                fac.AntdText('bordered：True'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdQRCode(value='https://fac.feffery.tech/', bordered=False),
                fac.AntdText('bordered：False'),
            ]
        ),
    ],
    direction='vertical',
)
```

### custom_color

- 说明：演示 custom_color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdQRCode(value='https://fac.feffery.tech/', color='#52c41a'),
        fac.AntdQRCode(
            value='https://fac.feffery.tech/',
            color='#1677ff',
            bgColor='#f5f5f5',
        ),
    ]
)
```

### custom_render_type

- 说明：演示 custom_render_type 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='qrcode-custom-render-type-demo-segmented',
            options=[
                {'label': 'canvas', 'value': 'canvas'},
                {'label': 'svg', 'value': 'svg'},
            ],
            defaultValue='canvas',
        ),
        html.Div(id='qrcode-custom-render-type-demo-output'),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('qrcode-custom-render-type-demo-output', 'children'),
    Input('qrcode-custom-render-type-demo-segmented', 'value'),
)
def qrcode_custom_render_type_demo_input_callback(input_value):
    return fac.AntdQRCode(type=input_value, value='https://fac.feffery.tech/')
```

### custom_size

- 说明：演示 custom_size 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCompact(
            [
                fac.AntdButton(
                    'Smaller',
                    id='qrcode-size-smaller-button',
                    icon=fac.AntdIcon(icon='antd-minus'),
                ),
                fac.AntdButton(
                    'Larger',
                    id='qrcode-size-larger-button',
                    icon=fac.AntdIcon(icon='antd-plus'),
                ),
            ]
        ),
        fac.AntdQRCode(
            id='qrcode-size-demo',
            errorLevel='H',
            size=160,
            iconSize=40,
            value='https://fac.feffery.tech/',
            icon='/assets/imgs/fac-logo.svg',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    [
        Output('qrcode-size-demo', 'size'),
        Output('qrcode-size-demo', 'iconSize'),
    ],
    [
        Input('qrcode-size-smaller-button', 'nClicks'),
        Input('qrcode-size-larger-button', 'nClicks'),
    ],
    State('qrcode-size-demo', 'size'),
    prevent_initial_call=True,
)
def qrcode_size_demo_input_callback(smaller_clicks, larger_clicks, size):
    triggered_id = dash.ctx.triggered_id
    if triggered_id == 'qrcode-size-smaller-button':
        new_size = size - 10
        if new_size <= 48:
            return [48, 12]
        return [new_size, new_size / 4]
    if triggered_id == 'qrcode-size-larger-button':
        new_size = size + 10
        if new_size >= 300:
            return [300, 75]
        return [new_size, new_size / 4]

    return dash.no_update
```

### download_qrcode

- 说明：演示 download_qrcode 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='qrcode-download-demo-segmented',
            options=[
                {'label': 'canvas', 'value': 'canvas'},
                {'label': 'svg', 'value': 'svg'},
            ],
            defaultValue='canvas',
        ),
        fac.AntdQRCode(id='qrcode', value='https://fac.feffery.tech/'),
        fac.AntdButton(
            '下载',
            id='qrcode-download-button',
            type='primary',
        ),
    ],
    id='myqrcode',
    direction='vertical',
)

...

@app.callback(
    [Output('qrcode', 'type'), Output('qrcode', 'icon')],
    Input('qrcode-download-demo-segmented', 'value'),
)
def qrcode_download_demo_input_callback(input_value):
    if input_value == 'canvas':
        return ['canvas', '/assets/imgs/fac-logo.svg']
    elif input_value == 'svg':
        return [
            'svg',
            'https://gw.alipayobjects.com/zos/rmsportal/KDpgvguMpGfqaHPjicRK.svg',
        ]
    return dash.no_update


app.clientside_callback(
    '''
    (nClicks, type) => {
        function doDownload(url, fileName) {
            const a = document.createElement('a');
            a.download = fileName;
            a.href = url;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        };
        const downloadCanvasQRCode = () => {
            const canvas = document.getElementById('myqrcode')?.querySelector('canvas');
            if (canvas) {
                const url = canvas.toDataURL();
                doDownload(url, 'QRCode.png');
            }
        };
        const downloadSvgQRCode = () => {
            const svg = document.getElementById('myqrcode')?.querySelector('svg');
            const svgData = new XMLSerializer().serializeToString(svg);
            const blob = new Blob([svgData], {
                type: 'image/svg+xml;charset=utf-8',
            });
            const url = URL.createObjectURL(blob);
            doDownload(url, 'QRCode.svg');
        };
        if (nClicks) {
            if (type === 'canvas') {
                downloadCanvasQRCode();
            } else if (type === 'svg') {
                downloadSvgQRCode();
            }
        }
    }
    ''',
    Input('qrcode-download-button', 'nClicks'),
    State('qrcode', 'type'),
    prevent_initial_call=True,
)
```

### error_level

- 说明：演示 error_level 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        html.Div(id='qrcode-error-level-demo-output'),
        fac.AntdSegmented(
            id='qrcode-error-level-demo-segmented',
            options=[
                {'label': 'L', 'value': 'L'},
                {'label': 'M', 'value': 'M'},
                {'label': 'Q', 'value': 'Q'},
                {'label': 'H', 'value': 'H'},
            ],
            value='L',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('qrcode-error-level-demo-output', 'children'),
    Input('qrcode-error-level-demo-segmented', 'value'),
)
def qrcode_custom_render_type_demo_input_callback(input_value):
    return fac.AntdQRCode(
        errorLevel=input_value,
        value='https://gw.alipayobjects.com/zos/rmsportal/KDpgvguMpGfqaHPjicRK.svg',
    )
```

### high_usage

- 说明：演示 high_usage 的用法。

#### 代码
```python
fac.AntdPopover(
    fac.AntdButton('Hover me', type='primary'),
    content=fac.AntdQRCode(
        value='https://fac.feffery.tech/', bordered=False
    ),
    overlayInnerStyle={'padding': 0},
)
```

### icon_size

- 说明：演示 icon_size 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSegmented(
            id='qrcode-icon-size-demo-segmented',
            options=[
                {'label': '默认', 'value': '默认'},
                {'label': '同比例', 'value': '同比例'},
                {'label': '自定义', 'value': '自定义'},
            ],
            defaultValue='默认',
        ),
        fac.AntdQRCode(
            id='qrcode-icon-size',
            value='https://fac.feffery.tech/',
            icon='/assets/imgs/fac-logo.svg',
        ),
    ],
    id='myqrcode',
    direction='vertical',
)

...

@app.callback(
    Output('qrcode-icon-size', 'iconSize'),
    Input('qrcode-icon-size-demo-segmented', 'value'),
)
def qrcode_download_demo_input_callback(input_value):
    if input_value == '同比例':
        return 60
    elif input_value == '自定义':
        return {
            'width': 60,
            'height': 80,
        }
    return dash.no_update
```

### qrcode_icon

- 说明：演示 qrcode_icon 的用法。

#### 代码
```python
fac.AntdQRCode(
    errorLevel='H',
    value='https://fac.feffery.tech/',
    icon='/assets/imgs/fac-logo.svg'
)
```

### qrcode_status

- 说明：演示 qrcode_status 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdQRCode(value='https://fac.feffery.tech/', status='active'),
        fac.AntdQRCode(value='https://fac.feffery.tech/', status='expired'),
        fac.AntdQRCode(value='https://fac.feffery.tech/', status='loading'),
        fac.AntdQRCode(value='https://fac.feffery.tech/', status='scanned'),
    ],
    gap='middle',
    wrap='wrap'
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- value (string; optional):
    二维码解析结果.

- type (a value equal to: 'canvas', 'svg'; default 'canvas'):
    渲染方式，可选项有`'canvas'`、`'svg'`  默认值：`'canvas'`.

- icon (string; optional):
    二维码内嵌图片地址.

- size (number; default 160):
    二维码像素边长  默认值：`160`.

- iconSize (dict; default 40):
    二维码内嵌图片像素边长  默认值：`40`.

    `iconSize` is a number | dict with keys:

    - width (number; optional)

    - height (number; optional)

- color (string; default '#000'):
    二维码颜色  默认值：`'#000'`.

- bgColor (string; default 'transparent'):
    二维码背景颜色  默认值：`'transparent'`.

- bordered (boolean; default True):
    二维码是否渲染边框  默认值：`True`.

- errorLevel (a value equal to: 'L', 'M', 'Q', 'H'; default 'M'):
    二维码纠错级别，可选项有`'L'`、`'M'`、`'Q'`、`'H'`  默认值：`'M'`.

- status (a value equal to: 'active', 'expired', 'loading', 'scanned'; default 'active'):
    二维码状态，可选项有`'active'`、`'expired'`、`'loading'`、`'scanned'`
    默认值：`'active'`.

- expires (number; optional):
    当前二维码过期时间，单位：秒，到期后二维码状态将会被强制更新为`'expired'`.

- autoSpin (boolean; default False):
    是否在`value`处于回调更新中时，自动切换为`loading`状态  默认值：`False`.

- refreshClicks (number; default 0):
    监听当前"点击刷新"按钮累计点击次数，仅在`status`为`'expired'`时有效  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
