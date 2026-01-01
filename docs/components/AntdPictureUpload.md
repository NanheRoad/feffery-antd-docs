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

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
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
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdPictureUpload(
    apiUrl='/upload/', fileMaxSize=1, buttonContent='点击上传图片'
)
```

### confirm_before_delete

- 说明：演示 confirm_before_delete 的用法。

#### 代码
```python
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
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdPictureUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    buttonContent='点击上传图片',
    disabled=True,
)
```

### editable

- 说明：演示 editable 的用法。

#### 代码
```python
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
```

### icons_visible

- 说明：演示 icons_visible 的用法。

#### 代码
```python
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
```
