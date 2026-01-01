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

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
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
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
```

### confirm_before_delete

- 说明：演示 confirm_before_delete 的用法。

#### 代码
```python
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
```

### directory_upload

- 说明：演示 directory_upload 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    directory=True,
    text='文件夹拖拽上传示例',
    hint='点击或拖拽文件夹至此处进行上传',
)
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
    disabled=True,
)
```

### failed_tooltip

- 说明：演示 failed_tooltip 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    failedTooltipInfo='啊哦，上传过程出了问题...',
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
```

### file_types

- 说明：演示 file_types 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileTypes=['csv', 'txt'],
    text='请上传.csv或.txt文件',
    hint='点击或拖拽文件至此处进行上传',
)
```

### list_max_length

- 说明：演示 list_max_length 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileListMaxLength=1,
    text='拖拽上传示例',
    hint='点击或拖拽文件至此处进行上传',
)
```

### multiple_upload

- 说明：演示 multiple_upload 的用法。

#### 代码
```python
fac.AntdDraggerUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    multiple=True,
    text='多文件拖拽上传示例',
    hint='点击或拖拽多个文件至此处进行上传',
)
```
