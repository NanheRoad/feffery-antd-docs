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

## 示例源码（demos）

### `views/AntdQRCode/demos/auto_spin.py`
```python
import feffery_antd_components as fac
import dash
import time
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdQRCode(
                id='auto-spin-qrcode-demo',
                value='https://fac.feffery.tech/',
                autoSpin=True,
            ),
            fac.AntdButton(
                '重新生成', id='auto-spin-qrcode-demo-button', type='primary'
            ),
        ],
        direction='vertical',
        align='center',
    )

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/basic_callbacks.py`
```python
import dash
from dash import html, dcc
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


@app.callback(
    Output('basic-qrcode-demo', 'value'),
    Input('basic-qrcode-demo-input', 'value'),
)
def basic_qrcode_demo_input_callback(input_value):
    if input_value:
        return input_value
    return '-'


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/border.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdQRCode(
                        value='https://fac.feffery.tech/', bordered=True
                    ),
                    fac.AntdText('bordered：True'),
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdQRCode(
                        value='https://fac.feffery.tech/', bordered=False
                    ),
                    fac.AntdText('bordered：False'),
                ]
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/custom_color.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdQRCode(value='https://fac.feffery.tech/', color='#52c41a'),
            fac.AntdQRCode(
                value='https://fac.feffery.tech/',
                color='#1677ff',
                bgColor='#f5f5f5',
            ),
        ]
    )

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/custom_render_type.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


@app.callback(
    Output('qrcode-custom-render-type-demo-output', 'children'),
    Input('qrcode-custom-render-type-demo-segmented', 'value'),
)
def qrcode_custom_render_type_demo_input_callback(input_value):
    return fac.AntdQRCode(type=input_value, value='https://fac.feffery.tech/')


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/custom_size.py`
```python
import feffery_antd_components as fac
import dash
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/download_qrcode.py`
```python
import feffery_antd_components as fac
import dash
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


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
    """
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
    """,
    Input('qrcode-download-button', 'nClicks'),
    State('qrcode', 'type'),
    prevent_initial_call=True,
)


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/error_level.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


@app.callback(
    Output('qrcode-error-level-demo-output', 'children'),
    Input('qrcode-error-level-demo-segmented', 'value'),
)
def qrcode_custom_render_type_demo_input_callback(input_value):
    return fac.AntdQRCode(
        errorLevel=input_value,
        value='https://gw.alipayobjects.com/zos/rmsportal/KDpgvguMpGfqaHPjicRK.svg',
    )


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/high_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPopover(
        fac.AntdButton('Hover me', type='primary'),
        content=fac.AntdQRCode(
            value='https://fac.feffery.tech/', bordered=False
        ),
        overlayInnerStyle={'padding': 0},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPopover(
    fac.AntdButton('Hover me', type='primary'),
    content=fac.AntdQRCode(
        value='https://fac.feffery.tech/', bordered=False
    ),
    overlayInnerStyle={'padding': 0},
)
"""
    }
]

```

### `views/AntdQRCode/demos/icon_size.py`
```python
import feffery_antd_components as fac
import dash
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdQRCode/demos/qrcode_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdQRCode(
        errorLevel='H',
        value='https://fac.feffery.tech/',
        icon='/assets/imgs/fac-logo.svg',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdQRCode(
    errorLevel='H',
    value='https://fac.feffery.tech/',
    icon='/assets/imgs/fac-logo.svg'
)
"""
    }
]

```

### `views/AntdQRCode/demos/qrcode_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdFlex(
        [
            fac.AntdQRCode(value='https://fac.feffery.tech/', status='active'),
            fac.AntdQRCode(value='https://fac.feffery.tech/', status='expired'),
            fac.AntdQRCode(value='https://fac.feffery.tech/', status='loading'),
            fac.AntdQRCode(value='https://fac.feffery.tech/', status='scanned'),
        ],
        gap='middle',
        wrap='wrap',
    )

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```
