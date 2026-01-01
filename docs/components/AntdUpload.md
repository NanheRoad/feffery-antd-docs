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
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdUpload(apiUrl='/upload/', fileMaxSize=1)
```

### block_button

- 说明：演示 block_button 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, buttonProps={'block': True}
)
```

### confirm_before_delete

- 说明：演示 confirm_before_delete 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
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
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    directory=True,
    buttonContent='点击选择文件夹进行上传',
)
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, disabled=True
)
```

### failed_tooltip

- 说明：演示 failed_tooltip 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    failedTooltipInfo='啊哦，上传过程出了问题...',
)
```

### file_types

- 说明：演示 file_types 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    fileTypes=['csv', 'txt'],
    buttonContent='请上传csv或txt文件',
)
```

### list_max_length

- 说明：演示 list_max_length 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/', fileMaxSize=1, fileListMaxLength=1
)
```

### multiple_upload

- 说明：演示 multiple_upload 的用法。

#### 代码
```python
fac.AntdUpload(
    apiUrl='/upload/',
    fileMaxSize=1,
    multiple=True,
    buttonContent='点击上传多个文件',
)
```
