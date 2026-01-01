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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- dataSource (list of dicts; optional):
    配置选项.

    `dataSource` is a list of dicts with keys:

    - key (string | number; optional):
        当前选项唯一识别id.

    - title (a list of or a singular dash component, string or number; optional):
        组件型，当前选项标题内容.

    - disabled (boolean; optional):
        是否禁用当前选项  默认值：`False`.

- selectionsIcon (a list of or a singular dash component, string or number; optional):
    组件型，自定义下拉菜单图标.

- height (string | number; optional):
    穿梭框整体高度.

- pagination (dict; default False):
    选项分页展示配置  默认值：`False`.

    `pagination` is a boolean | dict with keys:

    - pageSize (number; optional):
        每页最大选项数.

- oneWay (boolean; default False):
    是否启用单向模式  默认值：`False`.

- operations (list of a list of or a singular dash component, string or numbers; default ['', '']):
    左右移动操作按钮内容  默认值：`'['', '']'`.

- showSearch (boolean; default False):
    是否显示搜索框  默认值：`False`.

- optionFilterMode (a value equal to: 'case-insensitive', 'case-sensitive', 'regex'; default 'case-insensitive'):
    搜索匹配模式，可选项有`'case-insensitive'`（大小写不敏感）、`'case-sensitive'`（大小写敏感）、`'regex'`（正则表达式）
    默认值：`'case-insensitive'`.

- showSelectAll (boolean; default True):
    是否显示全选勾选框  默认值：`True`.

- titles (list of a list of or a singular dash component, string or numbers; optional):
    左右标题内容.

- targetKeys (list of number | strings; optional):
    监听或设置右侧区域已选项`key`值.

- moveDirection (a value equal to: 'left', 'right'; optional):
    监听最近一次选项移动对应方向，可选项有`'left'`、`'right'`.

- moveKeys (list of number | strings; optional):
    监听最近一次选项移动涉及的选项`key`值.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- readOnly (boolean; default False):
    是否渲染为只读状态  默认值：`False`.

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

- persisted_props (list of a value equal to: 'targetKeys's; optional):
    开启属性持久化功能的若干属性名，可选项有`'targetKeys'`  默认值：`['targetKeys']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
