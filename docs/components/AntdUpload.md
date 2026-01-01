# AntdUpload

## 简介源码：`views/AntdUpload/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from components import tips


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': '文件上传'},
                {'title': 'AntdUpload 上传'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdUpload 上传', level=2),
        fac.AntdParagraph('提供点击按钮触发的通用文件上传功能。'),
        # 上传接口示例小贴士
        tips.render(tip_type='upload api demo'),
    ]

```

## 示例源码（demos）

### `views/AntdUpload/demos/basic_callbacks.py`
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
        fac.AntdSpace(
            [
                'multiple:',
                fac.AntdSwitch(
                    id='upload-demo-is-multiple',
                    checked=False,
                    checkedChildren='True',
                    unCheckedChildren='False',
                ),
            ],
            style={'marginBottom': '5px', 'width': '100%'},
        ),
        fac.AntdUpload(id='upload-demo', apiUrl='/upload/', fileMaxSize=1),
        fac.AntdSpin(html.Pre(id='upload-demo-output'), text='回调中'),
    ]

    return demo_contents


@app.callback(
    Output('upload-demo', 'multiple'),
    Input('upload-demo-is-multiple', 'checked'),
)
def upload_is_multiple(checked):
    return checked


@app.callback(
    Output('upload-demo-output', 'children'),
    [
        Input('upload-demo', 'lastUploadTaskRecord'),
        Input('upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
    if lastUploadTaskRecord:
        return json.dumps(
            {
                'lastUploadTaskRecord': lastUploadTaskRecord,
                'listUploadTaskRecord': listUploadTaskRecord,
            },
            indent=4,
            ensure_ascii=False,
        )


code_string = [
    {
        'code': """
[
    fac.AntdSpace(
        [
            'multiple:',
            fac.AntdSwitch(
                id='upload-demo-is-multiple',
                checked=False,
                checkedChildren='True',
                unCheckedChildren='False',
            ),
        ],
        style={'marginBottom': '5px', 'width': '100%'},
    ),
    fac.AntdUpload(id='upload-demo', apiUrl='/upload/', fileMaxSize=1),
    fac.AntdSpin(html.Pre(id='upload-demo-output'), text='回调中'),
]

...

@app.callback(
    Output('upload-demo', 'multiple'),
    Input('upload-demo-is-multiple', 'checked'),
)
def upload_is_multiple(checked):
    return checked


@app.callback(
    Output('upload-demo-output', 'children'),
    [
        Input('upload-demo', 'lastUploadTaskRecord'),
        Input('upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
    if lastUploadTaskRecord:
        return json.dumps(
            {
                'lastUploadTaskRecord': lastUploadTaskRecord,
                'listUploadTaskRecord': listUploadTaskRecord,
            },
            indent=4,
            ensure_ascii=False,
        )
"""
    }
]

```

### `views/AntdUpload/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(apiUrl='/upload/', fileMaxSize=1)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(apiUrl='/upload/', fileMaxSize=1)
"""
    }
]

```

### `views/AntdUpload/demos/block_button.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/', fileMaxSize=1, buttonProps={'block': True}
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, buttonProps={'block': True}
)
"""
    }
]

```

### `views/AntdUpload/demos/confirm_before_delete.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        defaultFileList=[
            {'name': f'demo{i}.txt', 'status': 'done'} for i in range(1, 6)
        ],
        confirmBeforeDelete=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    defaultFileList=[
        {'name': f'demo{i}.txt', 'status': 'done'} for i in range(1, 6)
    ],
    confirmBeforeDelete=True,
)
"""
    }
]

```

### `views/AntdUpload/demos/directory_upload.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        directory=True,
        buttonContent='点击选择文件夹进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    directory=True,
    buttonContent='点击选择文件夹进行上传',
)
"""
    }
]

```

### `views/AntdUpload/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/', fileMaxSize=1, disabled=True
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, disabled=True
)
"""
    }
]

```

### `views/AntdUpload/demos/failed_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        failedTooltipInfo='啊哦，上传过程出了问题...',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    failedTooltipInfo='啊哦，上传过程出了问题...',
)
"""
    }
]

```

### `views/AntdUpload/demos/file_types.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        fileTypes=['csv', 'txt'],
        buttonContent='请上传csv或txt文件',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileTypes=['csv', 'txt'],
    buttonContent='请上传csv或txt文件',
)
"""
    }
]

```

### `views/AntdUpload/demos/list_max_length.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/', fileMaxSize=1, fileListMaxLength=1
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, fileListMaxLength=1
)
"""
    }
]

```

### `views/AntdUpload/demos/multiple_upload.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        multiple=True,
        buttonContent='点击上传多个文件',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    multiple=True,
    buttonContent='点击上传多个文件',
)
"""
    }
]

```
