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

## 示例源码（demos）

### `views/AntdTree/demos/async_load_node.py`
```python
import time
import feffery_antd_components as fac
from feffery_dash_utils.tree_utils import TreeManager
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/basic_callbacks.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/check_strictly.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/context_menu_callbacks.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/custom_node_style.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


code_string = [
    {
        'code': '''
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
'''
    }
]

```

### `views/AntdTree/demos/default_expand_all.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/drag_callbacks.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


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


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/drag_in_same_level.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/draggable.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/flat_tree_data.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/multiple.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/multiple_with_checkbox.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_check_status_style.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_check_status_suffix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_context_menu.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_favorited.py`
```python
import json
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


@app.callback(
    Output('tree-favorites-demo-output', 'children'),
    Input('tree-favorites-demo', 'favoritedKeys'),
)
def tree_favorites_demo(favoritedKeys):
    return json.dumps(
        dict(favoritedKeys=favoritedKeys), indent=4, ensure_ascii=False
    )


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_scroll.py`
```python
import random
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


@app.callback(
    Output('tree-scroll-demo', 'scrollTarget'),
    Input('tree-scroll-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def tree_scroll_demo(nClicks):
    return {'key': f'节点{random.randint(1, 51)}'}


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/node_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/not_show_line.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/show_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/switcher_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdTree/demos/tree_search.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
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

    return demo_contents


app.clientside_callback(
    """(value) => value""",
    Output('tree-search-demo', 'searchKeyword'),
    Input('tree-search-demo-keyword', 'value'),
)


code_string = [
    {
        'code': '''
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
'''
    }
]

```

### `views/AntdTree/demos/virtual_scroll.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTree(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

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
