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
