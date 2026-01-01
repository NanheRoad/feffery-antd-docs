# AntdPictureUpload

## 简介源码：`views/AntdPictureUpload/intro.py`
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
                {'title': 'AntdPictureUpload 图片上传'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdPictureUpload 图片上传', level=2),
        fac.AntdParagraph('专门的图片上传功能。'),
        # 上传接口示例小贴士
        tips.render(tip_type='upload api demo'),
    ]

```

## 示例源码（demos）

### `views/AntdPictureUpload/demos/basic_callbacks.py`
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
        fac.AntdPictureUpload(
            id='picture-upload-demo',
            apiUrl='/upload/',
            fileMaxSize=1,
            buttonContent='点击上传图片',
        ),
        fac.AntdSpin(html.Pre(id='picture-upload-demo-output'), text='回调中'),
    ]

    return demo_contents


@app.callback(
    Output('picture-upload-demo-output', 'children'),
    [
        Input('picture-upload-demo', 'lastUploadTaskRecord'),
        Input('picture-upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def picture_upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
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
    fac.AntdPictureUpload(
        id='picture-upload-demo',
        apiUrl='/upload/',
        fileMaxSize=1,
        buttonContent='点击上传图片',
    ),
    fac.AntdSpin(html.Pre(id='picture-upload-demo-output'), text='回调中'),
]

...

@app.callback(
    Output('picture-upload-demo-output', 'children'),
    [
        Input('picture-upload-demo', 'lastUploadTaskRecord'),
        Input('picture-upload-demo', 'listUploadTaskRecord'),
    ],
    prevent_initial_call=True,
)
def picture_upload_callback_demo(lastUploadTaskRecord, listUploadTaskRecord):
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

### `views/AntdPictureUpload/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPictureUpload(
        apiUrl='/upload/', fileMaxSize=1, buttonContent='点击上传图片'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPictureUpload(
    apiUrl='/upload/', fileMaxSize=1, buttonContent='点击上传图片'
)
"""
    }
]

```

### `views/AntdPictureUpload/demos/confirm_before_delete.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPictureUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        buttonContent='点击上传图片',
        defaultFileList=[
            {
                'name': 'feffery-添加好友二维码.jpg',
                'status': 'done',
                'url': '/assets/imgs/index/feffery-添加好友二维码.jpg',
            }
            for i in range(1, 6)
        ],
        confirmBeforeDelete=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPictureUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    buttonContent='点击上传图片',
    defaultFileList=[
        {
            'name': 'feffery-添加好友二维码.jpg',
            'status': 'done',
            'url': '/assets/imgs/index/feffery-添加好友二维码.jpg',
        }
        for i in range(1, 6)
    ],
    confirmBeforeDelete=True,
)
"""
    }
]

```

### `views/AntdPictureUpload/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPictureUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        buttonContent='点击上传图片',
        disabled=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPictureUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    buttonContent='点击上传图片',
    disabled=True,
)
"""
    }
]

```

### `views/AntdPictureUpload/demos/editable.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdPictureUpload(
        apiUrl='/upload/',
        fileMaxSize=1,
        buttonContent='点击上传图片',
        editable=True,
        editConfig={
            'grid': True,
            'rotate': True,
            'modalTitle': '图片编辑窗口标题示例',
            'modalWidth': 600,
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdPictureUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    buttonContent='点击上传图片',
    editable=True,
    editConfig={
        'grid': True,
        'rotate': True,
        'modalTitle': '图片编辑窗口标题示例',
        'modalWidth': 600,
    },
)
"""
    }
]

```

### `views/AntdPictureUpload/demos/icons_visible.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdSwitch(id='show-remove-icon', checked=True),
                    label='showRemoveIcon',
                ),
                fac.AntdFormItem(
                    fac.AntdSwitch(id='show-preview-icon', checked=True),
                    label='showPreviewIcon',
                ),
            ]
        ),
        fac.AntdPictureUpload(
            id='picture-upload-icon-hide-demo',
            apiUrl='/upload/',
            fileMaxSize=1,
            buttonContent='点击上传图片',
            defaultFileList=[
                {
                    'name': 'feffery-添加好友二维码.jpg',
                    'status': 'done',
                    'url': '/assets/imgs/index/feffery-添加好友二维码.jpg',
                }
                for i in range(1, 6)
            ],
        ),
    ]

    return demo_contents


@app.callback(
    [
        Output('picture-upload-icon-hide-demo', 'showRemoveIcon'),
        Output('picture-upload-icon-hide-demo', 'showPreviewIcon'),
    ],
    [
        Input('show-remove-icon', 'checked'),
        Input('show-preview-icon', 'checked'),
    ],
)
def picture_upload_icon_hide_demo(showRemoveIcon, showPreviewIcon):
    return showRemoveIcon, showPreviewIcon


code_string = [
    {
        'code': """
[
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdSwitch(id='show-remove-icon', checked=True),
                label='showRemoveIcon',
            ),
            fac.AntdFormItem(
                fac.AntdSwitch(id='show-preview-icon', checked=True),
                label='showPreviewIcon',
            ),
        ]
    ),
    fac.AntdPictureUpload(
        id='picture-upload-icon-hide-demo',
        apiUrl='/upload/',
        fileMaxSize=1,
        buttonContent='点击上传图片',
        defaultFileList=[
            {
                'name': 'feffery-添加好友二维码.jpg',
                'status': 'done',
                'url': '/assets/imgs/index/feffery-添加好友二维码.jpg',
            }
            for i in range(1, 6)
        ],
    ),
]

...

@app.callback(
    [
        Output('picture-upload-icon-hide-demo', 'showRemoveIcon'),
        Output('picture-upload-icon-hide-demo', 'showPreviewIcon'),
    ],
    [
        Input('show-remove-icon', 'checked'),
        Input('show-preview-icon', 'checked'),
    ],
)
def picture_upload_icon_hide_demo(showRemoveIcon, showPreviewIcon):
    return showRemoveIcon, showPreviewIcon
"""
    }
]

```
