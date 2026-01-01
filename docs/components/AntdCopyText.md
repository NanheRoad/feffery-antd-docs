# AntdCopyText

## 简介源码：`views/AntdCopyText/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdCopyText 文本复制'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCopyText 文本复制', level=2),
        fac.AntdParagraph('用于帮助用户快速复制指定文本内容。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### _format

- 说明：演示 _format 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdCopyText(
                text='field1\tfield2\tfield3\nvalue1\tvalue2\tvalue3',
                beforeIcon=fac.AntdButton('点我复制'),
                afterIcon=fac.AntdButton('复制成功'),
            ),
            label='text/plain',
        ),
        fac.AntdFormItem(
            fac.AntdCopyText(
                text='<a href="http://fac.feffery.tech/" >demo link</ a>',
                beforeIcon=fac.AntdButton('点我复制'),
                afterIcon=fac.AntdButton('复制成功'),
                format='text/html',
            ),
            label='text/html',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInput(
            id='copy-text-input',
            maxLength=20,
            style={
                'width': '150px'
            }
        ),
        fac.AntdCopyText(
            id='copy-text-output',
            text='无内容'
        )
    ]
)

...

@app.callback(
    Output('copy-text-output', 'text'),
    Input('copy-text-input', 'value')
)
def copy_text_callback(value):
    return value or '无内容'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdCopyText(
    text='AntdCopyText复制示例'
)
```

### custom_addon

- 说明：演示 custom_addon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCopyText(
            text='AntdCopyText复制示例',
            beforeIcon='点我复制',
            afterIcon='复制成功',
        ),
        fac.AntdCopyText(
            text='AntdCopyText复制示例',
            beforeIcon=fac.AntdIcon(icon='antd-smile'),
            afterIcon=fac.AntdIcon(icon='antd-like'),
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
```

### tooltips

- 说明：演示 tooltips 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdCopyText(
                text='test',
                beforeIcon=fac.AntdButton('点我复制'),
                afterIcon=fac.AntdButton('复制成功'),
                tooltips=False,
            ),
            label='关闭提示',
        ),
        fac.AntdFormItem(
            fac.AntdCopyText(
                text='test',
                beforeIcon=fac.AntdButton('点我复制'),
                afterIcon=fac.AntdButton('复制成功'),
                tooltips=['请点击复制', '搞定！'],
            ),
            label='自定义提示',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
