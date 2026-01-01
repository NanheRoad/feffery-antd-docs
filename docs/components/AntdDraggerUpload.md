# AntdDraggerUpload

## 简介源码：`views/AntdDraggerUpload/intro.py`
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
                {'title': 'AntdDraggerUpload 拖拽上传'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDraggerUpload 拖拽上传', level=2),
        fac.AntdParagraph('构造可拖拽或点击触发文件上传的区域。'),
        # 上传接口示例小贴士
        tips.render(tip_type='upload api demo'),
    ]

```

## 示例源码（demos）

### `views/AntdDraggerUpload/demos/basic_callbacks.py`
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
                    id='dragger-upload-demo-is-multiple',
                    checked=False,
                    checkedChildren='True',
                    unCheckedChildren='False',
                ),
            ],
            style={'marginBottom': '5px', 'width': '100%'},
        ),
        fac.AntdDraggerUpload(
            id='dragger-upload-demo',
            apiUrl='/upload/',
            fileMaxSize=1,
            text='拖拽上传示例',
            hint='点击或拖拽文件至此处进行上传',
        ),
        fac.AntdSpin(html.Pre(id='dragger-upload-demo-output'), text='回调中'),
    ]

    return demo_contents


@app.callback(
    Output('dragger-upload-demo', 'multiple'),
    Input('dragger-upload-demo-is-multiple', 'checked'),
)
def dragger_upload_is_multiple(checked):
    return checked


@app.callback(
    Output('dragger-upload-demo-output', 'children'),
    [
        Input('dragger-upload-demo', 'lastUploadTaskRecord'),
        Input('dragger-upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def dragger_upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
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
                id='dragger-upload-demo-is-multiple',
                checked=False,
                checkedChildren='True',
                unCheckedChildren='False',
            ),
        ],
        style={'marginBottom': '5px', 'width': '100%'},
    ),
    fac.AntdDraggerUpload(
        id='dragger-upload-demo',
        apiUrl='/upload/',
        fileMaxSize=1,
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
    ),
    fac.AntdSpin(html.Pre(id='dragger-upload-demo-output'), text='回调中'),
]

...

@app.callback(
    Output('dragger-upload-demo', 'multiple'),
    Input('dragger-upload-demo-is-multiple', 'checked'),
)
def dragger_upload_is_multiple(checked):
    return checked


@app.callback(
    Output('dragger-upload-demo-output', 'children'),
    [
        Input('dragger-upload-demo', 'lastUploadTaskRecord'),
        Input('dragger-upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def dragger_upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
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

### `views/AntdDraggerUpload/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/confirm_before_delete.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
        defaultFileList=[
            {'name': f'demo{i}.txt', 'status': 'done'} for i in range(1, 6)
        ],
        confirmBeforeDelete=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
    defaultFileList=[
        {'name': f'demo{i}.txt', 'status': 'done'} for i in range(1, 6)
    ],
    confirmBeforeDelete=True,
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/directory_upload.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        directory=True,
        text='文件夹拖拽上传示例',
        hint='点击或拖拽文件夹至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    directory=True,
    text='文件夹拖拽上传示例',
    hint='点击或拖拽文件夹至此处进行上传',
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
        disabled=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
    disabled=True,
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/failed_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        failedTooltipInfo='啊哦，上传过程出了问题...',
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    failedTooltipInfo='啊哦，上传过程出了问题...',
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/file_types.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        fileTypes=['csv', 'txt'],
        text='请上传.csv或.txt文件',
        hint='点击或拖拽文件至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileTypes=['csv', 'txt'],
    text='请上传.csv或.txt文件',
    hint='点击或拖拽文件至此处进行上传',
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/list_max_length.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        fileListMaxLength=1,
        text='拖拽上传示例',
        hint='点击或拖拽文件至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileListMaxLength=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
"""
    }
]

```

### `views/AntdDraggerUpload/demos/multiple_upload.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDraggerUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        multiple=True,
        text='多文件拖拽上传示例',
        hint='点击或拖拽多个文件至此处进行上传',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    multiple=True,
    text='多文件拖拽上传示例',
    hint='点击或拖拽多个文件至此处进行上传',
)
"""
    }
]

```
