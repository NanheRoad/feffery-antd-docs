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
