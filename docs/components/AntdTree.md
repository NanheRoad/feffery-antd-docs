# AntdTree

## 简介源码：`views/AntdTree/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdTree 树形控件'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTree 树形控件', level=2),
        fac.AntdParagraph('用于渲染展示树形数据结构，并支持丰富的交互功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### async_load_node

- 说明：演示 async_load_node 的用法。

#### 代码
```python
from feffery_dash_utils.tree_utils import TreeManager

...

fac.AntdTree(
    id='tree-async-demo',
    treeData=[
        {
            'key': '节点1',
            'title': '节点1',
        },
        {
            'key': '节点2',
            'title': '节点2',
            'children': [
                {
                    'key': '节点2-1',
                    'title': '节点2-1',
                    'isLeaf': True,
                },
            ],
        },
        {
            'key': '节点3',
            'title': '节点3',
            'isLeaf': True,
        },
    ],
    enableAsyncLoad=True,
)

...

@app.callback(
    Output('tree-async-demo', 'treeData'),
    Input('tree-async-demo', 'loadingNode'),
    State('tree-async-demo', 'treeData'),
    prevent_initial_call=True,
)
def tree_demo(loadingNode, treeData):
    time.sleep(0.5)
    return TreeManager.update_tree_node(
        treeData,
        node_key=loadingNode['key'],
        new_node={
            'children': [
                {
                    'key': loadingNode['key'] + '-1',
                    'title': loadingNode['key'] + '-1',
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
    fac.AntdTree(
        id='tree-demo',
        treeData=[
            {
                'title': '四川省',
                'key': '四川省',
                'children': [
                    {'title': '成都市', 'key': '成都市'},
                    {'title': '广安市', 'key': '广安市'},
                ],
            },
            {
                'title': '重庆市',
                'key': '重庆市',
                'children': [
                    {
                        'title': '渝中区',
                        'key': '渝中区',
                        'children': [
                            {'title': '解放碑街道', 'key': '解放碑街道'}
                        ],
                    },
                    {'title': '渝北区', 'key': '渝北区'},
                ],
            },
        ],
        multiple=True,
        checkable=True,
    ),
    html.Pre(id='tree-demo-output'),
]

...

@app.callback(
    Output('tree-demo-output', 'children'),
    [
        Input('tree-demo', 'selectedKeys'),
        Input('tree-demo', 'checkedKeys'),
        Input('tree-demo', 'halfCheckedKeys'),
        Input('tree-demo', 'expandedKeys'),
    ],
)
def tree_demo(selectedKeys, checkedKeys, halfCheckedKeys, expandedKeys):
    return json.dumps(
        dict(
            selectedKeys=selectedKeys,
            checkedKeys=checkedKeys,
            halfCheckedKeys=halfCheckedKeys,
            expandedKeys=expandedKeys,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ]
)
```

### check_strictly

- 说明：演示 check_strictly 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    multiple=True,
    checkable=True,
    checkStrictly=True,
)
```

### context_menu_callbacks

- 说明：演示 context_menu_callbacks 的用法。

#### 代码
```python
[
    fac.AntdTree(
        id='tree-context-menu-demo',
        treeData=[
            {
                'title': '四川省',
                'key': '四川省',
                'children': [
                    {
                        'title': '成都市',
                        'key': '成都市',
                    },
                    {
                        'title': '广安市',
                        'key': '广安市',
                    },
                ],
                'contextMenu': [
                    {'key': f'四川省-操作选项{i}', 'label': f'操作选项{i}'}
                    for i in range(1, 6)
                ],
            },
            {
                'title': '重庆市',
                'key': '重庆市',
                'children': [
                    {
                        'title': '渝中区',
                        'key': '渝中区',
                        'children': [
                            {
                                'title': '解放碑街道',
                                'key': '解放碑街道',
                            }
                        ],
                    },
                    {
                        'title': '渝北区',
                        'key': '渝北区',
                    },
                ],
                'contextMenu': [
                    {
                        'key': f'重庆市-操作选项{i}',
                        'label': f'操作选项{i}',
                        'icon': 'antd-function',
                    }
                    for i in range(1, 6)
                ],
            },
        ],
    ),
    html.Pre(id='tree-context-menu-demo-output'),
]

...

@app.callback(
    Output('tree-context-menu-demo-output', 'children'),
    Input('tree-context-menu-demo', 'clickedContextMenu'),
)
def tree_context_menu_demo(clickedContextMenu):
    return json.dumps(
        dict(clickedContextMenu=clickedContextMenu),
        indent=4,
        ensure_ascii=False,
    )
```

### custom_node_style

- 说明：演示 custom_node_style 的用法。

#### 代码
```python
[
    # 动态样式
    fuc.FefferyStyle(
        rawStyle="""
.tree-node-style-demo1 {
    color: #2f9e44;
}

.tree-node-style-demo1:hover {
    color: #b2f2bb;
}

.tree-node-style-demo2 {
    color: #fd7e14;
}
"""
    ),
    fac.AntdTree(
        treeData=[
            {
                'title': '四川省',
                'key': '四川省',
                'className': 'tree-node-style-demo1',
                'children': [
                    {
                        'title': '成都市',
                        'key': '成都市',
                        'className': 'tree-node-style-demo1',
                    },
                    {
                        'title': '广安市',
                        'key': '广安市',
                        'className': 'tree-node-style-demo1',
                    },
                ],
            },
            {
                'title': '重庆市',
                'key': '重庆市',
                'className': 'tree-node-style-demo2',
                'children': [
                    {
                        'title': '渝中区',
                        'key': '渝中区',
                        'className': 'tree-node-style-demo2',
                        'children': [
                            {
                                'title': '解放碑街道',
                                'key': '解放碑街道',
                                'className': 'tree-node-style-demo2',
                            }
                        ],
                    },
                    {
                        'title': '渝北区',
                        'key': '渝北区',
                        'className': 'tree-node-style-demo2',
                    },
                ],
            },
        ],
        defaultExpandAll=True,
    ),
]
```

### default_expand_all

- 说明：演示 default_expand_all 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    defaultExpandAll=True,
)
```

### drag_callbacks

- 说明：演示 drag_callbacks 的用法。

#### 代码
```python
[
    fac.AntdTree(
        id='tree-drag-demo',
        treeData=[
            {
                'title': '四川省',
                'key': '四川省',
                'children': [
                    {'title': '成都市', 'key': '成都市'},
                    {'title': '广安市', 'key': '广安市'},
                ],
            },
            {
                'title': '重庆市',
                'key': '重庆市',
                'children': [
                    {
                        'title': '渝中区',
                        'key': '渝中区',
                        'children': [
                            {'title': '解放碑街道', 'key': '解放碑街道'}
                        ],
                    },
                    {'title': '渝北区', 'key': '渝北区'},
                ],
            },
        ],
        draggable=True,
    ),
    html.Pre(id='tree-drag-demo-output'),
]

...

@app.callback(
    Output('tree-drag-demo-output', 'children'),
    [
        Input('tree-drag-demo', 'treeData'),
        Input('tree-drag-demo', 'draggedNodeKey'),
    ],
)
def tree_drag_demo(treeData, draggedNodeKey):
    return json.dumps(
        dict(treeData=treeData, draggedNodeKey=draggedNodeKey),
        indent=4,
        ensure_ascii=False,
    )
```

### drag_in_same_level

- 说明：演示 drag_in_same_level 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '根节点',
            'key': '根节点',
            'children': [
                {
                    'title': f'节点{i}',
                    'key': f'节点{i}',
                }
                for i in range(1, 6)
            ],
        }
    ],
    draggable=True,
    dragInSameLevel=True,
    defaultExpandAll=True,
)
```

### draggable

- 说明：演示 draggable 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    draggable=True,
    defaultExpandAll=True,
)
```

### flat_tree_data

- 说明：演示 flat_tree_data 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {'title': '四川省', 'key': '四川省'},
        {'title': '成都市', 'key': '成都市', 'parent': '四川省'},
        {'title': '广安市', 'key': '广安市', 'parent': '四川省'},
        {'title': '重庆市', 'key': '重庆市'},
        {'title': '渝中区', 'key': '渝中区', 'parent': '重庆市'},
        {'title': '渝北区', 'key': '渝北区', 'parent': '重庆市'},
        {'title': '解放碑街道', 'key': '解放碑街道', 'parent': '渝中区'},
    ],
    treeDataMode='flat',
)
```

### multiple

- 说明：演示 multiple 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    multiple=True,
)
```

### multiple_with_checkbox

- 说明：演示 multiple_with_checkbox 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    multiple=True,
    checkable=True,
)
```

### node_check_status_style

- 说明：演示 node_check_status_style 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    defaultExpandAll=True,
    multiple=True,
    checkable=True,
    nodeCheckedStyle={'fontWeight': 'bold'},
    nodeUncheckedStyle={'textDecoration': 'line-through'},
)
```

### node_check_status_suffix

- 说明：演示 node_check_status_suffix 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    defaultExpandAll=True,
    multiple=True,
    checkable=True,
    nodeCheckedSuffix='🙂',
    nodeUncheckedSuffix='🙃',
)
```

### node_context_menu

- 说明：演示 node_context_menu 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {
                    'title': '成都市',
                    'key': '成都市',
                },
                {
                    'title': '广安市',
                    'key': '广安市',
                },
            ],
            'contextMenu': [
                {'key': f'四川省-操作选项{i}', 'label': f'操作选项{i}'}
                for i in range(1, 6)
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {
                            'title': '解放碑街道',
                            'key': '解放碑街道',
                        }
                    ],
                },
                {
                    'title': '渝北区',
                    'key': '渝北区',
                },
            ],
            'contextMenu': [
                {
                    'key': f'重庆市-操作选项{i}',
                    'label': f'操作选项{i}',
                    'icon': 'antd-function',
                }
                for i in range(1, 6)
            ],
        },
    ],
    defaultExpandAll=True,
)
```

### node_favorited

- 说明：演示 node_favorited 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTree(
            id='tree-favorites-demo',
            treeData=[
                {
                    'title': '四川省',
                    'key': '四川省',
                    'enableFavorites': False,
                    'children': [
                        {'title': '成都市', 'key': '成都市'},
                        {'title': '广安市', 'key': '广安市'},
                    ],
                },
                {
                    'title': '重庆市',
                    'key': '重庆市',
                    'enableFavorites': False,
                    'children': [
                        {
                            'title': '渝中区',
                            'key': '渝中区',
                            'children': [
                                {'title': '解放碑街道', 'key': '解放碑街道'}
                            ],
                        },
                        {'title': '渝北区', 'key': '渝北区'},
                    ],
                },
            ],
            defaultExpandAll=True,
            enableNodeFavorites=True,
        ),
        html.Pre(id='tree-favorites-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('tree-favorites-demo-output', 'children'),
    Input('tree-favorites-demo', 'favoritedKeys'),
)
def tree_favorites_demo(favoritedKeys):
    return json.dumps(
        dict(favoritedKeys=favoritedKeys), indent=4, ensure_ascii=False
    )
```

### node_scroll

- 说明：演示 node_scroll 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '随机滚动', id='tree-scroll-demo-trigger', type='primary'
        ),
        fac.AntdTree(
            id='tree-scroll-demo',
            treeData=[
                {
                    'title': '全部节点',
                    'key': '全部节点',
                    'children': [
                        {'title': f'节点{i}', 'key': f'节点{i}'}
                        for i in range(1, 51)
                    ],
                }
            ],
            defaultExpandAll=True,
            height=200,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('tree-scroll-demo', 'scrollTarget'),
    Input('tree-scroll-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def tree_scroll_demo(nClicks):
    return {'key': f'节点{random.randint(1, 51)}'}
```

### node_tooltip

- 说明：演示 node_tooltip 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'tooltipProps': {'title': 'tooltip示例😀'},
            'children': [
                {
                    'title': '成都市',
                    'key': '成都市',
                    'tooltipProps': {'title': 'tooltip示例😉'},
                },
                {
                    'title': '广安市',
                    'key': '广安市',
                    'tooltipProps': {'title': 'tooltip示例😉'},
                },
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'tooltipProps': {
                'title': 'tooltip示例😀',
                'placement': 'right',
            },
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'tooltipProps': {
                        'title': 'tooltip示例😉',
                        'placement': 'bottom',
                    },
                    'children': [
                        {
                            'title': '解放碑街道',
                            'key': '解放碑街道',
                            'tooltipProps': {
                                'title': 'tooltip示例😉',
                                'placement': 'left',
                            },
                        }
                    ],
                },
                {
                    'title': '渝北区',
                    'key': '渝北区',
                    'tooltipProps': {
                        'title': 'tooltip示例😉',
                        'placement': 'bottom',
                    },
                },
            ],
        },
    ],
    defaultExpandAll=True,
)
```

### not_show_line

- 说明：演示 not_show_line 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    showLine=False,
)
```

### show_icon

- 说明：演示 show_icon 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'icon': 'antd-cloud',
            'children': [
                {
                    'title': '成都市',
                    'key': '成都市',
                    'icon': 'antd-cloud-server',
                },
                {
                    'title': '广安市',
                    'key': '广安市',
                    'icon': 'antd-cloud-server',
                },
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'icon': 'antd-cloud',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'icon': 'antd-cloud-server',
                    'children': [
                        {
                            'title': '解放碑街道',
                            'key': '解放碑街道',
                            'icon': 'antd-cloud-server',
                        }
                    ],
                },
                {
                    'title': '渝北区',
                    'key': '渝北区',
                    'icon': 'antd-cloud-server',
                },
            ],
        },
    ],
    showIcon=True,
    defaultExpandAll=True,
)
```

### switcher_icon

- 说明：演示 switcher_icon 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': '四川省',
            'key': '四川省',
            'children': [
                {'title': '成都市', 'key': '成都市'},
                {'title': '广安市', 'key': '广安市'},
            ],
        },
        {
            'title': '重庆市',
            'key': '重庆市',
            'children': [
                {
                    'title': '渝中区',
                    'key': '渝中区',
                    'children': [
                        {'title': '解放碑街道', 'key': '解放碑街道'}
                    ],
                },
                {'title': '渝北区', 'key': '渝北区'},
            ],
        },
    ],
    switcherIcon=fac.AntdIcon(icon='antd-down', style={'color': '#ff7875'}),
)
```

### tree_search

- 说明：演示 tree_search 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdInput(
            id='tree-search-demo-keyword',
            placeholder='请输入搜索关键词',
            value='省',
            style={'width': '100%'},
        ),
        fac.AntdTree(
            id='tree-search-demo',
            treeData=[
                {
                    'title': '四川省',
                    'key': '四川省',
                    'children': [
                        {'title': '成都市', 'key': '成都市'},
                        {'title': '广安市', 'key': '广安市'},
                    ],
                },
                {
                    'title': '重庆市',
                    'key': '重庆市',
                    'children': [
                        {
                            'title': '渝中区',
                            'key': '渝中区',
                            'children': [
                                {'title': '解放碑街道', 'key': '解放碑街道'}
                            ],
                        },
                        {'title': '渝北区', 'key': '渝北区'},
                    ],
                },
            ],
            defaultExpandAll=True,
            highlightStyle={'background': '#ffffb8', 'padding': 0},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

app.clientside_callback(
    """(value) => value""",
    Output('tree-search-demo', 'searchKeyword'),
    Input('tree-search-demo-keyword', 'value'),
)
```

### virtual_scroll

- 说明：演示 virtual_scroll 的用法。

#### 代码
```python
fac.AntdTree(
    treeData=[
        {
            'title': f'节点{i}',
            'key': f'节点{i}',
            'children': [
                {
                    'title': f'节点{i}-{j}',
                    'key': f'节点{i}-{j}',
                }
                for j in range(1, 10)
            ],
        }
        for i in range(1, 101)
    ],
    height=200,
    style={'border': '1px dashed #ced4da'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- treeDataMode (a value equal to: 'tree', 'flat'; default 'tree'):
    对应`treeData`格式的渲染模式，可选项有`'tree'`（树形模式）、`'flat'`（扁平模式）
    默认值：`'tree'`.

- treeData (list; optional):
    定义构造树所需的数据结构，与`treeDataMode`一致.

- treeNodeKeyToTitle (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    针对树结构中的指定节点，定义作为标题的组件型内容，优先级高于`treeData`中对应的`title`值.

- showIcon (boolean; default False):
    是否渲染节点额外图标  默认值：`False`.

- selectable (boolean; default True):
    节点是否可点击选择  默认值：`True`.

- multiple (boolean; default False):
    节点是否允许多选  默认值：`False`.

- checkable (boolean; default False):
    节点是否可勾选  默认值：`False`.

- defaultExpandAll (boolean; default False):
    初始化是否展开全部节点  默认值：`False`.

- expandedKeys (list of strings; optional):
    监听或设置已展开节点`key`值数组.

- defaultExpandedKeys (list of strings; optional):
    初始化已展开节点`key`值数组.

- defaultExpandParent (boolean; default False):
    初始化是否展开处于展开状态节点的父节点  默认值：`True`.

- selectedKeys (list of strings; optional):
    监听或设置已选择节点`key`值数组.

- defaultSelectedKeys (list of strings; optional):
    初始化已选择节点`key`值数组.

- checkedKeys (list of strings; optional):
    监听或设置已勾选节点`key`值数组.

- defaultCheckedKeys (list of strings; optional):
    初始化已勾选节点`key`值数组.

- halfCheckedKeys (list of strings; optional):
    监听或设置处于半勾选状态下的节点`key`值数组.

- checkStrictly (boolean; default False):
    节点与其后代节点之间的选择行为是否彼此独立  默认值：`False`.

- showLine (dict; default { 'showLeafIcon': False }):
    是否显示连接线.

    `showLine` is a boolean | dict with keys:

    - showLeafIcon (boolean; optional):
        叶节点是否渲染前缀图标.

- switcherIcon (a list of or a singular dash component, string or number; optional):
    组件型，自定义树节点的展开/折叠图标.

- height (number; optional):
    虚拟滚动模式下的组件最大像素高度，未设置时则不启用虚拟滚动功能.

- draggable (boolean; default False):
    节点是否可拖拽  默认值：`False`.

- showDragIcon (boolean; default True):
    开启节点拖拽功能后，是否为节点渲染拖拽图标  默认值：`True`.

- dragInSameLevel (boolean; default False):
    当`draggable=True`时，是否仅允许同级拖拽  默认值：`False`.

- dragDisabledKeys (list of strings; optional):
    禁止进行拖拽调整的节点`key`值数组  默认值：`[]`.

- dropDisabledKeys (list of strings; optional):
    禁止进行拖拽放置的节点`key`值数组  默认值：`[]`.

- draggedNodeKey (string; optional):
    监听最近一次被拖拽节点`key`值信息.

- clickedContextMenu (dict; optional):
    监听节点右键菜单项点击事件.

    `clickedContextMenu` is a dict with keys:

    - nodeKey (string; optional):
        事件对应节点`key`值.

    - menuKey (string; optional):
        事件对应右键菜单项`key`值.

    - timestamp (number; optional):
        事件对应时间戳信息.

- enableNodeFavorites (boolean; default False):
    是否启用节点收藏功能  默认值：`False`.

- favoritedKeys (list of strings; optional):
    监听或设置已收藏节点`key`值数组.

- scrollTarget (dict; optional):
    执行滚动到指定节点的动作，每次执行完毕后会重置为空值.

    `scrollTarget` is a dict with keys:

    - key (string; required):
        滚动目标节点`key`值.

    - align (a value equal to: 'top', 'bottom', 'auto'; optional):
        滚动目标节点对齐位置，可选项有`'top'`、`'bottom'`、`'auto'`  默认值：`'auto'`.

    - offset (number; optional):
        滚动后的像素偏移量.

- searchKeyword (string | list of strings; optional):
    快捷树搜索功能对应的单个关键词，或由多个关键词构成的数组.

- caseSensitive (boolean; default True):
    针对`searchKeyword`，是否大小写敏感  默认值：`True`.

- highlightStyle (dict; default {
    fontWeight: 'bold',
    backgroundColor: 'transparent',
    padding: 0,
    color: '#ff5500'
}):
    快捷树搜索关键词匹配部分的高亮样式.

- nodeCheckedSuffix (a list of or a singular dash component, string or number; optional):
    组件型，节点勾选状态下的后缀元素.

- nodeUncheckedSuffix (a list of or a singular dash component, string or number; optional):
    组件型，节点非勾选状态下的后缀元素.

- nodeCheckedStyle (dict; optional):
    节点勾选状态下的css样式.

- nodeUncheckedStyle (dict; optional):
    节点非勾选状态下的css样式.

- enableAsyncLoad (boolean; default False):
    是否开启子节点异步加载功能，开启后无`children`属性，且未设置`isLeaf`为`True`的节点将可展开并触发`loadingNode`事件更新
    默认值：`False`.

- loadingNode (dict; optional):
    监听触发异步数据加载的节点展开事件信息.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'selectedKeys', 'checkedKeys', 'expandedKeys', 'halfCheckedKeys's; optional):
    开启属性持久化功能的若干属性名，可选项有`'selectedKeys'`、`'checkedKeys'`、`'expandedKeys'`、`'halfCheckedKeys'`
    默认值：`['selectedKeys', 'checkedKeys', 'expandedKeys',
    'halfCheckedKeys']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.

## 补充 API 说明

In the default mode, the `treeData` parameter is freely nested through the `children` field to construct any tree structure, where the valid parameters for each node are as follows:

- title (string; required):

  The title of the current node.

- key (string; required):

  The unique identifier for the current node.

- children (list; optional):

  Defines the child nodes for the current node.

- disabled (boolean; default False):

  Whether the current node is disabled.

- icon (string; optional):

  The prefix icon type for the current node. When `iconRenderer` is `'AntdIcon'`, it corresponds to the same parameter in `AntdIcon`. When `iconRenderer` is `'fontawesome'`, it is the CSS class name.

- iconRenderer (options: 'AntdIcon', 'fontawesome'; optional):

  The rendering method for the prefix icon of the current node. Options include `'AntdIcon'` and `'fontawesome'`.

- checkable (boolean; optional):

  When the overall `checkable=True` for the tree component, it controls whether the checkbox is rendered for the current node.

- disableCheckbox (boolean; optional):

  When the overall `checkable=True` for the tree component, it controls whether the checkbox for the current node is disabled.

- selectable (boolean; optional):

  Whether the current node is clickable for selection.

- enableFavorites (boolean; optional):

  When the overall `enableNodeFavorites=True` for the tree component, it controls whether the current node can be favorited.

- style (dict; optional):

  The CSS style for the current node.

- className (string; optional):

  The CSS class name for the current node.

- tooltipProps (dict; optional):

  Configures the tooltip-related parameters for the current node.

  - title (string; optional):

    The content of the tooltip for the current node.

  - placement (options: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight'; default 'top'):

    The direction in which the tooltip for the current node expands. Options include `'top'`, `'left'`, `'right'`, `'bottom'`, `'topLeft'`, `'topRight'`, `'bottomLeft'`, and `'bottomRight'`.

- contextMenu (dict; optional):

  Configures the context menu-related parameters for the current node.

  - key (string; optional):

    The unique identifier for the current context menu item.

  - label (string; optional):

    The title content of the current context menu item.

  - icon (string; optional):

    The prefix icon type for the current node. When `iconRenderer` is `'AntdIcon'`, it corresponds to the same parameter in `AntdIcon`. When `iconRenderer` is `'fontawesome'`, it is the CSS class name.

  - iconRenderer (options: 'AntdIcon', 'fontawesome'; optional):

    The rendering method for the prefix icon of the current node. Options include `'AntdIcon'` and `'fontawesome'`.

- isLeaf (boolean; optional):

  Whether the current node is a leaf node.
