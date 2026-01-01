# AntdTableBasic

## 简介源码：`views/AntdTableBasic/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('数据展示')},
                {'title': translator.t('AntdTable 表格')},
                {'title': translator.t('基础功能')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件主要基础功能示例。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：基础数据表格。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': 'int型示例', 'dataIndex': 'int型示例'},
        {'title': 'float型示例', 'dataIndex': 'float型示例'},
        {'title': 'str型示例', 'dataIndex': 'str型示例'},
        {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
    ],
    data=[
        {
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now(),
        }
    ]
    * 3,
)
```

### 添加边框线

- 说明：设置参数`bordered=True`为表格添加边框线。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    bordered=True,
)
```

### 字段内容对齐方式

- 说明：在参数`columns`中控制字段的`align`以控制字段内容对齐方式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': align, 'dataIndex': align, 'align': align}
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
```

### 字段标题对齐方式

- 说明：在参数`columns`中控制字段的`headerAlign`以控制字段标题对齐方式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': align,
            'dataIndex': align,
            'headerAlign': align,
        }
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
```

### css控制列宽

- 说明：基于**CSS**实现更为灵活的列宽控制。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': f'字段{i}',
            'dataIndex': f'字段{i}',
            'width': 'calc(100% / 5)',
        }
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
)
```

### 动态控制自定义行样式

- 说明：参数`rowClassName`支持基于动态`javascript`函数的行自定义css类控制。

#### 代码
```python
[
    fuc.FefferyStyle(
        rawStyle="""
.odd-row-class-name-demo {
    color: #f5222d;
}

.even-row-class-name-demo {
    color: #52c41a;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int型示例', 'dataIndex': 'int型示例'},
            {'title': 'float型示例', 'dataIndex': 'float型示例'},
            {'title': 'str型示例', 'dataIndex': 'str型示例'},
            {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
        ],
        data=[
            {
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now(),
            }
        ]
        * 4,
        rowClassName={
            'func': "(record, index) => index % 2 === 1 ? 'odd-row-class-name-demo' : 'even-row-class-name-demo'"
        },
    ),
]
```

### 可编辑单元格

- 说明：在参数`columns`中控制字段的`editable`以开启字段单元格可编辑功能。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': '请输入内容'},
        },
    ],
    data=[
        {
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
    ]
    * 3,
    bordered=True,
)
```

### 禁用部分单元格不可编辑

- 说明：为各数据记录行妥善设置唯一识别`key`后，可禁用部分单元格不可编辑。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {
                'placeholder': '请输入内容',
                'disabledKeys': ['row-2'],
            },
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
```

### 冻结部分列

- 说明：在参数`columns`中控制字段的`fixed`以实现冻结部分列的功能。

#### 代码
```python
[
    fac.AntdDivider('冻结在左侧', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': 'left' if i == 1 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('冻结在右侧', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': 'right' if i == 5 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('双侧同时冻结', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': (
                        'left' if i == 1 else ('right' if i == 5 else None)
                    ),
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
]
```

### 多层表头

- 说明：在参数`columns`中控制字段的`group`以渲染具有相应多层表头的表格。

#### 代码
```python
[
    fac.AntdDivider('单层分组', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': '字段1-1', 'dataIndex': '字段1-1', 'group': '字段1'},
            {'title': '字段1-2', 'dataIndex': '字段1-2', 'group': '字段1'},
            {'title': '字段2', 'dataIndex': '字段2'},
            {'title': '字段3-1', 'dataIndex': '字段3-1', 'group': '字段3'},
            {'title': '字段3-2', 'dataIndex': '字段3-2', 'group': '字段3'},
            {'title': '字段3-3', 'dataIndex': '字段3-3', 'group': '字段3'},
        ],
        data=[
            {
                '字段1-1': 1,
                '字段1-2': 1,
                '字段2': 1,
                '字段3-1': 1,
                '字段3-2': 1,
                '字段3-3': 1,
            }
        ]
        * 3,
        bordered=True,
    ),
    fac.AntdDivider('更多层分组', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {
                'title': '字段1-1-1',
                'dataIndex': '字段1-1-1',
                'group': ['字段1', '字段1-1'],
            },
            {
                'title': '字段1-1-2',
                'dataIndex': '字段1-1-2',
                'group': ['字段1', '字段1-1'],
            },
            {'title': '字段1-2', 'dataIndex': '字段1-2', 'group': '字段1'},
            {'title': '字段2', 'dataIndex': '字段2'},
        ],
        data=[{'字段1-1-1': 1, '字段1-1-2': 1, '字段1-2': 1, '字段2': 1}]
        * 3,
        bordered=True,
    ),
]
```

### 监听单元格编辑事件

- 说明：在回调函数中监听属性`recentlyChangedRow`、`recentlyChangedColumn`获知最近一次单元格编辑事件相关信息。

#### 代码
```python
[
    fac.AntdTable(
        id='table-editable-demo',
        columns=[
            {
                'title': 'int型示例',
                'dataIndex': 'int型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'float型示例',
                'dataIndex': 'float型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'str型示例',
                'dataIndex': 'str型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': '日期时间示例',
                'dataIndex': '日期时间示例',
                'editable': True,
                'width': '25%',
            },
        ],
        data=[
            {
                'key': f'row-{i}',
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now().strftime(
                    '%Y-%m-%d %H:%M:%S'
                ),
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-editable-demo-output'),
]

...

@app.callback(
    Output('table-editable-demo-output', 'children'),
    [
        Input('table-editable-demo', 'recentlyChangedRow'),
        Input('table-editable-demo', 'recentlyChangedColumn'),
    ],
    prevent_initial_call=True,
)
def table_editable_demo(recentlyChangedRow, recentlyChangedColumn):
    return json.dumps(
        dict(
            recentlyChangedRow=recentlyChangedRow,
            recentlyChangedColumn=recentlyChangedColumn,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### 自带的加载中效果

- 说明：通过参数`loading`控制是否开启表格自带的加载中效果。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSwitch(id='table-loading', checked=False),
        fac.AntdTable(
            id='table-loading-demo',
            columns=[
                {'title': 'int型示例', 'dataIndex': 'int型示例'},
                {'title': 'float型示例', 'dataIndex': 'float型示例'},
                {'title': 'str型示例', 'dataIndex': 'str型示例'},
                {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
            ],
            data=[
                {
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now(),
                }
            ]
            * 3,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('table-loading-demo', 'loading'),
    Input('table-loading', 'checked'),
    prevent_initial_call=True,
)
def table_loading(checked):
    return checked
```

### maxHeight的使用

- 说明：设置参数`maxHeight`后，当表格实际像素高度超出`maxHeight`所设定值时，会自动渲染垂直滚动条。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    maxHeight=150,
)
```

### maxWidth的使用

- 说明：设置参数`maxWidth`后，当表格实际像素宽度超出`maxWidth`所设定值时，会自动渲染水平滚动条。

#### 代码
```python
[
    html.Div(
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
            title='maxWidth=900',
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' * 4 for i in range(1, 6)}] * 3,
        maxWidth='max-content',
        title='maxWidth="max-content"',
    ),
]
```

### 嵌套可编辑单元格

- 说明：为各数据记录行妥善设置唯一识别`key`后，嵌套数据结构下同样支持字段单元格可编辑功能。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': '请输入内容'},
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
            'children': [
                {
                    'key': f'row-{i}-{j}',
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
                for j in range(1, 4)
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
```

### 数值型列宽

- 说明：默认情况下，为各字段设置数值型列宽后，会自动计算转换为比例，作为各个字段的百分比列宽。

#### 代码
```python
[
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
            for i, width in zip(range(1, 6), [50, 100, 50, 100, 50])
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    ),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
            for i, width in zip(
                range(1, 6), [5000, 10000, 5000, 10000, 5000]
            )
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    ),
]
```

### 百分比列宽

- 说明：使用百分比形式控制列宽。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
        for i, width in zip(
            range(1, 6), ['10%', '20%', '30%', '25%', '15%']
        )
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
)
```

### 自定义行样式

- 说明：通过参数`rowClassName`添加额外行样式。

#### 代码
```python
[
    fuc.FefferyStyle(
        rawStyle="""
.table-row-class-name-demo {
    color: #1890ff;
    font-weight: bold;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int型示例', 'dataIndex': 'int型示例'},
            {'title': 'float型示例', 'dataIndex': 'float型示例'},
            {'title': 'str型示例', 'dataIndex': 'str型示例'},
            {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
        ],
        data=[
            {
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now(),
            }
        ]
        * 3,
        rowClassName='table-row-class-name-demo',
    ),
]
```

### scrollToFirstRowOnChange的使用

- 说明：设置参数`scrollToFirstRowOnChange=False`后，翻页等操作后表格将不会自动滚回当页第一行。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='control-table-scroll-to-first-row-on-change-demo',
                checked=True,
            ),
            label='scrollToFirstRowOnChange',
        ),
        fac.AntdTable(
            id='table-scroll-to-first-row-on-change-demo',
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 50,
            maxHeight=150,
            scrollToFirstRowOnChange=False,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output(
        'table-scroll-to-first-row-on-change-demo', 'scrollToFirstRowOnChange'
    ),
    Input('control-table-scroll-to-first-row-on-change-demo', 'checked'),
)
def control_table_scroll_to_first_row_on_change(checked):
    return checked
```

### 表格尺寸规格

- 说明：设置参数`size`控制表格尺寸规格。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    f'size="{size}"', innerTextOrientation='left'
                ),
                fac.AntdTable(
                    columns=[
                        {'title': 'int型示例', 'dataIndex': 'int型示例'},
                        {
                            'title': 'float型示例',
                            'dataIndex': 'float型示例',
                        },
                        {'title': 'str型示例', 'dataIndex': 'str型示例'},
                        {
                            'title': '日期时间示例',
                            'dataIndex': '日期时间示例',
                        },
                    ],
                    data=[
                        {
                            'int型示例': 123,
                            'float型示例': 1.23,
                            'str型示例': '示例字符',
                            '日期时间示例': datetime.now(),
                        }
                    ],
                    size=size,
                    bordered=True,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```
