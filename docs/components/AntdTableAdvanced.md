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
