# AntdTreeSelect

## 简介源码：`views/AntdTreeSelect/intro.py`
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
                {'title': 'AntdTreeSelect 树选择'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTreeSelect 树选择', level=2),
        fac.AntdParagraph('提供在树形结构中选择若干项的功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### async_load_node

- 说明：演示 async_load_node 的用法。

#### 代码
```python
from feffery_dash_utils.tree_utils import TreeManager

...

fac.AntdTreeSelect(
    id='tree-select-async-demo',
    treeData=[
        {
            'key': '节点1',
            'title': '节点1',
            'value': '节点1',
        },
        {
            'key': '节点2',
            'title': '节点2',
            'value': '节点2',
        },
        {
            'key': '节点3',
            'title': '节点3',
            'value': '节点3',
            'isLeaf': True,
        },
    ],
    enableAsyncLoad=True,
    style={'width': 300},
)

...

@app.callback(
    Output('tree-select-async-demo', 'treeData'),
    Input('tree-select-async-demo', 'loadingNode'),
    State('tree-select-async-demo', 'treeData'),
    prevent_initial_call=True,
)
def tree_select_async_demo(loadingNode, treeData):
    time.sleep(0.5)
    return TreeManager.update_tree_node(
        treeData,
        node_key=loadingNode['key'],
        new_node={
            'children': [
                {
                    'key': loadingNode['key'] + '-1',
                    'title': loadingNode['key'] + '-1',
                    'value': loadingNode['key'] + '-1',
                }
            ]
        },
        mode='overlay',
    )
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
[
    fac.AntdDivider('单选示例', innerTextOrientation='left'),
    fac.AntdTreeSelect(
        id='tree-select-demo',
        treeData=[
            {
                'key': '节点1',
                'value': '1',
                'title': '节点1',
                'children': [
                    {
                        'key': f'节点1-{i}',
                        'value': f'1-{i}',
                        'title': f'节点1-{i}',
                    }
                    for i in range(1, 5)
                ],
            },
            {'key': '节点2', 'value': '2', 'title': '节点2'},
        ],
        placeholder='请选择',
        style={'width': 256},
    ),
    fac.AntdSpace(
        id='tree-select-demo-output',
        direction='vertical',
        style={'width': '100%'},
    ),
    fac.AntdDivider('多选示例', innerTextOrientation='left'),
    fac.AntdTreeSelect(
        id='tree-select-multiple-demo',
        treeData=[
            {
                'key': '节点1',
                'value': '1',
                'title': '节点1',
                'children': [
                    {
                        'key': f'节点1-{i}',
                        'value': f'1-{i}',
                        'title': f'节点1-{i}',
                    }
                    for i in range(1, 5)
                ],
            },
            {'key': '节点2', 'value': '2', 'title': '节点2'},
        ],
        placeholder='请选择',
        multiple=True,
        treeCheckable=True,
        style={'width': 256},
    ),
    fac.AntdSpace(
        id='tree-select-multiple-demo-output',
        direction='vertical',
        style={'width': '100%'},
    ),
]

...

@app.callback(
    Output('tree-select-multiple-demo-output', 'children'),
    [
        Input('tree-select-multiple-demo', 'value'),
        Input('tree-select-multiple-demo', 'treeExpandedKeys'),
    ],
)
def tree_select_multiple_demo(value, treeExpandedKeys):
    return [
        fac.AntdText(f'value: {value}'),
        fac.AntdText(f'treeExpandedKeys: {treeExpandedKeys}'),
    ]
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    style={'width': 256},
)
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTreeSelect(
            treeData=[
                {
                    'key': '节点1',
                    'value': '1',
                    'title': '节点1',
                    'children': [
                        {
                            'key': f'节点1-{i}',
                            'value': f'1-{i}',
                            'title': f'节点1-{i}',
                        }
                        for i in range(1, 5)
                    ],
                },
                {'key': '节点2', 'value': '2', 'title': '节点2'},
            ],
            placeholder=f'placement="{placement}"',
            placement=placement,
            style={'width': 256},
        )
        for placement in [
            'bottomLeft',
            'bottomRight',
            'topLeft',
            'topRight',
        ]
    ],
    direction='vertical',
)
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    disabled=True,
    style={'width': 256},
)
```

### flat_tree_data

- 说明：演示 flat_tree_data 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeDataMode='flat',
    treeData=[
        {'key': '节点1', 'value': '1', 'title': '节点1'},
        *[
            {
                'key': f'节点1-{i}',
                'value': f'1-{i}',
                'title': f'节点1-{i}',
                'parent': '节点1',
            }
            for i in range(1, 6)
        ],
    ],
    placeholder='请选择',
    style={'width': 256},
)
```

### maxCount

- 说明：演示 maxCount 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    id='test-max-count-demo',
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 11)
            ],
        }
    ],
    placeholder='请选择',
    multiple=True,
    treeCheckable=True,
    showCheckedStrategy='show-child',
    maxCount=3,
    style={'width': 256},
)
```

### max_tag_placeholder

- 说明：演示 max_tag_placeholder 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    maxTagCount=2,
    maxTagPlaceholder=fac.AntdIcon(icon='antd-ellipsis'),
    multiple=True,
    style={'width': 256},
)
```

### max_tag_text_length

- 说明：演示 max_tag_text_length 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    maxTagCount=2,
    maxTagTextLength=4,
    multiple=True,
    style={'width': 256},
)
```

### multiple

- 说明：演示 multiple 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    multiple=True,
    style={'width': 256},
)
```

### multiple_checkable

- 说明：演示 multiple_checkable 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    multiple=True,
    treeCheckable=True,
    style={'width': 256},
)
```

### multiple_mode_search

- 说明：演示 multiple_mode_search 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdRadioGroup(
            id='tree-select-multiple-mode-search-demo-switch-mode',
            options=[
                {'label': mode, 'value': mode}
                for mode in ['case-insensitive', 'case-sensitive', 'regex']
            ],
            defaultValue='case-insensitive',
            optionType='button',
        ),
        fac.AntdTreeSelect(
            id='tree-select-multiple-mode-search-demo',
            treeData=[
                {
                    'key': f'节点{i}',
                    'title': f'节点{i}',
                    'value': f'节点{i}',
                    'children': [
                        {
                            'key': f'节点{i}-{j}',
                            'title': f'节点{i}-{j}',
                            'value': f'节点{i}-{j}',
                        }
                        for j in range(1, 4)
                    ],
                }
                for i in list('AbCdEf')
            ],
            style={'width': 300},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('tree-select-multiple-mode-search-demo', 'treeNodeFilterMode'),
    Input('tree-select-multiple-mode-search-demo-switch-mode', 'value'),
)
def tree_select_multiple_mode_search_demo(value):
    return value
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    prefix=fac.AntdIcon(icon='antd-user'),
    style={'width': 256},
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    defaultValue='节点2',
    readOnly=True,
    style={'width': 256},
)
```

### show_checked_strategy

- 说明：演示 show_checked_strategy 的用法。

#### 代码
```python
[
    fac.AntdDivider(
        'showCheckedStrategy="show-all"（默认）',
        innerTextOrientation='left',
    ),
    fac.AntdTreeSelect(
        treeData=[
            {
                'key': '节点1',
                'value': '1',
                'title': '节点1',
                'children': [
                    {
                        'key': f'节点1-{i}',
                        'value': f'1-{i}',
                        'title': f'节点1-{i}',
                    }
                    for i in range(1, 5)
                ],
            },
            {'key': '节点2', 'value': '2', 'title': '节点2'},
        ],
        placeholder='请选择',
        multiple=True,
        treeCheckable=True,
        style={'width': 256},
    ),
    fac.AntdDivider(
        'showCheckedStrategy="show-parent"', innerTextOrientation='left'
    ),
    fac.AntdTreeSelect(
        treeData=[
            {
                'key': '节点1',
                'value': '1',
                'title': '节点1',
                'children': [
                    {
                        'key': f'节点1-{i}',
                        'value': f'1-{i}',
                        'title': f'节点1-{i}',
                    }
                    for i in range(1, 5)
                ],
            },
            {'key': '节点2', 'value': '2', 'title': '节点2'},
        ],
        placeholder='请选择',
        multiple=True,
        treeCheckable=True,
        showCheckedStrategy='show-parent',
        style={'width': 256},
    ),
    fac.AntdDivider(
        'showCheckedStrategy="show-child"', innerTextOrientation='left'
    ),
    fac.AntdTreeSelect(
        treeData=[
            {
                'key': '节点1',
                'value': '1',
                'title': '节点1',
                'children': [
                    {
                        'key': f'节点1-{i}',
                        'value': f'1-{i}',
                        'title': f'节点1-{i}',
                    }
                    for i in range(1, 5)
                ],
            },
            {'key': '节点2', 'value': '2', 'title': '节点2'},
        ],
        placeholder='请选择',
        multiple=True,
        treeCheckable=True,
        showCheckedStrategy='show-child',
        style={'width': 256},
    ),
]
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTreeSelect(
            treeData=[
                {
                    'key': '节点1',
                    'value': '1',
                    'title': '节点1',
                    'children': [
                        {
                            'key': f'节点1-{i}',
                            'value': f'1-{i}',
                            'title': f'节点1-{i}',
                        }
                        for i in range(1, 5)
                    ],
                },
                {'key': '节点2', 'value': '2', 'title': '节点2'},
            ],
            placeholder=f'status="{status}"',
            status=status,
            style={'width': 256},
        )
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
```

### suffix_icon

- 说明：演示 suffix_icon 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    suffixIcon=fac.AntdIcon(icon='antd-lock'),
    style={'width': 256},
)
```

### switcher_icon

- 说明：演示 switcher_icon 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    switcherIcon=fac.AntdIcon(icon='antd-down'),
    style={'width': 256},
)
```

### tree_check_strictly

- 说明：演示 tree_check_strictly 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    multiple=True,
    treeCheckable=True,
    treeCheckStrictly=True,
    style={'width': 256},
)
```

### tree_line

- 说明：演示 tree_line 的用法。

#### 代码
```python
fac.AntdTreeSelect(
    treeData=[
        {
            'key': '节点1',
            'value': '1',
            'title': '节点1',
            'children': [
                {
                    'key': f'节点1-{i}',
                    'value': f'1-{i}',
                    'title': f'节点1-{i}',
                }
                for i in range(1, 5)
            ],
        },
        {'key': '节点2', 'value': '2', 'title': '节点2'},
    ],
    placeholder='请选择',
    treeLine=True,
    treeDefaultExpandAll=True,
    style={'width': 256},
)
```

## 补充 API 说明

In the default mode, the `treeData` parameter is freely nested through the `children` field to construct any tree structure, where the legal parameters for each node are described as follows:

- title (string; required):

  The title of the current node.

- key (string; required):

  The unique identifier ID of the current node.

- children (list; optional):

  Defines the child nodes for the current node.

- value (string or number; optional):

  The unique value of the current node.

- disabled (boolean; default False):

  Whether the current node is disabled.

- checkable (boolean; optional):

  Controls whether the checkbox is displayed for the current node when `treeCheckable=True`.

- disableCheckbox (boolean; optional):

  Whether the checkbox of the current node is disabled when `treeCheckable=True`.

- selectable (boolean; optional):

  Whether the current node is clickable for selection.

- isLeaf (boolean; optional):

  Whether the current node is a leaf node (terminal node).
