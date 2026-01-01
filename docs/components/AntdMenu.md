# AntdMenu

## 简介源码：`views/AntdMenu/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('导航')},
                {'title': translator.t('AntdMenu 导航菜单')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdMenu 导航菜单'), level=2),
        fac.AntdParagraph(
            translator.t(
                '导航菜单用于引导用户在不同层级的页面之间进行跳转，一般分为顶部导航和侧边导航，顶部导航提供全局性的类目和功能，侧边导航提供多级结构来收纳和排列网站架构。'
            )
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 进阶回调监听

- 说明：通过回调监听参数`currentItem`、`currentKeyPath`、`currentItemPath`获取更多选中项相关信息。

#### 代码
```python
[
    fac.AntdMenu(
        id='menu-advanced-demo',
        currentKey='1-1-1',
        menuItems=[
            {
                'component': 'SubMenu',
                'props': {
                    'key': f'{sub_menu}',
                    'title': f'子菜单{sub_menu}',
                },
                'children': [
                    {
                        'component': 'ItemGroup',
                        'props': {
                            'key': f'{sub_menu}-{item_group}',
                            'title': f'菜单项分组{sub_menu}-{item_group}',
                        },
                        'children': [
                            {
                                'component': 'Item',
                                'props': {
                                    'key': f'{sub_menu}-{item_group}-{item}',
                                    'title': f'菜单项{sub_menu}-{item_group}-{item}',
                                },
                            }
                            for item in range(1, 3)
                        ],
                    }
                    for item_group in range(1, 3)
                ],
            }
            for sub_menu in range(1, 5)
        ],
        mode='horizontal',
    ),
    html.Pre(
        id='menu-advanced-demo-output',
        style={'maxHeight': 400, 'overflowY': 'auto'},
    ),
]

...

@app.callback(
    Output('menu-advanced-demo-output', 'children'),
    [
        Input('menu-advanced-demo', 'currentItem'),
        Input('menu-advanced-demo', 'currentKeyPath'),
        Input('menu-advanced-demo', 'currentItemPath'),
    ],
)
def menu_advanced_callback_demo(currentItem, currentKeyPath, currentItemPath):
    return json.dumps(
        dict(
            currentItem=currentItem,
            currentKeyPath=currentKeyPath,
            currentItemPath=currentItemPath,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### 菜单项链接跳转

- 说明：菜单项节点可设置对应的跳转链接地址。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'Item',
            'props': {
                'key': 'AntdMenu文档页',
                'title': 'AntdMenu文档页',
                'href': '/AntdMenu',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': 'fac仓库',
                'title': 'fac仓库',
                'href': 'https://github.com/CNFeffery/feffery-antd-components',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': 'fuc仓库',
                'title': 'fuc仓库',
                'href': 'https://github.com/CNFeffery/feffery-utils-components',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': 'fmc仓库',
                'title': 'fmc仓库',
                'href': 'https://github.com/CNFeffery/feffery-markdown-components',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': 'feffery博客园',
                'title': 'feffery博客园',
                'href': 'https://www.cnblogs.com/feffery/',
            },
        },
    ],
    mode='inline',
    defaultSelectedKey='AntdMenu文档页',
    style={'width': 256},
)
```

### 回调监听

- 说明：通过回调监听当前选中的菜单项。

#### 代码
```python
[
    fac.AntdMenu(
        id='menu-demo',
        currentKey='1-1-1',
        menuItems=[
            {
                'component': 'SubMenu',
                'props': {
                    'key': f'{sub_menu}',
                    'title': f'子菜单{sub_menu}',
                },
                'children': [
                    {
                        'component': 'ItemGroup',
                        'props': {
                            'key': f'{sub_menu}-{item_group}',
                            'title': f'菜单项分组{sub_menu}-{item_group}',
                        },
                        'children': [
                            {
                                'component': 'Item',
                                'props': {
                                    'key': f'{sub_menu}-{item_group}-{item}',
                                    'title': f'菜单项{sub_menu}-{item_group}-{item}',
                                },
                            }
                            for item in range(1, 3)
                        ],
                    }
                    for item_group in range(1, 3)
                ],
            }
            for sub_menu in range(1, 5)
        ],
        mode='horizontal',
    ),
    html.Div(
        id='menu-demo-output',
        style={
            'height': '200px',
            'background': '#a5d8ff',
            'color': 'white',
            'fontSize': '24px',
            'display': 'flex',
            'justifyContent': 'center',
            'alignItems': 'center',
        },
    ),
]

...

@app.callback(
    Output('menu-demo-output', 'children'), Input('menu-demo', 'currentKey')
)
def menu_callback_demo(currentKey):
    return f'currentKey: {currentKey}'
```

### 基础使用

- 说明：基础的导航菜单。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'SubMenu',
            'props': {
                'key': f'{sub_menu}',
                'title': f'子菜单{sub_menu}',
            },
            'children': [
                {
                    'component': 'ItemGroup',
                    'props': {
                        'key': f'{sub_menu}-{item_group}',
                        'title': f'菜单项分组{sub_menu}-{item_group}',
                    },
                    'children': [
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'{sub_menu}-{item_group}-{item}',
                                'title': f'菜单项{sub_menu}-{item_group}-{item}',
                            },
                        }
                        for item in range(1, 3)
                    ],
                }
                for item_group in range(1, 3)
            ],
        }
        for sub_menu in range(1, 5)
    ],
    style={'width': 256},
)
```

### 内置折叠状态控制

- 说明：使用导航菜单内置的折叠状态控制功能。

#### 代码
```python
fac.AntdMenu(
    defaultSelectedKey='图标antd-home',
    menuItems=[
        {
            'component': 'Item',
            'props': {
                'key': f'图标{icon}',
                'title': f'图标{icon}',
                'icon': icon,
            },
        }
        for icon in [
            'antd-home',
            'antd-cloud-upload',
            'antd-bar-chart',
            'antd-pie-chart',
            'antd-dot-chart',
            'antd-line-chart',
            'antd-apartment',
            'antd-app-store',
            'antd-app-store-add',
            'antd-bell',
            'antd-calculator',
            'antd-calendar',
            'antd-database',
            'antd-history',
            'fc-services',
            'fc-questions',
            'fc-organization',
        ]
    ],
    mode='inline',
    renderCollapsedButton=True,
    style={'maxWidth': 256},
)
```

### 配合侧边栏自定义控制折叠

- 说明：配合侧边栏组件**AntdSider**可实现针对导航菜单更灵活的折叠控制。

#### 代码
```python
fac.AntdLayout(
    [
        fac.AntdSider(
            [
                # 自定义折叠按钮
                fac.AntdButton(
                    id='menu-collapse-sider-custom-demo-trigger',
                    icon=fac.AntdIcon(
                        id='menu-collapse-sider-custom-demo-trigger-icon',
                        icon='antd-arrow-left',
                        style={'fontSize': '14px'},
                    ),
                    shape='circle',
                    type='text',
                    style={
                        'position': 'absolute',
                        'zIndex': 1,
                        'top': 25,
                        'right': -13,
                        'boxShadow': 'rgb(0 0 0 / 10%) 0px 4px 10px 0px',
                        'background': 'white',
                    },
                ),
                fac.AntdMenu(
                    menuItems=[
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'图标{icon}',
                                'title': f'图标{icon}',
                                'icon': icon,
                            },
                        }
                        for icon in [
                            'antd-home',
                            'antd-cloud-upload',
                            'antd-bar-chart',
                            'antd-pie-chart',
                            'antd-dot-chart',
                            'antd-line-chart',
                            'antd-apartment',
                            'antd-app-store',
                            'antd-app-store-add',
                            'antd-bell',
                            'antd-calculator',
                            'antd-calendar',
                            'antd-database',
                            'antd-history',
                        ]
                    ],
                    mode='inline',
                    style={'height': '100%', 'overflow': 'hidden auto'},
                ),
            ],
            id='menu-collapse-sider-custom-demo',
            collapsible=True,
            collapsedWidth=60,
            trigger=None,
            style={'position': 'relative'},
        ),
        fac.AntdContent(style={'background': '#f8f9fa'}),
    ],
    style={'height': 600},
)

...

app.clientside_callback(
    """(nClicks, collapsed) => {
        return [!collapsed, collapsed ? 'antd-arrow-left' : 'antd-arrow-right'];
    }""",
    [
        Output('menu-collapse-sider-custom-demo', 'collapsed'),
        Output('menu-collapse-sider-custom-demo-trigger-icon', 'icon'),
    ],
    Input('menu-collapse-sider-custom-demo-trigger', 'nClicks'),
    State('menu-collapse-sider-custom-demo', 'collapsed'),
    prevent_initial_call=True,
)
```

### 组件型菜单项

- 说明：配合参数`menuItemKeyToTitle`可以将指定的菜单项标题用组件元素代替。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'Item',
            'props': {
                'title': '常规菜单项',
                'key': '常规菜单项',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '带标签菜单项',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '带徽标菜单项',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '分离徽标菜单项',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '自定义图标',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '单独右对齐',
            },
        },
        {
            'component': 'Item',
            'props': {
                'key': '单独居中',
            },
        },
    ],
    menuItemKeyToTitle={
        '带标签菜单项': fac.AntdSpace(
            [
                '带标签菜单项',
                fac.AntdTag(content='我是标签', color='green'),
            ]
        ),
        '带徽标菜单项': fac.AntdBadge(
            '带徽标菜单项', count=66, offset=[15, 0]
        ),
        '分离徽标菜单项': fac.AntdRow(
            [
                fac.AntdCol('分离徽标菜单项'),
                fac.AntdCol(fac.AntdBadge(count=8, color='#1a73e8')),
            ],
            justify='space-between',
        ),
        '自定义图标': fac.AntdSpace(
            [
                *[
                    fac.AntdIcon(icon=icon)
                    for icon in [
                        'antd-build',
                        'antd-bug',
                        'antd-repair',
                        'antd-setting',
                    ]
                ],
                '自定义图标',
            ]
        ),
        '单独右对齐': html.Div(
            '单独右对齐', style={'textAlign': 'end'}
        ),
        '单独居中': html.Div('单独居中', style={'textAlign': 'center'}),
    },
    mode='inline',
    defaultSelectedKey='常规菜单项',
    style={'width': 220},
)
```

### 暗黑主题

- 说明：内置的暗黑主题风格。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'SubMenu',
            'props': {
                'key': f'{sub_menu}',
                'title': f'子菜单{sub_menu}',
            },
            'children': [
                {
                    'component': 'ItemGroup',
                    'props': {
                        'key': f'{sub_menu}-{item_group}',
                        'title': f'菜单项分组{sub_menu}-{item_group}',
                    },
                    'children': [
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'{sub_menu}-{item_group}-{item}',
                                'title': f'菜单项{sub_menu}-{item_group}-{item}',
                            },
                        }
                        for item in range(1, 3)
                    ],
                }
                for item_group in range(1, 3)
            ],
        }
        for sub_menu in range(1, 5)
    ],
    mode='inline',
    theme='dark',
    style={'width': 256},
)
```

### 设置默认展开项

- 说明：为导航菜单设置初始化时就处于展开状态的子菜单节点。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'SubMenu',
            'props': {
                'key': f'{sub_menu}',
                'title': f'子菜单{sub_menu}',
            },
            'children': [
                {
                    'component': 'ItemGroup',
                    'props': {
                        'key': f'{sub_menu}-{item_group}',
                        'title': f'菜单项分组{sub_menu}-{item_group}',
                    },
                    'children': [
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'{sub_menu}-{item_group}-{item}',
                                'title': f'菜单项{sub_menu}-{item_group}-{item}',
                            },
                        }
                        for item in range(1, 3)
                    ],
                }
                for item_group in range(1, 3)
            ],
        }
        for sub_menu in range(1, 5)
    ],
    mode='inline',
    defaultOpenKeys=['1', '3'],
    style={'width': 256},
)
```

### 设置默认选中项

- 说明：为导航菜单设置初始化时就处于选中状态的菜单项节点。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'SubMenu',
            'props': {
                'key': f'{sub_menu}',
                'title': f'子菜单{sub_menu}',
            },
            'children': [
                {
                    'component': 'ItemGroup',
                    'props': {
                        'key': f'{sub_menu}-{item_group}',
                        'title': f'菜单项分组{sub_menu}-{item_group}',
                    },
                    'children': [
                        {
                            'component': 'Item',
                            'props': {
                                'key': f'{sub_menu}-{item_group}-{item}',
                                'title': f'菜单项{sub_menu}-{item_group}-{item}',
                            },
                        }
                        for item in range(1, 3)
                    ],
                }
                for item_group in range(1, 3)
            ],
        }
        for sub_menu in range(1, 5)
    ],
    mode='inline',
    defaultOpenKeys=['1'],
    defaultSelectedKey='1-2-2',
    style={'width': 256},
)
```

### 自定义子菜单展开图标

- 说明：设置参数`expandIcon`自定义树节点的展开/折叠图标。

#### 代码
```python
[
    fac.Fragment(
        [
            fac.AntdDivider(
                f'mode="{mode}"',
                innerTextOrientation='left',
            ),
            fac.AntdMenu(
                menuItems=[
                    {
                        'component': 'SubMenu',
                        'props': {
                            'key': f'{sub_menu}',
                            'title': f'子菜单{sub_menu}',
                        },
                        'children': [
                            {
                                'component': 'ItemGroup',
                                'props': {
                                    'key': f'{sub_menu}-{item_group}',
                                    'title': f'菜单项分组{sub_menu}-{item_group}',
                                },
                                'children': [
                                    {
                                        'component': 'Item',
                                        'props': {
                                            'key': f'{sub_menu}-{item_group}-{item}',
                                            'title': f'菜单项{sub_menu}-{item_group}-{item}',
                                        },
                                    }
                                    for item in range(1, 3)
                                ],
                            }
                            for item_group in range(1, 3)
                        ],
                    }
                    for sub_menu in range(1, 5)
                ],
                mode=mode,
                expandIcon={
                    'expand': fac.AntdIcon(icon='antd-down-circle'),
                    'collapse': fac.AntdIcon(icon='antd-up-circle'),
                },
                style={'width': 256},
            ),
        ]
    )
    for mode in ['vertical', 'horizontal', 'inline']
]
```

### 调整子菜单缩进宽度

- 说明：子菜单逐级缩进的像素宽度可调整。

#### 代码
```python
fac.AntdMenu(
    menuItems=[
        {
            'component': 'SubMenu',
            'props': {'key': '子菜单1', 'title': '子菜单1'},
            'children': [
                {
                    'component': 'SubMenu',
                    'props': {
                        'key': '子菜单1-1',
                        'title': '子菜单1-1',
                    },
                    'children': [
                        {
                            'component': 'SubMenu',
                            'props': {
                                'key': '子菜单1-1-1',
                                'title': '子菜单1-1-1',
                            },
                            'children': [
                                {
                                    'component': 'Item',
                                    'props': {
                                        'key': '菜单项示例',
                                        'title': '菜单项示例',
                                    },
                                }
                            ],
                        }
                    ],
                }
            ],
        }
    ],
    defaultOpenKeys=['子菜单1', '子菜单1-1', '子菜单1-1-1'],
    mode='inline',
    inlineIndent=50,
    style={'width': 300},
)
```

### 显示模式

- 说明：导航菜单具有三种显示模式，其中`horizontal`模式会在宽度受限时自动呈现省略状态。

#### 代码
```python
[
    html.Div(
        [
            fac.AntdDivider(
                f'mode="{mode}"', innerTextOrientation='left'
            ),
            fac.AntdMenu(
                menuItems=[
                    {
                        'component': 'SubMenu',
                        'props': {
                            'key': f'{sub_menu}',
                            'title': f'子菜单{sub_menu}',
                        },
                        'children': [
                            {
                                'component': 'ItemGroup',
                                'props': {
                                    'key': f'{sub_menu}-{item_group}',
                                    'title': f'菜单项分组{sub_menu}-{item_group}',
                                },
                                'children': [
                                    {
                                        'component': 'Item',
                                        'props': {
                                            'key': f'{sub_menu}-{item_group}-{item}',
                                            'title': f'菜单项{sub_menu}-{item_group}-{item}',
                                        },
                                    }
                                    for item in range(1, 3)
                                ],
                            }
                            for item_group in range(1, 3)
                        ],
                    }
                    for sub_menu in range(1, 5)
                ],
                mode=mode,
                style={'width': 256},
            ),
        ]
    )
    for mode in ['vertical', 'horizontal', 'inline']
]
```

### 前缀图标

- 说明：为各菜单项快捷设置前缀图标。

#### 代码
```python
fac.AntdMenu(
    defaultSelectedKey='图标antd-home',
    menuItems=[
        {
            'component': 'Item',
            'props': {
                'key': f'图标{icon}',
                'title': f'图标{icon}',
                'icon': icon,
            },
        }
        for icon in [
            'antd-home',
            'antd-cloud-upload',
            'antd-bar-chart',
            'antd-pie-chart',
            'antd-dot-chart',
            'antd-line-chart',
            'antd-apartment',
            'antd-app-store',
            'antd-app-store-add',
            'antd-bell',
            'antd-calculator',
            'antd-calendar',
            'antd-database',
            'antd-history',
            'fc-services',
            'fc-questions',
            'fc-organization',
        ]
    ],
    mode='inline',
    style={'width': 256},
)
```

### 控制子菜单展开触发行为

- 说明：设置参数`triggerSubMenuAction='click'`控制子菜单展开触发行为为“点击”。

#### 代码
```python
[
    fac.Fragment(
        [
            fac.AntdDivider(
                f'mode="{mode}"',
                innerTextOrientation='left',
            ),
            fac.AntdMenu(
                menuItems=[
                    {
                        'component': 'SubMenu',
                        'props': {
                            'key': f'{sub_menu}',
                            'title': f'子菜单{sub_menu}',
                        },
                        'children': [
                            {
                                'component': 'ItemGroup',
                                'props': {
                                    'key': f'{sub_menu}-{item_group}',
                                    'title': f'菜单项分组{sub_menu}-{item_group}',
                                },
                                'children': [
                                    {
                                        'component': 'Item',
                                        'props': {
                                            'key': f'{sub_menu}-{item_group}-{item}',
                                            'title': f'菜单项{sub_menu}-{item_group}-{item}',
                                        },
                                    }
                                    for item in range(1, 3)
                                ],
                            }
                            for item_group in range(1, 3)
                        ],
                    }
                    for sub_menu in range(1, 5)
                ],
                mode=mode,
                expandIcon={
                    'expand': fac.AntdIcon(icon='antd-down-circle'),
                    'collapse': fac.AntdIcon(icon='antd-up-circle'),
                },
                style={'width': 256},
            ),
        ]
    )
    for mode in ['vertical', 'horizontal', 'inline']
]
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- currentItem (dict; optional):
    Monitor the information of the currently selected menu item.

- currentItemPath (list; optional):
    Monitor the path information of the currently selected menu item.

- currentKey (string; optional):
    Monitor or set the key value of the currently selected menu item.

- currentKeyPath (list; optional):
    Monitor the key value path information of the currently selected menu item.

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- defaultOpenKeys (list of strings; optional):
    The key values of the menu items that are expanded by default.

- defaultSelectedKey (string; optional)

- expandIcon (dict; optional):
    Custom expansion icon, it is recommended to use a dictionary type only when `mode='inline'`.

    `expandIcon` is a list of or a singular dash component, string or number | dict with keys:

    - collapse (a list of or a singular dash component, string or number; optional):
        The icon for collapsing.

    - expand (a list of or a singular dash component, string or number; optional):
        The icon for expanding.

- inlineCollapsed (boolean; default False):
    Whether the current menu is collapsed, only effective in inline mode. Default value: `False`.

- inlineIndent (number; default 24):
    The pixel indentation width of the submenu relative to the upper level in inline mode. Default value: `24`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the current component.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- menuItemKeyToTitle (dict with strings as keys and values of type a list of or a singular dash component, string or number; optional):
    Define component-type menu item titles for specified nodes, with a higher priority than the title attribute of the corresponding node in `menuItems`.

- menuItems (list; optional):
    The data structure of the navigation menu.

- mode (a value equal to: 'vertical', 'horizontal', 'inline'; default 'vertical'):
    The display mode, with options `vertical`, `horizontal`, `inline`. Default value: `vertical`.

- onlyExpandCurrentSubMenu (boolean; default False):
    Whether to only expand the parent menu of the currently selected item. Default value: `False`.

- openKeys (list of strings; optional):
    Monitor or set the key values of the currently expanded submenu items.

- persisted_props (list of a value equal to: 'currentKey', 'openKeys's; default ['currentKey', 'openKeys']):
    An array of property values that are enabled for persistence in the current component, with options `currentKey`, `openKeys`.
    Default value: `['currentKey', 'openKeys']`.

- persistence (boolean | string | number; optional):
    Whether to enable persistence for the current component.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The type of persistent storage for the properties of the current component. Default value: `local`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    The anchoring strategy for the menu expansion layer, with options `parent`, `body`. Default value: `body`.

- renderCollapsedButton (boolean; default False):
    Whether to render the menu collapse state control button. Default value: `False`.

- style (dict; optional):
    The CSS style of the current component.

- theme (a value equal to: 'light', 'dark'; default 'light'):
    The theme, with options `light`, `dark`. Default value: `light`.

- triggerSubMenuAction (a value equal to: 'hover', 'click'; default 'hover'):
    The trigger behavior for the `SubMenu` to expand/close, with options `hover`, `click`, which is invalid when `mode='inline'`.
    Default value: `hover`.


## 补充 API 说明

In the default mode, the `menuItems` parameter is freely nested through the `children` field to construct any tree-shaped menu structure. The legal parameters for each node are described as follows:

- component (options include: 'Item', 'SubMenu', 'ItemGroup', 'Divider'; required):

  The type of the current menu node. Options include `'Item'` (menu item), `'SubMenu'` (submenu), `'ItemGroup'` (menu item group), and `'Divider'` (divider line).

- props (dict; optional):

  Configure the attribute values related to the current node.

  - key (string; required):

    The unique identifier for the current node.

  - title (string; optional):

    The title of the current node.

  - disabled (boolean; default False):

    Whether the current node is disabled.

  - danger (boolean; default False):

    Whether the current node is displayed in a danger state.

  - href (string; optional):

    The link address for the current node.

  - icon (string; optional):

    The type of prefix icon for the current node. When `iconRenderer` is `'AntdIcon'`, it corresponds to the same parameter in `AntdIcon`. When `iconRenderer` is `'fontawesome'`, it is the CSS class name.

  - iconRenderer (options include: 'AntdIcon', 'fontawesome'; optional):

    The rendering method for the prefix icon of the current node. Options include `'AntdIcon'` and `'fontawesome'`.

  - dashed (boolean; default False):

    If the current node is a divider, set whether to display it as a dashed line.

  - name (string; optional):

    A unique auxiliary identifier for the current node.
