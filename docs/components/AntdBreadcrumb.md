# AntdBreadcrumb

## 简介源码：`views/AntdBreadcrumb/intro.py`
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
                {'title': translator.t('AntdBreadcrumb 面包屑')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdBreadcrumb 面包屑'), level=2),
        fac.AntdParagraph(
            translator.t('用于展示当前页面在系统层级结构中的位置。')
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 添加链接跳转功能

- 说明：设置参数`href`添加链接跳转功能。

#### 代码
```python
fac.AntdBreadcrumb(
    items=[
        {
            'title': 'awesome-feffery-dash仓库主页',
            'href': 'https://github.com/CNFeffery/awesome-feffery-dash',
            'target': '_blank',
        },
        {
            'title': 'feffery-antd-components文档首页',
            'href': '/',
            'target': '_blank',
        },
        {
            'title': 'AntdBreadcrumb文档页',
            'href': '/AntdBreadcrumb',
            'target': '_blank',
        },
    ]
)
```

### 回调监听

- 说明：通过`clickedItem`进行面包屑节点点击事件的监听。

#### 代码
```python
[
    fac.AntdBreadcrumb(
        id='breadcrumnb-demo',
        items=[
            {'title': '首页', 'key': '首页'},
            {'title': '下属页面1', 'key': '下属页面1'},
            {
                'title': '下属页面1-1',
                'key': '下属页面1-1',
                'menuItems': [
                    {
                        'key': '菜单项节点1',
                        'title': '菜单项节点1',
                    },
                    {
                        'key': '菜单项节点2',
                        'title': '菜单项节点2',
                    },
                ],
            },
        ],
    ),
    html.Pre(id='breadcrumnb-demo-output'),
]

...

import json

...

@app.callback(
    Output('breadcrumnb-demo-output', 'children'),
    Input('breadcrumnb-demo', 'clickedItem'),
    prevent_initial_call=True
)
def breadcrumb_callback_demo(clickedItem):

    return json.dumps(
        dict(clickedItem=clickedItem),
        indent=4,
        ensure_ascii=False
    )
```

### 基础使用

- 说明：最基础的面包屑。

#### 代码
```python
fac.AntdBreadcrumb(
    items=[
        {'title': '首页'},
        {'title': '下属页面1'},
        {'title': '下属页面1-1'},
    ]
)
```

### 节点添加悬浮菜单

- 说明：在面包屑的节点添加悬浮菜单。

#### 代码
```python
fac.AntdBreadcrumb(
    items=[
        {
            'title': 'awesome-feffery-dash仓库主页',
            'href': 'https://github.com/CNFeffery/awesome-feffery-dash',
            'target': '_blank',
            'menuItems': [
                {
                    'title': 'feffery-utils-components',
                    'href': 'https://github.com/CNFeffery/feffery-utils-components',
                    'target': '_blank',
                },
                {
                    'title': 'feffery-antd-charts',
                    'href': 'https://github.com/CNFeffery/feffery-antd-charts',
                    'target': '_blank',
                },
                {
                    'title': 'feffery-markdown-components',
                    'href': 'https://github.com/CNFeffery/feffery-markdown-components',
                    'target': '_blank',
                },
            ],
        },
        {
            'title': 'feffery-antd-components文档首页',
            'href': '/',
            'target': '_blank',
        },
        {
            'title': 'AntdBreadcrumb文档页',
            'href': '/AntdBreadcrumb',
            'target': '_blank',
        },
    ]
)
```

### 添加前缀图标

- 说明：通过参数`icon`，可基于图标代号直接使用**AntdIcon**中的各种图标作为节点的前缀图标。

#### 代码
```python
fac.AntdBreadcrumb(
    items=[
        {
            'title': 'awesome-feffery-dash仓库主页',
            'href': 'https://github.com/CNFeffery/awesome-feffery-dash',
            'target': '_blank',
            'icon': 'antd-github',
        },
        {
            'title': 'feffery-antd-components文档首页',
            'href': '/',
            'target': '_blank',
            'icon': 'antd-home',
        },
        {
            'title': 'AntdBreadcrumb文档页',
            'href': '/AntdBreadcrumb',
            'target': '_blank',
            'icon': 'fc-approval',
        },
    ]
)
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for `aria-*` formatted attributes.

- className (string | dict; optional):
    The CSS class name for the current component, supporting [dynamic CSS](/advanced-classname).

- clickedItem (dict; optional):
    Listens for breadcrumb node click events.

    `clickedItem` is a dictionary with keys:

    - itemKey (string; optional):
        The key value of the clicked node.

    - itemTitle (string; optional):
        The title of the clicked node.

    - timestamp (number; optional):
        The timestamp of the click event.

- data-* (string; optional):
    Wildcard for `data-*` formatted attributes.

- items (list of dicts; optional):
    The data structure for breadcrumb nodes.

    `items` is a list of dictionaries with keys:

    - href (string; optional):
        The link address of the node.

    - icon (string; optional):
        The name of the prefix icon for the node, associated with the `iconRenderer` method. Under the `'AntdIcon'` method, it is the same as the icon parameter of AntdIcon, and under the `'fontawesome'` method, it represents the CSS class name of the icon.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
        The rendering method for the prefix icon, with options `'AntdIcon'`, `'fontawesome'`. Default value: `'AntdIcon'`.

    - key (string; optional):
        The unique key value for the node.

    - menuItems (list of dicts; optional):
        The data structure required to set up a dropdown menu for the current node.

        `menuItems` is a list of dictionaries with keys:

        - disabled (boolean; optional):
            Whether to disable the current dropdown menu node.

        - href (string; optional):
            The link address of the dropdown menu node.

        - icon (string; optional):
            The name of the prefix icon for the dropdown menu node, associated with the `iconRenderer` method. Under the `'AntdIcon'` method, it is the same as the icon parameter of AntdIcon, and under the `'fontawesome'` method, it represents the CSS class name of the icon.

        - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
            The rendering method for the prefix icon, with options `'AntdIcon'`, `'fontawesome'`. Default value: `'AntdIcon'`.

        - target (string; optional):
            The link behavior for the dropdown menu node.

        - title (string; optional):
            The title of the dropdown menu node.

    - target (string; optional):
        The link behavior for the node.

    - title (string; optional):
        The title of the node.

- key (string; optional):
    Updating the `key` value of the current component can force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- separator (a list of or a singular dash component, string or number; default '/'):
    Component type, separator. Default value: `'/'`.

- style (dict; optional):
    The CSS styles for the current component.
