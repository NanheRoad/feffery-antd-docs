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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- popupClassName (string; optional):
    展开菜单css类名.

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- treeDataMode (a value equal to: 'tree', 'flat'; default 'tree'):
    对应`treeData`格式的渲染模式，可选项有`'tree'`（树形模式）、`'flat'`（扁平模式）
    默认值：`'tree'`.

- treeData (list; required):
    定义构造树所需的数据结构，与`treeDataMode`一致.

- treeNodeKeyToTitle (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    针对树结构中的指定节点，定义作为标题的组件型内容，优先级高于`treeData`中对应的`title`值.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    设置形态变体类型，可选的有'outlined'、'borderless'、'filled'、`'underlined'`，其中'outlined'等价于bordered=True，优先级高于bordered.

- placeholder (string; optional):
    输入框占位文字内容.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):
    选择菜单展开方向，可选项有`'bottomLeft'`、`'bottomRight'`、`'topLeft'`、`'topRight'`
    默认值：`'bottomLeft'`.

- treeLine (boolean; default False):
    是否显示连接线  默认值：`False`.

- value (string | number | list of string | numbers; optional):
    监听或设置已选值.

- defaultValue (string | number | list of string | numbers; optional):
    初始化已选值.

- maxCount (number; optional):
    当`multiple=True`时，可选中的最大数量
    如果`showCheckedStrategy='show-all'`且`treeCheckStrictly=False`，或者`showCheckedStrategy='show-parent'`，则`maxCount`无效.

- maxTagCount (number | a value equal to: 'responsive'; optional):
    当`multiple=True`时，已选值tag展示的最大数量.

- maxTagPlaceholder (a list of or a singular dash component, string or number; optional):
    当`multiple=True`时，隐藏已选值tag时显示的内容.

- maxTagTextLength (number; optional):
    当`multiple=True`时，最大显示的已选值tag文本长度.

- listHeight (number; default 256):
    选择菜单最大像素高度  默认值：`256`.

- multiple (boolean; default False):
    是否开启多选模式  默认值：`False`.

- suffixIcon (a list of or a singular dash component, string or number; optional):
    组件型，自定义的选择框后缀图标.

- switcherIcon (a list of or a singular dash component, string or number; optional):
    组件型，自定义树节点的展开/折叠图标.

- treeCheckable (boolean; default False):
    树节点是否可勾选  默认值：`False`.

- treeCheckStrictly (boolean; default False):
    节点与其后代节点之间的选择行为是否彼此独立  默认值：`False`.

- treeDefaultExpandAll (boolean; default False):
    初始化是否展开全部节点  默认值：`False`.

- treeDefaultExpandedKeys (list of strings; optional):
    初始化已展开节点`key`值数组.

- treeExpandedKeys (list of strings; optional):
    监听或设置已展开节点`key`值数组.

- virtual (boolean; default True):
    是否开启虚拟滚动  默认值：`True`.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- allowClear (boolean; default True):
    是否允许一键清空已选值  默认值：`True`.

- treeNodeFilterProp (a value equal to: 'title', 'value'; default 'value'):
    基于搜索框中输入内容进行搜索的目标字段，可选项有`'value'`、`'title'`  默认值：`'value'`.

- treeNodeFilterMode (a value equal to: 'case-insensitive', 'case-sensitive', 'regex'; default 'case-insensitive'):
    搜索匹配模式，可选项有`'case-insensitive'`（大小写不敏感）、`'case-sensitive'`（大小写敏感）、`'regex'`（正则表达式）
    默认值：`'case-insensitive'`.

- autoClearSearchValue (boolean; default True):
    当`multiple=True`时，设置是否在选中项后自动清空搜索框中的内容  默认值：`True`.

- showCheckedStrategy (a value equal to: 'show-all', 'show-parent', 'show-child'; default 'show-all'):
    已选项回填搜索框策略，可选项有`'show-all'`、`'show-parent'`、`'show-child'`
    默认值：`'show-all'`.

- dropdownBefore (a list of or a singular dash component, string or number; optional):
    组件型，选择菜单前缀内容.

- dropdownAfter (a list of or a singular dash component, string or number; optional):
    组件型，选择菜单后缀内容.

- prefix (a list of or a singular dash component, string or number; optional):
    组件型，前缀内嵌内容.

- readOnly (boolean; optional):
    是否渲染为只读状态  默认值：`False`.

- enableAsyncLoad (boolean; default False):
    是否开启子节点异步加载功能，开启后无`children`属性，且未设置`isLeaf`为`True`的节点将可展开并触发`loadingNode`事件更新
    默认值：`False`.

- loadingNode (dict; optional):
    监听触发异步数据加载的节点展开事件信息.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.

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
