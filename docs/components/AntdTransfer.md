# AntdTransfer

## 简介源码：`views/AntdTransfer/intro.py`
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
                {'title': 'AntdTransfer 穿梭框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTransfer 穿梭框', level=2),
        fac.AntdParagraph(
            '用于以直观的方式在两栏中移动选项，帮助用户完成选择行为。'
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
[
    fac.AntdTransfer(
        id='transfer-demo',
        dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
        targetKeys=[2, 3, 4],
    ),
    fac.AntdSpace(id='transfer-demo-output', direction='vertical'),
]

...

@app.callback(
    Output('transfer-demo-output', 'children'),
    [Input('transfer-demo', 'targetKeys'),
     Input('transfer-demo', 'moveDirection'),
     Input('transfer-demo', 'moveKeys')]
)
def transfer_demo(targetKeys, moveDirection, moveKeys):

    return [
        fac.AntdText(f'targetKeys: {targetKeys}'),
        fac.AntdText(f'moveDirection: {moveDirection}'),
        fac.AntdText(f'moveKeys: {moveKeys}')
    ]
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
)
```

### custom_height

- 说明：演示 custom_height 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    f'height="{height}"', innerTextOrientation='left'
                ),
                fac.AntdTransfer(
                    dataSource=[
                        {'key': i, 'title': f'选项{i}'}
                        for i in range(1, 10)
                    ],
                    targetKeys=[2, 3, 4],
                    height=height,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for height in ['300px', '10rem', '30vh']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### custom_move_button_content

- 说明：演示 custom_move_button_content 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    operations=['放入', '移出'],
)
```

### custom_titles

- 说明：演示 custom_titles 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    titles=['左侧区域', '右侧区域'],
)
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    disabled=True,
)
```

### multiple_mode_search

- 说明：演示 multiple_mode_search 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='transfer-multiple-mode-search-demo-switch-mode',
            options=[
                {'label': mode, 'value': mode}
                for mode in ['case-insensitive', 'case-sensitive', 'regex']
            ],
            defaultValue='case-insensitive',
            optionType='button',
        ),
        fac.AntdTransfer(
            id='transfer-multiple-mode-search-demo',
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in list('AbCdEf')
            ],
            targetKeys=[],
            showSearch=True,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('transfer-multiple-mode-search-demo', 'optionFilterMode'),
    Input('transfer-multiple-mode-search-demo-switch-mode', 'value'),
)
def transfer_multiple_mode_search_demo(value):
    return value
```

### pagination

- 说明：演示 pagination 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 50)],
    targetKeys=[2, 3, 4],
    pagination={'pageSize': 5},
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    readOnly=True,
)
```

### search

- 说明：演示 search 的用法。

#### 代码
```python
fac.AntdTransfer(
    dataSource=[{'key': i, 'title': f'选项{i}'} for i in range(1, 10)],
    targetKeys=[2, 3, 4],
    showSearch=True,
)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTransfer(
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
            ],
            targetKeys=[2, 3, 4],
            status='warning',
        ),
        fac.AntdTransfer(
            dataSource=[
                {'key': i, 'title': f'选项{i}'} for i in range(1, 10)
            ],
            targetKeys=[2, 3, 4],
            status='error',
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
