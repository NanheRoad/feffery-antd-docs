# AntdTableAdvanced

## 简介源码：`views/AntdTableAdvanced/intro.py`
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
                {'title': translator.t('进阶功能')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件主要进阶功能示例。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 编辑模式格式校验

- 说明：通过参数`columnsFormatConstraint`为对应字段配合单元格编辑模式下的内容校验正则表达式规则。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': '纯数字约束', 'dataIndex': '纯数字约束', 'editable': True, 'width': '25%'},
        {'title': '纯字母约束', 'dataIndex': '纯字母约束', 'editable': True, 'width': '25%'},
        {'title': '日期格式约束', 'dataIndex': '日期格式约束', 'editable': True, 'width': '25%'},
        {'title': '纯汉字约束', 'dataIndex': '纯汉字约束', 'editable': True, 'width': '25%'},
    ],
    data=[
        {'纯数字约束': '12345', '纯字母约束': 'fac', '日期格式约束': '2099-01-01', '纯汉字约束': '测试'}
    ],
    columnsFormatConstraint={
        '纯数字约束': {'rule': '^[0-9]+$', 'content': '不符合纯数字输入要求'},
        '纯字母约束': {'rule': '^[a-zA-Z]+$', 'content': '不符合纯字母输入要求'},
        '日期格式约束': {'rule': '^\\d{4}-\\d{2}-\\d{2}$', 'content': '不符合日期格式输入要求'},
        '纯汉字约束': {'rule': '^[一-龥]+$', 'content': '不符合纯汉字输入要求'},
    },
)
```

### 单元格条件样式

- 说明：通过参数`conditionalStyleFuncs`对指定字段进行单元格条件样式渲染规则控制。

#### 代码
```python
import numpy as np
fac.AntdTable(
    columns=[
        {"title": "示例字段1", "dataIndex": "示例字段1", "width": "100"},
        {"title": "示例字段2", "dataIndex": "示例字段2", "width": "100"},
        {"title": "示例字段3", "dataIndex": "示例字段3", "width": "100"},
    ],
    data=[
        {"示例字段1": i, "示例字段2": i, "示例字段3": round(np.random.rand(), 3)}
        for i in range(10)
    ],
    bordered=True,
    conditionalStyleFuncs={{
        "示例字段1": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { backgroundColor: "#ebfbee" } }
    }
}
""",
        "示例字段2": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { color: "red" } }
    }
}
""",
        "示例字段3": """
(record, index) => {
    if ( record['示例字段3'] <= 0.5 ) {
        return {
            style: {
                background: `linear-gradient(90deg, rgb(61, 153, 112) 0%, rgb(61, 153, 112) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
                backgroundClip: 'padding-box'
            }
        };
    }
    return {
        style: {
            background: `linear-gradient(90deg, rgb(255, 65, 54) 0%, rgb(255, 65, 54) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
            backgroundClip: 'padding-box'
        }
    };
}
""",
    }},
)
```

### 局部容器内悬浮层显示矫正

- 说明：与表格部分功能有关的悬浮层控件，譬如字段筛选对应的下拉菜单等，默认是以页面根节点为滚动事件参考容器，因此当表格置于局部容器内时，已展开的悬浮层控件会不跟随局部容器滑轮滚动事件移动，这种情况下可以设置参数`containerId='局部容器id'`来进行优化。

#### 代码
```python
[
    fac.AntdTitle('左例（未设置） 右例（设置containerId参数）', level=5),
    html.Div(
        [
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'字段{j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            '字段1': {'filterMode': 'keyword'},
                            '字段3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                },
            ),
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'字段{j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            '字段1': {'filterMode': 'keyword'},
                            '字段3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                        containerId='containerId-container-demo',
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                id='containerId-container-demo',
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                    'position': 'relative',
                },
            ),
        ],
        style={'display': 'flex'},
    ),
]
```

### 自定义空内容

- 说明：设置参数`emptyContent`自定义空数据提示内容。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    emptyContent=fac.AntdEmpty(
        image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
        description=fac.AntdText('没有数据哦~', type='secondary'),
        styles={'image': {'height': 150}},
    ),
)
```

### 基础使用

- 说明：通过参数`expandedRowKeyToContent`为指定行渲染行展开内容。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
)
```

### 点击整行触发展开

- 说明：设置参数`expandRowByClick=True`后，点击整行即可触发行展开。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    expandRowByClick=True,
)
```

### 初始化展开行

- 说明：通过参数`defaultExpandedRowKeys`控制初始化需要处于展开状态的行展开内容。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    defaultExpandedRowKeys=['row-2', 'row-6'],
)
```

### filter_callbacks

- 说明：演示 filter_callbacks 的用法。

#### 代码
```python
[
    fac.AntdTable(
        id='table-filter-demo',
        columns=[
            {'title': '基础示例', 'dataIndex': '基础示例', 'width': '20%'},
            {'title': '自定义选项', 'dataIndex': '自定义选项', 'width': '20%'},
            {'title': '单选模式', 'dataIndex': '单选模式', 'width': '20%'},
            {'title': '启用搜索框', 'dataIndex': '启用搜索框', 'width': '20%'},
            {'title': '搜索型筛选', 'dataIndex': '搜索型筛选', 'width': '20%'},
        ],
        data=[
            {
                '基础示例': s,
                '自定义选项': s,
                '单选模式': s,
                '启用搜索框': s,
                '搜索型筛选': s,
            }
            for s in list('abced')
        ],
        filterOptions={{
            '基础示例': {{}},
            '自定义选项': {{'filterCustomItems': list('abcdefghijk')}},
            '单选模式': {{'filterMultiple': False}},
            '启用搜索框': {{'filterSearch': True}},
            '搜索型筛选': {{'filterMode': 'keyword'}},
        }},
    ),
    html.Pre(id='table-filter-demo-output'),
]

# ...

@app.callback(
    Output('table-filter-demo-output', 'children'),
    Input('table-filter-demo', 'filter'),
    prevent_initial_call=True,
)
def table_filter_demo(filter_):
    return json.dumps(filter_, indent=4, ensure_ascii=False)
```

### 勾选模式

- 说明：通过勾选选项进行字段筛选。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': '基础示例', 'dataIndex': '基础示例', 'width': '20%'},
        {'title': '自定义选项', 'dataIndex': '自定义选项', 'width': '20%'},
        {'title': '单选模式', 'dataIndex': '单选模式', 'width': '20%'},
        {'title': '启用搜索框', 'dataIndex': '启用搜索框', 'width': '20%'},
        {'title': '树形筛选', 'dataIndex': '树形筛选', 'width': '20%'},
    ],
    data=[
        {
            '基础示例': s,
            '自定义选项': s,
            '单选模式': s,
            '启用搜索框': s,
            '树形筛选': s,
        }
        for s in list('abced')
    ],
    filterOptions={
        '基础示例': {},
        '自定义选项': {'filterCustomItems': list('abcdefghijk')},
        '单选模式': {'filterMultiple': False},
        '启用搜索框': {'filterSearch': True},
        '树形筛选': {
            'filterMode': 'tree',
            'filterCustomTreeItems': [
                {'text': 'a-c', 'children': [{'text': s, 'value': s} for s in list('abc')]},
                {'text': 'd', 'value': 'd'},
                {'text': 'e', 'value': 'e'},
            ],
        },
    },
)
```

### 默认选中项

- 说明：为字段筛选功能设置默认选中项。

#### 代码
```python
fac.AntdTable(
    columns=[{'title': '基础示例', 'dataIndex': '基础示例'}],
    data=[{'基础示例': s} for s in list('abced')],
    filterOptions={'基础示例': {}},
    defaultFilteredValues={'基础示例': ['a', 'c', 'e']},
    style={'width': 200},
)
```

### 搜索模式

- 说明：通过关键词搜索进行字段筛选。

#### 代码
```python
fac.AntdTable(
    columns=[{'title': '搜索型筛选', 'dataIndex': '搜索型筛选'}],
    data=[{'搜索型筛选': s} for s in list('abced')],
    filterOptions={'搜索型筛选': {'filterMode': 'keyword'}},
    style={'width': 200},
)
```

### 监听单元格点击事件

- 说明：通过参数`enableCellClickListenColumns`设置需要启用单元格点击事件监听的字段。

#### 代码
```python
[
    fac.AntdTable(
        id='table-click-event-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {
                'key': f'row-{row}',
                **{f'字段{i}': f'字段{i}第{row}行' for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableCellClickListenColumns=[f'字段{i}' for i in range(1, 6, 2)],
    ),
    html.Pre(id='table-click-event-demo-output'),
]

# ...

@app.callback(
    Output('table-click-event-demo-output', 'children'),
    [
        Input('table-click-event-demo', 'nClicksCell'),
        Input('table-click-event-demo', 'nDoubleClicksCell'),
    ],
    [
        State('table-click-event-demo', 'enableCellClickListenColumns'),
        State('table-click-event-demo', 'recentlyCellClickColumn'),
        State('table-click-event-demo', 'recentlyCellClickRecord'),
        State('table-click-event-demo', 'recentlyCellDoubleClickColumn'),
        State('table-click-event-demo', 'recentlyCellDoubleClickRecord'),
    ],
    prevent_initial_call=True,
)
def table_click_event_demo(
    nClicksCell,
    nDoubleClicksCell,
    enableCellClickListenColumns,
    recentlyCellClickColumn,
    recentlyCellClickRecord,
    recentlyCellDoubleClickColumn,
    recentlyCellDoubleClickRecord,
):
    return json.dumps(
        dict(
            enableCellClickListenColumns=enableCellClickListenColumns,
            nClicksCell=nClicksCell,
            recentlyCellClickColumn=recentlyCellClickColumn,
            recentlyCellClickRecord=recentlyCellClickRecord,
            nDoubleClicksCell=nDoubleClicksCell,
            recentlyCellDoubleClickColumn=recentlyCellDoubleClickColumn,
            recentlyCellDoubleClickRecord=recentlyCellDoubleClickRecord,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### 监听鼠标移入事件

- 说明：设置参数`enableHoverListen=True`后开启表格内部鼠标移入事件监听。

#### 代码
```python
[
    fac.AntdTable(
        id="table-hover-event-demo",
        columns=[
            {"title": f"字段{i}", "dataIndex": f"字段{i}", "width": "20%"}
            for i in range(1, 6)
        ],
        data=[
            {
                "key": f"row-{row}",
                **{f"字段{i}": f"字段{i}第{row}行" for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableHoverListen=True,
    ),
    html.Pre(id="table-hover-event-demo-output"),
]

# ...

app.clientside_callback(
    """( recentlyMouseEnterColumnDataIndex,
         recentlyMouseEnterRowKey,
         recentlyMouseEnterRow ) => {
        return JSON.stringify(
            {
                recentlyMouseEnterColumnDataIndex,
                recentlyMouseEnterRowKey,
                recentlyMouseEnterRow
            },
            null,
            4
        );
    }""",
    Output("table-hover-event-demo-output", "children"),
    [
        Input("table-hover-event-demo", "recentlyMouseEnterColumnDataIndex"),
        Input("table-hover-event-demo", "recentlyMouseEnterRowKey"),
        Input("table-hover-event-demo", "recentlyMouseEnterRow"),
    ],
    prevent_initial_call=True,
)
```

### 行数据嵌套

- 说明：在定义参数`data`时可通过键值对属性`children`向下嵌套展示行记录。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 'calc(100% / 3)'}
        for i in range(1, 4)
    ],
    data=[
        {
            'key': f'row-{i}',
            '字段1': '第一层',
            '字段2': '第一层',
            '字段3': '第一层',
            'children': [
                {
                    'key': f'row-{i}{j}',
                    '字段1': '第二层',
                    '字段2': '第二层',
                    '字段3': '第二层',
                }
                for j in range(3)
            ],
        }
        for i in range(3)
    ],
    bordered=True,
)
```

### 禁用状态

- 说明：以禁用状态显示分页控件。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination={'disabled': True, 'pageSize': 5},
)
```

### 关闭分页功能

- 说明：设置参数`pagination=False`关闭分页功能。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination=False,
)
```

### 单页自动隐藏控件

- 说明：单页数据时自动隐藏分页相关控件。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    pagination={'pageSize': 10, 'hideOnSinglePage': True},
)
```

### 每页记录数

- 说明：控制每页显示的最大记录数量。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 7},
)
```

### 允许用户调整每页记录数

- 说明：渲染控件供用户调整每页显示的最大记录数量。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination={
        'pageSize': 5,
        'showSizeChanger': True,
        'pageSizeOptions': [5, 10, 20],
    },
)
```

### 控件位置

- 说明：分页控件的不同显示位置。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(f'位置="{placement}"', innerTextOrientation='left'),
                fac.AntdTable(
                    columns=[
                        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}],
                    pagination={'position': placement},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for placement in [
            'topLeft', 'topCenter', 'topRight',
            'bottomLeft', 'bottomCenter', 'bottomRight'
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 显示较少的跳页按钮

- 说明：优先显示数量更少的跳页按钮。

#### 代码
```python
[
    fac.AntdDivider('showLessItems=False（默认）', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'current': 5},
    ),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'showLessItems': True, 'current': 5},
    ),
]
```

### 开启快捷跳页功能

- 说明：渲染控件供用户输入页码进行快捷跳页。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'showQuickJumper': True},
)
```

### 简洁模式

- 说明：渲染简洁风格的分页控件。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'simple': True},
)
```

### 回调监听

- 说明：在回调函数中监听行选择相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-row-selection-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
            for i in range(1, 4)
        ],
        data=[
            {
                **{f'字段{i}': '示例内容' for i in range(1, 4)},
                'key': f'row-{row+1}',
            }
            for row in range(3)
        ],
        rowSelectionType='checkbox',
    ),
    html.Pre(id='table-row-selection-demo-output'),
]

# ...

@app.callback(
    Output('table-row-selection-demo-output', 'children'),
    [
        Input('table-row-selection-demo', 'selectedRowKeys'),
        Input('table-row-selection-demo', 'selectedRows'),
    ],
    prevent_initial_call=True,
)
def table_row_selection_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
```

### 多选模式

- 说明：多选型行选择功能。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='checkbox',
)
```

### 单选模式

- 说明：单选型行选择功能。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='radio',
)
```

### 同步数据变化

- 说明：设置参数`selectedRowsSyncWithData=True`后，针对表格数据源的更新会根据当前的`selectedRowKeys`状态，对`selectedRows`信息进行同步刷新（使用此项功能时请确保原始输入数据源各行记录手动设置了键值对key）。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '刷新数据',
            id='table-row-selection-sync-selected-rows-demo-update-data',
            type='primary',
        ),
        fac.AntdTable(
            id='table-row-selection-sync-selected-rows-demo',
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 4)
            ],
            data=[
                {
                    **{f'字段{i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
                    'key': f'row-{row+1}',
                }
                for row in range(3)
            ],
            rowSelectionType='checkbox',
            selectedRowsSyncWithData=True,
        ),
        html.Pre(id='table-row-selection-sync-selected-rows-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

# ...

@app.callback(
    Output('table-row-selection-sync-selected-rows-demo', 'data'),
    Input('table-row-selection-sync-selected-rows-demo-update-data', 'nClicks'),
    prevent_initial_call=True,
)
def table_row_selection_sync_selected_rows_demo_update_data(nClicks):
    return [
        {
            **{f'字段{i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ]


@app.callback(
    Output('table-row-selection-sync-selected-rows-demo-output', 'children'),
    [
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRowKeys'),
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRows'),
    ],
)
def table_row_selection_sync_selected_rows_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
```

### 回调监听

- 说明：通过回调函数监听排序事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-sort-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
            for _ in range(10)
        ],
        bordered=True,
        sortOptions={
            'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
            'multiple': True,
        },
    ),
    html.Pre(id='table-sort-demo-output'),
]

# ...

@app.callback(
    Output('table-sort-demo-output', 'children'),
    Input('table-sort-demo', 'sorter'),
    prevent_initial_call=True,
)
def table_sort_demo(sorter):
    return json.dumps(sorter, indent=4, ensure_ascii=False)
```

### 多字段组合

- 说明：基于多个字段的固定顺序进行组合排序。

#### 代码
```python
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
        'multiple': True,
    },
)
```

### 多字段动态组合

- 说明：设置参数'multiple': 'auto'后，多字段组合排序的字段优先级顺序将动态遵循用户的排序点击顺序。

#### 代码
```python
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
        'multiple': 'auto',
    },
)
```

### 单字段

- 说明：基于单个字段进行排序。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': 'int型示例', 'dataIndex': 'int型示例', 'width': '25%'},
        {'title': 'float型示例', 'dataIndex': 'float型示例', 'width': '25%'},
        {'title': 'str型示例', 'dataIndex': 'str型示例', 'width': '25%'},
        {'title': '日期时间示例', 'dataIndex': '日期时间示例', 'width': '25%'},
    ],
    data=[
        {
            'int型示例': i,
            'float型示例': round(i * 0.1, 1),
            'str型示例': f'示例字符{i}',
            '日期时间示例': f'2099-01-0{i}',
        }
        for i in [4, 2, 1, 5, 3]
    ],
    sortOptions={
        'sortDataIndexes': ['int型示例', 'float型示例', 'str型示例', '日期时间示例'],
    },
)
```

### 额外信息提示

- 说明：通过参数`showSorterTooltip`、`showSorterTooltipTarget`控制可排序字段表头的额外信息提示。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='table-sort-tooltip-demo-show-sorter-tooltip',
                checked=True,
            ),
            label='showSorterTooltip',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='table-sort-tooltip-demo-show-sorter-tooltip-target',
                options=['full-header', 'sorter-icon'],
                value='full-header',
            ),
            label='showSorterTooltipTarget',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdTable(
            id='table-sort-tooltip-demo',
            columns=[
                {'title': 'int型示例', 'dataIndex': 'int型示例', 'width': '25%'},
                {'title': 'float型示例', 'dataIndex': 'float型示例', 'width': '25%'},
                {'title': 'str型示例', 'dataIndex': 'str型示例', 'width': '25%'},
                {'title': '日期时间示例', 'dataIndex': '日期时间示例', 'width': '25%'},
            ],
            data=[
                {
                    'int型示例': i,
                    'float型示例': round(i * 0.1, 1),
                    'str型示例': f'示例字符{i}',
                    '日期时间示例': f'2099-01-0{i}',
                }
                for i in [4, 2, 1, 5, 3]
            ],
            sortOptions={
                'sortDataIndexes': ['int型示例', 'float型示例', 'str型示例', '日期时间示例']
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

app.clientside_callback(
    """(showSorterTooltip, showSorterTooltipTarget) => [showSorterTooltip, showSorterTooltipTarget]""",
    [
        Output('table-sort-tooltip-demo', 'showSorterTooltip'),
        Output('table-sort-tooltip-demo', 'showSorterTooltipTarget'),
    ],
    [
        Input('table-sort-tooltip-demo-show-sorter-tooltip', 'checked'),
        Input('table-sort-tooltip-demo-show-sorter-tooltip-target', 'value'),
    ],
)
```

### 粘性表头

- 说明：设置参数`sticky=True`后，针对高度超过视口高度的表格，将在浏览表格时自动进行恰当的表头吸顶。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 4)
    ],
    data=[
        {f'字段{i}': '示例内容' for i in range(1, 4)} for row in range(30)
    ],
    sticky=True,
    size='large',
    pagination={'pageSize': 999},
    title='请点击本示例下方的“在新窗口打开”按钮，以查看无页首遮挡干扰的完整效果。',
)
```

### 基础使用

- 说明：在表格底部渲染总结栏。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
)
```

### 空列占位

- 说明：通过参数`summaryRowBlankColumns`为总结行设置前缀占位空列数量，适用于行选择功能开启等场景。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 固定在底部

- 说明：将总结栏固定在表格底部。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
    summaryRowFixed=True,
    maxHeight=150,
)
```

### 固定在顶部

- 说明：将总结栏固定在表格顶部。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
    summaryRowFixed='top',
    maxHeight=150,
)
```

### 多行

- 说明：配置多行总结栏。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
)
```

### 配合多层表头

- 说明：配合多层表头使用总结栏。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': '字段1', 'dataIndex': '字段1'},
        {'title': '字段2', 'dataIndex': '字段2'},
        {'title': '字段3', 'dataIndex': '字段3', 'group': '组1'},
        {'title': '字段4', 'dataIndex': '字段4', 'group': '组1'},
        {'title': '字段5', 'dataIndex': '字段5'},
        {'title': '字段6', 'dataIndex': '字段6'},
    ],
    data=[{f'字段{i}': f'示例内容{i}' for i in range(1, 7)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结', 'align': 'center'},
        {'content': '第2到3列总结', 'colSpan': 2, 'align': 'center'},
        {'content': '第4列总结', 'align': 'center'},
        {'content': '第5到6列总结', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
    ],
)
```

### 文本域编辑模式

- 说明：文本域编辑模式下，`enter`键的按下将不会退出当前输入框，而是会进行换行。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': '文本域编辑示例',
            'dataIndex': '文本域编辑示例',
            'editable': True,
            'editOptions': {
                'mode': 'text-area',  # 开启文本域编辑模式
                'autoSize': {'minRows': 1, 'maxRows': 3},
            },
        }
    ],
    data=[{'文本域编辑示例': '内容示例'}] * 3,
    bordered=True,
    style={'width': 200},
)
```

### 字段标题添加额外信息

- 说明：通过参数`titlePopoverInfo`为对应字段快捷添加额外说明信息。

#### 代码
```python
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    titlePopoverInfo={
        f'字段{i}': {
            'title': f'字段{i}说明',
            'content': f'这是字段{i}的说明巴拉巴拉巴拉',
            'placement': 'top',
        }
        for i in range(1, 6)
    },
)
```

## API 参数说明

- id (string; optional):
  Unique id of the component.

- key (string; optional):
  Update the `key` value of the current component to force re-rendering.

- className (string; optional):
  CSS class name of the component.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
  Language for component text. Options: `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German), `'ru-ru'` (Russian).
  Default: `'zh-cn'`.

- containerId (string; optional):
  When the table is rendered in a scrollable container, specify the container id to avoid abnormal behavior of expanded rows when scrolling.

- columns (list of dicts; optional):
  Configure column definitions.

  `columns` is a list of dicts with keys:

  - title (a list of or a singular dash component, string or number; required):
    Required. Current column title.

  - dataIndex (string; required):
    Required. Unique identifier of the column.

  - group (string | list of strings; optional):
    Group information of the column, used for rendering multi-level headers.

  - renderOptions (dict; optional):
    Configure [re-render mode](/AntdTable-rerender) parameters.

    `renderOptions` is a dict with keys:

    - renderType (a value equal to: 'link', 'ellipsis', 'copyable', 'ellipsis-copyable', 'tags', 'status-badge', 'image', 'custom-format', 'corner-mark', 'row-merge', 'dropdown', 'dropdown-links', 'image-avatar', 'mini-line', 'mini-bar', 'mini-progress', 'mini-ring-progress', 'mini-area', 'button', 'checkbox', 'switch', 'select'; optional):
      Re-render type. Options: `'link'`, `'ellipsis'`, `'copyable'`, `'ellipsis-copyable'`, `'tags'`, `'status-badge'`, `'image'`,
      `'custom-format'`, `'corner-mark'`, `'row-merge'`, `'dropdown'`, `'dropdown-links'`, `'image-avatar'`,
      `'mini-line'`, `'mini-bar'`, `'mini-progress'`, `'mini-ring-progress'`, `'mini-area'`,
      `'button'`, `'checkbox'`, `'switch'`, `'select'`.

    - renderLinkText (string; optional):
      When `renderType='link'`, set link text content.

    - renderButtonSplit (boolean; optional):
      When `renderType='button'`, whether to add dividers between multiple buttons.

    - renderButtonPopConfirmProps (dict; optional):
      When `renderType='button'`, configure confirmation popup parameters.

      `renderButtonPopConfirmProps` is a dict with keys:

      - title (string; optional):
        Confirmation popup title.

      - okText (string; optional):
        Confirmation button text.

      - cancelText (string; optional):
        Cancel button text.

    - miniChartColor (string; optional):
      For `renderType='mini-line'`, `'mini-area'`, `'mini-bar'`, set chart color.

    - tooltipCustomContent (string; optional):
      For `renderType='mini-line'`, `'mini-area'`, `'mini-bar'`, JavaScript function string for tooltip content.

    - progressOneHundredPercentColor (string; optional):
      For `renderType='mini-progress'`, `'mini-ring-progress'`, fill color when progress reaches 100%.

    - progressShowPercent (boolean; optional):
      For `renderType='mini-progress'`, whether to show percent text.
      Default: `False`.

    - progressPercentPrecision (number; optional):
      For `renderType='mini-progress'`, number of decimal places for percent text. Default keeps original precision.

    - progressPercentPosition (dict; optional):
      For `renderType='mini-progress'`, position of percent text.

      `progressPercentPosition` is a dict with keys:

      - align (a value equal to: 'start', 'center', 'end'; optional):
        Alignment. Options: `'start'`, `'center'`, `'end'`.

      - type (a value equal to: 'inner', 'outer'; optional):
        Position. Options: `'inner'`, `'outer'`.

    - progressStrokeLinecap (a value equal to: 'square', 'round'; optional):
      For `renderType='mini-progress'`, progress bar cap style. Options: `'square'`, `'round'`.
      Default: `'square'`.

    - progressSize (number; optional):
      For `renderType='mini-progress'`, set pixel size.

    - progressColor (dict; optional):
      For `renderType='mini-progress'`, progress bar color. Supports gradient with keys `'from'`, `'to'`.

      `progressColor` is a string

      Or dict with keys:

  - from (string; optional):
    Gradient start color.

  - to (string; optional):
    Gradient end color.

    - ringProgressFontSize (number; optional):
      For `renderType='mini-ring-progress'`, font size of percent text.

    - dropdownProps (dict; optional):
      For `renderType='dropdown'`, `'dropdown-links'`, configure dropdown menu parameters.

      `dropdownProps` is a dict with keys:

      - title (string; optional):
        Dropdown anchor title.

      - arrow (boolean; optional):
        Whether to show arrow. Default: `False`.

      - disabled (boolean; optional):
        Whether to disable dropdown globally. Lower priority than per-item settings.

      - overlayClassName (string; optional):
        CSS class name of dropdown container.

      - overlayStyle (dict; optional):
        CSS style of dropdown container.

      - placement (a value equal to: 'bottomLeft', 'bottomCenter', 'bottomRight', 'topLeft', 'topCenter', 'topRight'; optional):
        Dropdown placement. Options: `'bottomLeft'`, `'bottomCenter'`, `'bottomRight'`, `'topLeft'`, `'topCenter'`, `'topRight'`.

  - fixed (a value equal to: 'left', 'right' | boolean; optional):
    Column fixed direction. Options: `'left'`, `'right'`. `True` = `'left'`.

  - editable (boolean; optional):
    Whether the column is editable. Default: `False`.

  - editOptions (dict; optional):
    Configure editable input box parameters.

    `editOptions` is a dict with keys:

    - mode (a value equal to: 'default', 'text-area'; optional):
      Input mode. Options: `'default'`, `'text-area'`. Default: `'default'`.

    - autoSize (dict; optional):
      When `mode='textarea'`, configure auto resize. Same as `AntdInput`.
      Default: `False`.

      `autoSize` is a boolean

      Or dict with keys:

  - minRows (number; optional)

  - maxRows (number; optional)

    - maxLength (number; optional):
      Max characters in editable input. Default: unlimited.

    - placeholder (string; optional):
      Placeholder text when empty.

    - disabledKeys (list of strings; optional):
      List of row `key` values to disable input.

  - align (a value equal to: 'left', 'center', 'right'; optional):
    Column alignment. Options: `'left'`, `'center'`, `'right'`. Default: `'center'`.

  - headerAlign (a value equal to: 'left', 'center', 'right'; optional):
    Header alignment. Follows column alignment by default. Options: `'left'`, `'center'`, `'right'`.
    Default: `'center'`.

  - width (number | string; optional):
    Column width.

  - minWidth (number | string; optional):
    Minimum width. Only effective when `tableLayout="auto"`.

  - hidden (boolean; optional):
    Whether to hide the column. Default: `False`.

  - className (string; optional):
    Column CSS class name.

  - defaultSortOrder (a value equal to: 'ascend', 'descend'; optional):
    Default sort order when initializing. Options: `'ascend'`, `'descend'`.

  - filterResetToDefaultFilteredValue (boolean; optional):
    If default filter values are set via `defaultFilteredValues`, whether reset restores them.
    Default: `False`.

- showHeader (boolean; default True):
  Whether to display table header. Default: `True`.

- rowHoverable (boolean; default True):
  Whether rows have hover effect. Default: `True`.

- tableLayout (a value equal to: 'auto', 'fixed'; optional):
  When column widths are not set, control width allocation. Options: `'auto'`, `'fixed'`.

- data (list of dicts; optional):
  Define table data source, corresponding to `columns`.

  `data` is a list of dicts with strings as keys and values of type
  list of boolean | number | string | dict | lists | a list of or a
  singular dash component, string or number | string | number |
  boolean | dict with keys:

  - content (string; optional):
    For `'link'` mode, link text content. Overrides `renderLinkText` in column config.

  - href (string; optional):
    For `'link'` mode, link address.

  - target (string; optional):
    For `'link'` mode, link target. Default: `'_blank'`.

  - disabled (boolean; optional):
    For `'link'` mode, whether the link is disabled. Default: `False`.

    Or list of numbers | dict with keys:

  - color (string; optional):
    For `'tags'` mode, tag color.

  - tag (string | number; optional):
    For `'tags'` mode, tag content. | list of dicts with keys:

  - color (string; optional):
    For `'tags'` mode, tag color.

  - tag (string | number; optional):
    For `'tags'` mode, tag content. | dict with keys:

  - disabled (boolean; optional):
    For `'button'` mode, same as parameter in `AntdButton`.

  - type (a value equal to: 'primary', 'ghost', 'dashed', 'link', 'text', 'default'; optional):
    For `'button'` mode, same as parameter in `AntdButton`.

    - color (a value equal to: 'default', 'primary', 'danger', 'blue', 'purple', 'cyan', 'green', 'magenta', 'pink', 'red', 'orange', 'yellow', 'volcano', 'geekblue', 'lime', 'gold'; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - variant (a value equal to: 'outlined', 'dashed', 'solid', 'filled', 'text', 'link'; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - danger (boolean; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - style (dict; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - content (string; optional):
      For `'button'` mode, button text content.

    - href (string; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - target (string; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - popConfirmProps (dict; optional):
      For `'button'` mode, configure confirmation popup parameters for the button (higher priority).

      `popConfirmProps` is a dict with keys:

      - title (string; optional):
        Confirmation popup title.

      - okText (string; optional):
        Confirmation button text.

      - cancelText (string; optional):
        Cancel button text.

    - icon (string; optional):
      For `'button'` mode, button prefix icon type. If `iconRenderer='AntdIcon'`, same as `AntdIcon`; if `iconRenderer='fontawesome'`, CSS class name.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'button'` mode, rendering method for button prefix icon.

    - tooltip (dict; optional):
      For `'button'` mode, add tooltip.

      `tooltip` is a dict with keys:

      - title (string; optional):
        Tooltip text.

      - placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight'; optional):
        Tooltip placement. Default: `'top'`.

    - custom (boolean | number | string | dict | list; optional):
      For `'button'` mode, extra information.

    - status (a value equal to: 'success', 'processing', 'default', 'error', 'warning'; optional):
      For `'status-badge'` mode, badge status.

    - text (string | number; optional):
      For `'status-badge'` mode, badge text.

    - src (string; optional):
      For `'image'` mode, image URL.

    - height (string | number; optional):
      For `'image'` mode, image height.

    - preview (boolean; optional):
      For `'image'` mode, whether image is previewable. Default: `True`.

    - placement (a value equal to: 'top-left', 'top-right', 'bottom-left', 'bottom-right'; optional):
      For `'corner-mark'` mode, badge position.

    - color (string; optional):
      For `'corner-mark'` mode, badge color. Default: `'#1890ff'`.

    - content (number | string; optional):
      For `'corner-mark'` mode, cell value.

    - offsetX (number; optional):
      For `'corner-mark'` mode, horizontal offset.

    - offsetY (number; optional):
      For `'corner-mark'` mode, vertical offset.

    - hide (boolean; optional):
      For `'corner-mark'` mode, whether to hide. Default: `False`.

    - checked (boolean; optional):
      For `'checkbox'` mode, checked status.

    - disabled (boolean; optional):
      For `'checkbox'` mode, disabled state.

    - label (string; optional):
      For `'checkbox'` mode, label text.

    - custom (boolean | number | string | dict | list; optional):
      For `'checkbox'` mode, extra information.

    - checked (boolean; optional):
      For `'switch'` mode, switch state.

    - disabled (boolean; optional):
      For `'switch'` mode, disabled state.

    - checkedChildren (string; optional):
      For `'switch'` mode, text when on.

    - unCheckedChildren (string; optional):
      For `'switch'` mode, text when off.

    - custom (boolean | number | string | dict | list; optional):
      For `'switch'` mode, extra information.

    - content (number | string; optional):
      For `'row-merge'` mode, cell value.

    - rowSpan (number; optional):
      For `'row-merge'` mode, number of merged cells.

    - title (string; optional):
      For `'dropdown'` mode, dropdown item text.

    - disabled (boolean; optional):
      For `'dropdown'` mode, whether dropdown item is disabled.

    - icon (string; optional):
      For `'dropdown'` mode, button prefix icon type.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'dropdown'` mode, icon rendering method.

    - custom (boolean | number | string | dict | list; optional):
      For `'dropdown'` mode, extra information.

    - isDivider (boolean; optional):
      For `'dropdown'` mode, whether item is divider. Default: `False`.

    - title (string; optional):
      For `'dropdown-links'` mode, dropdown item text.

    - href (string; optional):
      For `'dropdown-links'` mode, link URL.

    - disabled (boolean; optional):
      For `'dropdown-links'` mode, disabled.

    - icon (string; optional):
      For `'dropdown-links'` mode, icon type.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'dropdown-links'` mode, icon rendering method.

    - isDivider (boolean; optional):
      For `'dropdown-links'` mode, whether divider. Default: `False`.

    - src (string; optional):
      For `'image-avatar'` mode, avatar image URL.

    - size (dict; optional):
      For `'image-avatar'` mode, avatar size. Number = px, string = preset size (`'small'`, `'default'`, `'large'`). Supports responsive. Default: `'default'`.

      `size` is a number | 'large' | 'small' | 'default' | dict with keys: xs, sm, md, lg, xl, xxl.

    - shape (a value equal to: 'circle', 'square'; optional):
      For `'image-avatar'` mode, avatar shape. Default: `'circle'`.

    - className (string; optional):
      For `'select'` mode, CSS class name.

    - style (dict; optional):
      For `'select'` mode, CSS style. Default width: `'100%'`.

    - options (list of dicts; optional):
      For `'select'` mode, dropdown options.

      `options` is a list of dicts with keys:

      - label (string; optional):
        Option text.

      - value (string | number; optional):
        Option value.

    - listHeight (number; optional):
      For `'select'` mode, dropdown menu height. Default: `256`.

    - mode (a value equal to: 'multiple', 'tags'; optional):
      For `'select'` mode, selection mode. Default: single.

    - disabled (boolean; optional):
      For `'select'` mode, disabled state.

    - size (a value equal to: 'small', 'middle', 'large'; optional):
      For `'select'` mode, size. Default: `'middle'`.

    - bordered (boolean; optional):
      For `'select'` mode, whether bordered. Default: `True`.

    - placeholder (string; optional):
      For `'select'` mode, placeholder text.

    - placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; optional):
      For `'select'` mode, dropdown placement. Default: `'bottomLeft'`.

    - value (string | number | list of string | numbers; optional):
      For `'select'` mode, selected value(s).

    - maxTagCount (number | 'responsive'; optional):
      For `'select'` mode, max number of tags shown. Default: `5`.

    - optionFilterProp (a value equal to: 'value', 'label'; optional):
      For `'select'` mode, search target field. Default: `'value'`.

    - allowClear (boolean; optional):
      For `'select'` mode, allow clearing. Default: `True`.

- bordered (boolean; default False):
  Whether to render table borders. Default: `False`.

- maxHeight (number | string; optional):
  Maximum table height in pixels. When actual height exceeds this, a vertical scrollbar is rendered.

- maxWidth (number | string | boolean; optional):
  Maximum table width. When actual width exceeds this, a horizontal scrollbar is rendered.

- scrollToFirstRowOnChange (boolean; default True):
  After pagination, sorting, or filtering triggers table change, whether to scroll to the top. Default: `True`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
  Table cell size. Options: `'small'`, `'middle'`, `'large'`.

- rowSelectionType (a value equal to: 'checkbox', 'radio'; optional):
  Row selection mode. Options: `'checkbox'` (multi-select), `'radio'` (single-select). Default: disabled.

- selectedRowKeys (list of string | numbers; optional):
  Track selected row `key` values.

- selectedRows (list; optional):
  Track selected row records.

- rowSelectionWidth (string | number; default 32):
  Width of row selection column. Default: `32`.

- rowSelectionCheckStrictly (boolean; optional):
  For nested rows, whether selection of parent and child rows are independent. Default: `True`.

- rowSelectionIgnoreRowKeys (list of string | numbers; optional):
  Specify row `key` values that cannot be selected.

- selectedRowsSyncWithData (boolean; default False):
  When data source `data` updates, whether to sync `selectedRows` based on current `selectedRowKeys`.
  Default: `False`.

- sticky (dict; default False):
  Configure sticky header. Default: `False`.

  `sticky` is a boolean | dict with keys:

  - offsetHeader (number; optional):
    Vertical offset for sticky header.

  - offsetScroll (number; optional):
    Vertical offset for bottom scrollbar in sticky header.

- enableHoverListen (boolean; default False):
  Enable row mouse enter/leave event listening. May affect other features. Default: `False`.

- recentlyMouseEnterColumnDataIndex (string; optional):
  When `enableHoverListen=True`, track `dataIndex` of most recently hovered column.

- recentlyMouseEnterRowKey (string | number; optional):
  When `enableHoverListen=True`, track `key` of most recently hovered row.

- recentlyMouseEnterRow (dict; optional):
  When `enableHoverListen=True`, track record of most recently hovered row.

- titlePopoverInfo (dict; optional):
  Configure extra popover info for column titles.

  `titlePopoverInfo` is a dict with strings as keys and values of type dict with keys:

  - title (string; optional):
    Popover title.

  - content (string; optional):
    Popover content.

  - placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight', 'leftTop', 'leftBottom', 'rightTop', 'rightBottom'; optional):
    Popover placement. Options: `'top'`, `'left'`, `'right'`, `'bottom'`, `'topLeft'`, `'topRight'`, `'bottomLeft'`, `'bottomRight'`, `'leftTop'`, `'leftBottom'`, `'rightTop'`, `'rightBottom'`.
    Default: `'bottom'`.

  - overlayStyle (dict; optional):
    CSS style for popover overlay.

- columnsFormatConstraint (dict; optional):
  For editable fields, configure regex-based input validation rules.

  `columnsFormatConstraint` is a dict with strings as keys and values of type dict with keys:

  - rule (string; optional):
    Regular expression to validate input format.

  - content (string; optional):
    Message shown when validation fails.

- sortOptions (dict; optional):
  Configure sorting features.

  `sortOptions` is a dict with keys:

  - sortDataIndexes (list of strings; optional):
    Columns (`dataIndex`) involved in sorting. Order of array defines priority (high to low).

  - multiple (boolean | 'auto'; optional):
    Enable multi-column sorting. `'auto'` = auto multi-sort based on click order.
    Default: `False`.

  - forceCompareModes (dict with strings as keys and values of type 'number' | 'custom'; optional):
    Force sorting mode per column. Options: `'number'` (numeric), `'custom'` (custom).

  - customOrders (dict with strings as keys and values of type list; optional):
    When `forceCompareModes='custom'`, define custom sort order for column values.

- showSorterTooltip (boolean; default True):
  For sortable columns, whether to show tooltip on hover. Default: `True`.

- showSorterTooltipTarget (a value equal to: 'full-header', 'sorter-icon'; default 'full-header'):
  Tooltip hover target. Options: `'full-header'`, `'sorter-icon'`.
  Default: `'full-header'`.

- filterOptions (dict; optional):
  Configure filtering features.

  `filterOptions` is a dict with strings as keys and values of type dict with keys:

  - filterMode (a value equal to: 'checkbox', 'keyword', 'tree'; optional):
    Filter mode. Options: `'checkbox'`, `'keyword'`, `'tree'`. `'tree'` mode requires `filterCustomTreeItems`.
    Default: `'checkbox'`.

  - filterCustomItems (list | boolean | number | string | dict | list; optional):
    For `'checkbox'` mode, define custom filter items.

  - filterCustomTreeItems (list of dicts; optional):
    For `'tree'` mode, define custom tree structure.

  - filterMultiple (boolean; optional):
    For `'checkbox'` mode, whether multi-select is enabled. Default: `True`.

  - filterSearch (boolean; optional):
    For `'checkbox'` mode, whether search box is enabled. Default: `False`.

- defaultFilteredValues (dict with strings as keys and values of type list; optional):
  Default filter values for fields.

- pagination (dict; optional):
  Configure pagination. Set `False` to disable.

  `pagination` is a dict with keys:

  - position (a value equal to: 'topLeft', 'topCenter', 'topRight', 'bottomLeft', 'bottomCenter', 'bottomRight'; optional):
    Pagination component placement. Default: `'bottomRight'`.

  - pageSize (number; optional):
    Track or set max rows per page.

  - current (number; optional):
    Track or set current page number.

  - showSizeChanger (boolean; optional):
    Show pageSize switcher. Default: `True` if total rows > 50.

  - pageSizeOptions (list of numbers; optional):
    Options for pageSize switcher.

  - showTitle (boolean; optional):
    Whether to show native browser tooltip on page number hover. Default: `True`.

  - showQuickJumper (boolean; optional):
    Whether to render quick jump control. Default: `False`.

  - showTotalPrefix (string; optional):
    Prefix text for total records description.

  - showTotalSuffix (string; optional):
    Suffix text for total records description.

  - hideOnSinglePage (boolean; optional):
    Hide pagination if rows < one page. Default: `False`.

  - simple (boolean; optional):
    Enable simple mode. Default: `False`.

  - disabled (boolean; optional):
    Disable pagination controls. Default: `False`.

  - size (a value equal to: 'default', 'small'; optional):
    Pagination control size. Default: `'default'`.

  - total (number; optional):
    Manually set total rows, usually with [server-side mode](/AntdTable-server-side-mode).

  - showLessItems (boolean; optional):
    Prefer fewer jump items. Default: `False`.

- currentData (list; optional):
  Track table data after edits.

- recentlyChangedRow (dict; optional):
  Track row most recently edited.

- recentlyChangedColumn (string; optional):
  Track `dataIndex` of most recently edited column.

- sorter (dict; optional):
  Track sort behavior.

  `sorter` is a dict with keys:

  - columns (list of strings; optional):
    Track sorted columns (`dataIndex`).

  - orders (list of a value equal to: 'ascend', 'descend'; optional):
    Track sort order. `'ascend'` = ascending, `'descend'` = descending.

- filter (dict; optional):
  Track filter behavior.

- mode (a value equal to: 'client-side', 'server-side'; default 'client-side'):
  Data load mode. Options: `'client-side'` (client), `'server-side'` (server). Server mode fits large datasets. Default: `'client-side'`.

- summaryRowContents (list of dicts; optional):
  Configure summary row contents.

  `summaryRowContents` is a list of dicts with keys:

  - content (a list of or a singular dash component, string or number; optional):
    Component, summary cell content.

  - colSpan (number; optional):
    Number of columns spanned by cell. Default: `1`.

  - align (a value equal to: 'left', 'center', 'right'; optional):
    Column alignment. Options: `'left'`, `'center'`, `'right'`.

- summaryRowBlankColumns (number; default 0):
  Number of blank columns per summary row. For use with row selection, etc. Default: `0`.

- summaryRowFixed (boolean | a value equal to: 'top', 'bottom'; default False):
  Whether to fix summary row. Options: `'top'`, `'bottom'`. Default: `False`.

- conditionalStyleFuncs (dict with strings as keys and values of type string; optional):
  Configure conditional formatting JavaScript functions per column.

- expandedRowKeyToContent (list of dicts; optional):
  Configure expanded row content. Key = row `key`, value = expanded content.

  `expandedRowKeyToContent` is a list of dicts with keys:

  - key (string | number; required)

  - content (a list of or a singular dash component, string or number; optional)

- expandedRowWidth (string | number; optional):
  Width of expanded row control column.

- expandRowByClick (boolean; default False):
  Allow expanding row by clicking directly. Default: `False`.

- defaultExpandedRowKeys (list of strings; optional):
  Keys of rows expanded by default.

- expandedRowKeys (list of strings; optional):
  Track or set expanded row keys.

- enableCellClickListenColumns (list of strings; optional):
  Enable cell click/double-click/right-click event listening. Default: `False`.

- recentlyCellClickColumn (string; optional):
  When enabled, track `dataIndex` of most recent cell click.

- recentlyCellClickRecord (dict; optional):
  When enabled, track record of most recent cell click.

- nClicksCell (number; default 0):
  When enabled, track cumulative number of cell clicks. Default: `0`.

- cellClickEvent (dict; optional):
  When enabled, track details of most recent cell click.

  `cellClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page top-left.

  - pageY (number; optional):
    Y coordinate relative to page top-left.

  - clientX (number; optional):
    X coordinate relative to browser window.

  - clientY (number; optional):
    Y coordinate relative to browser window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- recentlyCellDoubleClickColumn (string; optional):
  Track `dataIndex` of most recent cell double-click.

- recentlyCellDoubleClickRecord (dict; optional):
  Track record of most recent cell double-click.

- nDoubleClicksCell (number; default 0):
  Track cumulative cell double-clicks. Default: `0`.

- cellDoubleClickEvent (dict; optional):
  Track details of most recent cell double-click.

  `cellDoubleClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page.

  - pageY (number; optional):
    Y coordinate relative to page.

  - clientX (number; optional):
    X coordinate relative to window.

  - clientY (number; optional):
    Y coordinate relative to window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- recentlyContextMenuClickColumn (string; optional):
  Track `dataIndex` of most recent cell right-click.

- recentlyContextMenuClickRecord (dict; optional):
  Track record of most recent cell right-click.

- nContextMenuClicksCell (number; default 0):
  Track cumulative cell right-clicks. Default: `0`.

- cellContextMenuClickEvent (dict; optional):
  Track details of most recent cell right-click.

  `cellContextMenuClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page.

  - pageY (number; optional):
    Y coordinate relative to page.

  - clientX (number; optional):
    X coordinate relative to window.

  - clientY (number; optional):
    Y coordinate relative to window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- emptyContent (a list of or a singular dash component, string or number; optional):
  Component for custom empty-state content.

- cellUpdateOptimize (boolean; default False):
  Strictly optimize cell rendering based on data. Default: `False`.

- miniChartHeight (number; default 30):
  Set height for mini-chart cells. Default: `30`.

- miniChartAnimation (boolean; default False):
  Enable animation for mini-chart cells. Default: `False`.

- recentlyButtonClickedRow (dict; optional):
  For `'button'` mode, track row of most recent button click.

- nClicksButton (number; default 0):
  For `'button'` mode, track cumulative button clicks. Default: `0`.

- clickedContent (string; optional):
  For `'button'` mode, track text of most recent button click.

- clickedCustom (boolean | number | string | dict | list; optional):
  For `'button'` mode, track `custom` field of most recent button click.

- recentlyButtonClickedDataIndex (string; optional):
  For `'button'` mode, track `dataIndex` of most recent button click.

- customFormatFuncs (dict with strings as keys and values of type string; optional):
  For `'custom-format'` mode, key = `dataIndex`, value = JavaScript pre-processing function.

- recentlyCheckedRow (dict; optional):
  For `'checkbox'` mode, track row of most recent check.

- recentlyCheckedLabel (string; optional):
  For `'checkbox'` mode, track label of most recent check.

- recentlyCheckedDataIndex (string; optional):
  For `'checkbox'` mode, track `dataIndex` of most recent check.

- recentlyCheckedStatus (boolean; optional):
  For `'checkbox'` mode, track status of most recent check.

- recentlySwitchRow (dict; optional):
  For `'switch'` mode, track row of most recent toggle.

- recentlySwitchDataIndex (string; optional):
  For `'switch'` mode, track `dataIndex` of most recent toggle.

- recentlySwitchStatus (boolean; optional):
  For `'switch'` mode, track status of most recent toggle.

- nClicksDropdownItem (number; default 0):
  For `'dropdown'` mode, track cumulative dropdown item clicks.

- recentlyClickedDropdownItemTitle (string; optional):
  For `'dropdown'` mode, track `title` of most recent item clicked.

- recentlyDropdownItemClickedDataIndex (string; optional):
  For `'dropdown'` mode, track `dataIndex` of most recent item clicked.

- recentlyDropdownItemClickedRow (dict; optional):
  For `'dropdown'` mode, track row of most recent item clicked.

- recentlySelectRow (dict; optional):
  For `'select'` mode, track row of most recent value update.

- recentlySelectDataIndex (string; optional):
  For `'select'` mode, track `dataIndex` of most recent value update.

- recentlySelectValue (number | string | list of number | strings; optional):
  For `'select'` mode, track value(s) of most recent update.

- hiddenRowKeys (list of strings; optional):
  Row `key` values to hide. Default: `[]`.

- dataDeepCompare (boolean; optional):
  On re-render, whether to deep compare `data` for optimization. Default: `False`.

- virtual (boolean; default False):
  Enable virtual scrolling. Default: `False`.

- title (a list of or a singular dash component, string or number; optional):
  Component for table title.

- footer (a list of or a singular dash component, string or number; optional):
  Component for table footer.

- loading (boolean; default False):
  Whether to show loading state. Default: `False`.

- rowClassName (dict; optional):
  CSS class for rows. Supports defining JavaScript function via `func`.

  `rowClassName` is a string | dict with keys:

  - func (string; optional):
    JavaScript function string.

- data-_ (string; optional):
  Wildcard for `data-_` attributes.

- aria-\* (string; optional):
