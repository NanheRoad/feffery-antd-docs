# AntdTabs

## 简介源码：`views/AntdTabs/intro.py`
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
                {'title': '标签页 AntdTabs'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('标签页 AntdTabs', level=2),
        fac.AntdParagraph('用于构建多标签页。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
[
    fac.AntdTabs(
        id='tabs-demo',
        items=[
            {'label': f'标签页{i}', 'key': f'标签页{i}'}
            for i in range(1, 6)
        ],
        defaultActiveKey='标签页3',
    ),
    fac.AntdText(id='tabs-demo-output'),
]

...

@app.callback(
    Output('tabs-demo-output', 'children'), Input('tabs-demo', 'activeKey')
)
def tabs_demo(activeKey):
    return f'activeKey: {activeKey}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {
            'key': f'标签页{i}',
            'label': f'标签页{i}',
            'children': fac.AntdCenter(
                f'这是标签页{i}的内容示例',
                style={
                    'fontSize': 18,
                    'background': f'rgba(28, 126, 214, calc(1 - 0.2 * {i}))',
                    'height': 200,
                },
            ),
        }
        for i in range(1, 6)
    ]
)
```

### centered

- 说明：演示 centered 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {'key': f'标签页{i}', 'label': f'标签页{i}'} for i in range(1, 6)
    ],
    centered=True,
)
```

### custom_tab_title

- 说明：演示 custom_tab_title 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {
            'key': f'标签页{i}',
            'label': fac.AntdSpace(
                [
                    fac.AntdText(f'标签页{i}'),
                    fac.AntdTooltip(
                        fac.AntdIcon(
                            icon='antd-question-circle',
                            style={'color': '#9b9b9b'},
                        ),
                        title=f'这是标签页{i}balabalabala',
                        placement='right',
                    ),
                ]
            ),
        }
        for i in range(1, 6)
    ]
)
```

### different_tab_position

- 说明：演示 different_tab_position 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTabs(
            items=[
                {
                    'key': f'标签页{i}',
                    'label': f'标签页{i}',
                    'children': fac.AntdCenter(
                        f'这是标签页{i}的内容示例',
                        style={
                            'fontSize': 18,
                            'background': f'rgba(28, 126, 214, calc(1 - 0.2 * {i}))',
                            'height': 260,
                        },
                    ),
                }
                for i in range(1, 6)
            ],
            tabPosition=position,
        )
        for position in ['top', 'left', 'bottom', 'right']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### different_type

- 说明：演示 different_type 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTabs(
            items=[
                {'key': f'标签页{i}', 'label': f'标签页{i}'}
                for i in range(1, 6)
            ],
            type=type_,
        )
        for type_ in ['line', 'card', 'editable-card']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### disabled_tabs

- 说明：演示 disabled_tabs 的用法。

#### 代码
```python
[
    fac.AntdDivider('基于disabled参数', innerTextOrientation='left'),
    fac.AntdTabs(
        items=[
            {
                'key': f'标签页{i}',
                'label': f'标签页{i}',
                'disabled': i in [3, 4],
            }
            for i in range(1, 6)
        ]
    ),
    fac.AntdDivider('基于disabledTabKeys参数', innerTextOrientation='left'),
    fac.AntdTabs(
        items=[
            {'key': f'标签页{i}', 'label': f'标签页{i}'}
            for i in range(1, 6)
        ],
        disabledTabKeys=['标签页3', '标签页4'],
    ),
]
```

### extra_content

- 说明：演示 extra_content 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {'key': f'标签页{i}', 'label': f'标签页{i}'} for i in range(1, 6)
    ],
    tabBarLeftExtraContent=fac.AntdButton('示例1'),
    tabBarRightExtraContent=fac.AntdButton('示例2'),
    centered=True,
)
```

### icon

- 说明：演示 icon 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {
            'key': f'标签页{i}',
            'label': f'标签页{i}',
            'icon': fac.AntdIcon(icon='antd-user'),
        }
        for i in range(1, 6)
    ]
)
```

### placeholder

- 说明：演示 placeholder 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[],
    placeholder=fac.AntdEmpty(description='当前没有可用的标签页哦'),
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTabs(
            items=[
                {'key': f'标签页{i}', 'label': f'标签页{i}'}
                for i in range(1, 6)
            ],
            size=size,
        )
        for size in ['small', 'default', 'large']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### tab_add_delete

- 说明：演示 tab_add_delete 的用法。

#### 代码
```python
[
    fac.AntdTabs(
        id='tabs-add-delete-demo',
        type='editable-card',
        items=[
            {
                'label': f'标签页{i}',
                'key': str(i),
                'children': fac.AntdCenter(
                    f'标签页{i}',
                    style={
                        'height': 200,
                        'fontSize': 28,
                    },
                ),
                'closable': not (i == 1),
            }
            for i in range(1, 6)
        ],
        tabBarRightExtraContent=fac.AntdIcon(
            id='tabs-add-delete-demo-add',
            icon='antd-plus-circle-two-tone',
            style={'fontSize': 20, 'cursor': 'pointer'},
        ),
    ),
    fac.Fragment(id='tabs-add-delete-demo-tab-count'),
]

...

@app.callback(
    [
        Output('tabs-add-delete-demo', 'items'),
        Output('tabs-add-delete-demo', 'activeKey'),
    ],
    [
        Input('tabs-add-delete-demo-add', 'nClicks'),
        Input('tabs-add-delete-demo', 'latestDeletePane'),
    ],
    [
        State('tabs-add-delete-demo', 'items'),
        State('tabs-add-delete-demo', 'activeKey'),
    ],
)
def tabs_add_delete_demo(nClicks, latestDeletePane, origin_items, activeKey):
    if dash.ctx.triggered_id == 'tabs-add-delete-demo-add':
        # 提取已有items中的最大key值
        origin_max_key = max([int(item['key']) for item in origin_items])

        return [
            [
                *origin_items,
                {
                    'label': f'标签页{origin_max_key+1}',
                    'key': str(origin_max_key + 1),
                    'children': fac.AntdCenter(
                        f'标签页{origin_max_key+1}',
                        style={
                            'height': 200,
                            'fontSize': 28,
                        },
                    ),
                },
            ],
            str(origin_max_key + 1),
        ]

    elif dash.ctx.triggered_id == 'tabs-add-delete-demo':
        return [
            [item for item in origin_items if item['key'] != latestDeletePane],
            '1' if latestDeletePane == activeKey else dash.no_update,
        ]

    return dash.no_update


@app.callback(
    Output('tabs-add-delete-demo-tab-count', 'children'),
    Input('tabs-add-delete-demo', 'tabCount'),
    State('tabs-add-delete-demo', 'tabCloseCounts'),
    prevent_initial_call=True,
)
def tabs_add_delete_demo_tab_count(tabCount, tabCloseCounts):
    return fac.AntdMessage(
        content=f'标签页自由增删示例 tabCount: {tabCount}，标签页关闭次数：{tabCloseCounts}',
        type='info',
    )
```

### tab_animation

- 说明：演示 tab_animation 的用法。

#### 代码
```python
[
    fac.AntdForm(
        [
            fac.AntdFormItem(
                fac.AntdSwitch(
                    id='tabs-animation-demo-inkBarAnimated',
                    checked=True,
                    checkedChildren='True',
                    unCheckedChildren='False',
                ),
                label='inkBarAnimated',
            ),
            fac.AntdFormItem(
                fac.AntdSwitch(
                    id='tabs-animation-demo-tabPaneAnimated',
                    checked=False,
                    checkedChildren='True',
                    unCheckedChildren='False',
                ),
                label='tabPaneAnimated',
            ),
        ],
        layout='inline',
    ),
    fac.AntdTabs(
        id='tabs-animation-demo',
        items=[
            {
                'key': f'标签页{i}',
                'label': f'标签页{i}',
                'children': fac.AntdCenter(
                    f'这是标签页{i}的内容示例',
                    style={
                        'fontSize': 18,
                        'background': f'rgba(28, 126, 214, calc(1 - 0.2 * {i}))',
                        'height': 200,
                    },
                ),
            }
            for i in range(1, 6)
        ],
    ),
]

...

app.clientside_callback(
    """(inkBarAnimated, tabPaneAnimated) => [inkBarAnimated, tabPaneAnimated]""",
    [
        Output('tabs-animation-demo', 'inkBarAnimated'),
        Output('tabs-animation-demo', 'tabPaneAnimated'),
    ],
    [
        Input('tabs-animation-demo-inkBarAnimated', 'checked'),
        Input('tabs-animation-demo-tabPaneAnimated', 'checked'),
    ],
)
```

### tab_bar_gutter

- 说明：演示 tab_bar_gutter 的用法。

#### 代码
```python
[
    fac.AntdSlider(
        id='tabs-gutter-demo-slider',
        min=20,
        max=60,
        step=5,
        defaultValue=20,
        tooltipVisible=False,
        marks={i * 5: f'{i*5}px' for i in range(1, 13)},
    ),
    fac.AntdTabs(
        id='tabs-gutter-demo',
        items=[
            {'key': f'标签页{i}', 'label': f'标签页{i}'}
            for i in range(1, 6)
        ],
    ),
]

...

app.clientside_callback(
    """(value) => value""",
    Output('tabs-gutter-demo', 'tabBarGutter'),
    Input('tabs-gutter-demo-slider', 'value'),
)
```

### tab_bar_style

- 说明：演示 tab_bar_style 的用法。

#### 代码
```python
fac.AntdTabs(
    items=[
        {'key': f'标签页{i}', 'label': f'标签页{i}'} for i in range(1, 6)
    ],
    tabBarStyle={'background': '#e6f7ff'},
)
```

### tab_context_menu

- 说明：演示 tab_context_menu 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTabs(
            id='tabs-context-menu-demo',
            items=[
                {
                    'label': f'标签页{i}',
                    'key': f'标签页{i}',
                    'contextMenu': [
                        {'key': f'菜单项{j}', 'label': f'菜单项{j}'}
                        for j in range(1, 6)
                    ],
                }
                for i in range(1, 6)
            ],
            size='large',
        ),
        html.Pre(id='tabs-context-menu-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('tabs-context-menu-demo-output', 'children'),
    Input('tabs-context-menu-demo', 'clickedContextMenu'),
)
def tabs_context_menu_demo(clickedContextMenu):
    return json.dumps(
        dict(clickedContextMenu=clickedContextMenu),
        indent=4,
        ensure_ascii=False,
    )
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- type (a value equal to: 'line', 'card', 'editable-card'; default 'line'):
    标签页类型，可选项有`'line'`、`'card'`、`'editable-card'`  默认值：`'line'`.

- items (list of dicts; optional):
    定义标签项.

    `items` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，标签页标题.

    - key (string; optional):
        标签页唯一识别id.

    - children (a list of or a singular dash component, string or number; optional):
        组件型，标签页内部元素.

    - icon (a list of or a singular dash component, string or number; optional):
        组件型，标签页图标元素.

    - closeIcon (boolean | a list of or a singular dash component, string or number; optional):
        `'editable-card'`型标签页可用，用于自定义关闭按钮，设置为`None`或`False`时会隐藏默认的关闭按钮.

    - destroyInactiveTabPane (boolean; optional):
        是否在当前标签页隐藏时，自动销毁当前标签页内部元素  默认值：`False`.

    - disabled (boolean; optional):
        是否禁用当前标签页  默认值：`False`.

    - forceRender (boolean; optional):
        初始化是否强制渲染当前标签页内部元素  默认值：`False`.

    - closable (boolean; optional):
        `'editable-card'`型标签页可用，控制当前标签页是否可被关闭  默认值：`True`.

    - contextMenu (list of dicts; optional):
        为当前标签页标题配置右键菜单相关参数.

        `contextMenu` is a list of dicts with keys:

        - key (string; optional):

            当前右键菜单项唯一标识id.

        - label (string; optional):

            当前右键菜单项标题.

        - icon (string; optional):

            当前右键菜单项前缀图标类型，`iconRenderer`为`'AntdIcon'`时同`AntdIcon`同名参数，`iconRenderer`为`'fontawesome'`时为css类名.

        - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):

            当前右键菜单项前缀图标渲染方式，可选项有`'AntdIcon'`、`'fontawesome'`.

- itemKeys (list of strings; optional):
    监听当前各标签页`key`值，顺序与`items`一致.

- activeKey (string; optional):
    监听或设置当前激活的标签页对应`key`值.

- defaultActiveKey (string; optional):
    初始化激活的标签页对应`key`值.

- disabledTabKeys (list of strings; optional):
    呈现禁用状态的标签页`key`值数组，优先级高于`items`中各标签页的`disabled`设定.

- tabPosition (a value equal to: 'top', 'left', 'right', 'bottom'; default 'top'):
    标签页切换控件显示方位，可选项有`'top'`、`'left'`、`'right'`、`'bottom'`
    默认值：`'top'`.

- size (a value equal to: 'small', 'default', 'large'; default 'default'):
    当前组件尺寸规格，可选项有`'small'`、`'default'`、`'large'`  默认值：'default'.

- centered (boolean; default False):
    是否居中显示标签页切换控件  默认值：`False`.

- indicator (dict; optional):
    配置指示条长度及对齐方式.

    `indicator` is a dict with keys:

    - size (number; optional):
        指示条像素宽度，当传入负数时，表示在完整宽度基础上应减去的像素宽度，默认与标签卡片同宽.

    - align (a value equal to: 'start', 'center', 'end'; optional):
        指示条对齐方式，可选项有`'start'`、`'center'`、`'end'`.

- tabBarGutter (number; optional):
    标签卡片之间的像素间距.

- tabBarStyle (dict; optional):
    标签卡片css样式.

- inkBarAnimated (boolean; default True):
    标签卡片切换是否添加动画效果  默认值：`True`.

- tabPaneAnimated (boolean; default False):
    标签内容切换是否添加动画效果  默认值：`False`.

- latestDeletePane (string; optional):
    监听最近一次删除操作对应的标签页`key`值.

- tabCloseCounts (number; default 0):
    标签页关闭按钮累计点击次数  默认值：`0`.

- tabBarLeftExtraContent (a list of or a singular dash component, string or number; optional):
    组件型，第一方位额外元素.

- tabBarRightExtraContent (a list of or a singular dash component, string or number; optional):
    组件型，第二方位额外元素.

- tabCount (number; optional):
    监听标签页数量.

- destroyInactiveTabPane (boolean; default False):
    统一设置是否自动销毁取消激活状态的标签页内部元素.

- clickedContextMenu (dict; optional):
    监听标签页标题右键菜单项相关点击事件.

    `clickedContextMenu` is a dict with keys:

    - tabKey (string; optional):
        被点击的右键菜单项对应标签页`key`值.

    - menuKey (string; optional):
        被点击的右键菜单项对应`key`值.

    - timestamp (number; optional):
        事件对应时间戳信息.

- placeholder (a list of or a singular dash component, string or number; optional):
    当`items`为空或长度为`0`时，替代进行占位显示的内容.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'activeKey's; optional):
    开启属性持久化功能的若干属性名，可选项有`'activeKey'`  默认值：`['activeKey']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
