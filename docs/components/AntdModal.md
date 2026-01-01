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

## 示例源码（demos）

### `views/AntdModal/demos/basic_callbacks.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdButton(
            '触发示例对话框', id='modal-basic-demo-open', type='primary'
        ),
        fac.AntdModal('示例内容', id='modal-basic-demo', title='对话框示例'),
    ]

    return demo_contents


@app.callback(
    Output('modal-basic-demo', 'visible'),
    Input('modal-basic-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_basic_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/centered.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('modal-centered-demo', 'visible'),
    Input('modal-centered-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_centered_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/confirm_loading.py`
```python
import time
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/custom_footer_button.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('modal-custom-button-demo', 'visible'),
    Input('modal-custom-button-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_custom_button_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/loading.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('modal-loading-demo', 'visible'),
    Input('modal-loading-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_loading_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/prevent_close.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/render_footer.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('modal-footer-demo', 'visible'),
    Input('modal-footer-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_footer_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/responsive_width.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


@app.callback(
    Output('modal-responsive-width-demo', 'visible'),
    Input('modal-responsive-width-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_responsive_width_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdModal/demos/width.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdButton(
            '触发示例对话框', id='modal-width-demo-open', type='primary'
        ),
        fac.AntdModal(
            '示例内容', id='modal-width-demo', title='对话框示例', width='75vw'
        ),
    ]

    return demo_contents


@app.callback(
    Output('modal-width-demo', 'visible'),
    Input('modal-width-demo-open', 'nClicks'),
    prevent_initial_call=True,
)
def modal_width_demo(nClicks):
    return True


code_string = [
    {
        'code': """
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
"""
    }
]

```
