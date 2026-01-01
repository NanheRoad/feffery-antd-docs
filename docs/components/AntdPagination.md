# AntdPagination

## 简介源码：`views/AntdPagination/intro.py`
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
                {'title': translator.t('AntdPagination 分页')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdPagination 分页'), level=2),
        fac.AntdParagraph(
            translator.t('采用分页的形式分隔长列表，每次只加载单页内容。')
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 添加更多功能

- 说明：设置快速跳页、每页记录数选择器、前后缀信息等功能。

#### 代码
```python
fac.AntdPagination(
    defaultPageSize=10,
    total=100,
    showQuickJumper=True,
    showSizeChanger=False,
    showTotalPrefix='总记录数：',
    showTotalSuffix='条！🧐'
)
```

### 对齐方式

- 说明：设置参数`align`控制分页控件对齐方式。

#### 代码
```python
[
    fac.AntdDivider("align='start'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='start'),
    fac.AntdDivider("align='center'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='center'),
    fac.AntdDivider("align='end'"),
    fac.AntdPagination(defaultPageSize=10, total=100, align='end'),
]
```

### 单页自动隐藏

- 说明：设置参数`hideOnSinglePage=True`，仅有1页时自动隐藏分页组件。

#### 代码
```python
[
    fac.AntdDivider(
        '默认hideOnSinglePage=False', innerTextOrientation='left'
    ),
    fac.AntdPagination(total=10, pageSize=20),
    fac.AntdDivider(
        'hideOnSinglePage=True', innerTextOrientation='left'
    ),
    fac.AntdPagination(total=10, pageSize=20, hideOnSinglePage=True),
]
```

### 回调监听

- 说明：可用于监听分页相关事件。

#### 代码
```python
[
    fac.AntdSpace(id='pagination-demo-output', direction='vertical'),
    fac.AntdPagination(
        id='pagination-demo',
        defaultPageSize=10,
        total=100,
        pageSizeOptions=[5, 10, 20],
        showSizeChanger=True,
    ),
]

...

@app.callback(
    Output('pagination-demo-output', 'children'),
    [Input('pagination-demo', 'current'),
     Input('pagination-demo', 'pageSize')]
)
def pagination_callback_demo(current, pageSize):

    return [
        fac.AntdText(f'内容项{i}')
        for i in range((current - 1) * pageSize, current * pageSize)
    ]
```

### 基础使用

- 说明：最基础的分页。

#### 代码
```python
fac.AntdPagination(defaultPageSize=10, total=100)
```

### 极简模式

- 说明：设置参数`simple=True`开启极简模式。

#### 代码
```python
fac.AntdPagination(
    defaultPageSize=10, total=100, simple=True, showTotal=False
)
```

### 迷你模式

- 说明：设置参数`size='small'`开启迷你模式。

#### 代码
```python
fac.AntdPagination(
    defaultPageSize=10, total=100, size='small'
)
```

### 展示较少的跳页按钮

- 说明：设置参数`showLessItems=True`时会展示较少的跳页按钮。

#### 代码
```python
[
    fac.AntdDivider(
        'showLessItems=False（默认）', innerTextOrientation='left'
    ),
    fac.AntdPagination(defaultPageSize=10, total=100, current=5),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdPagination(
        defaultPageSize=10, total=100, showLessItems=True, current=5
    ),
]
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- align (a value equal to: 'start', 'center', 'end'; default 'start'):
    Component alignment specification, with options `start`, `center`, `end`. Default value: `start`.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- batchPropsNames (list of strings; optional):
    List of property names to be included in batch property listening. Default value: `[]`.

- batchPropsValues (dict; optional):
    Batch listening for property values corresponding to the current batchPropsNames.

- className (string | dict; optional):
    Current component CSS class name, supporting [dynamic CSS](/advanced-classname).

- current (number; optional):
    Listening to or setting the current page number.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- defaultCurrent (number; default 1):
    The current page number upon initialization. Default value: `1`.

- defaultPageSize (number; default 10):
    The number of items per page upon initialization. Default value: `10`.

- disabled (boolean; default False):
    Whether to disable the functionality of the current component. Default value: `False`.

- hideOnSinglePage (boolean; default False):
    Whether to hide the pager when there is only one page. Default value: `False`.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the current component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    Component text language, with options `zh-cn` (Simplified Chinese), `en-us` (English), `de-de` (German).
    Default value: `zh-cn`.

- pageSize (number; optional):
    Listening to or setting the number of items per page.

- pageSizeOptions (list of numbers; optional):
    Options for switching the number of items per page.

- persisted_props (list of a value equal to: 'current', 'pageSize's; default ['current', 'pageSize']):
    Array of property values enabled for persistence in the current component, with options `current`, `pageSize`. Default value: `['current', 'pageSize']`.

- persistence (boolean | string | number; optional):
    Whether to enable persistence for the current component.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The type of persistent storage for the current component's properties. Default value: `local`.

- showLessItems (boolean; default False):
    Whether to display fewer page jump buttons. Default value: `False`.

- showQuickJumper (boolean; default False):
    Whether to render a quick page jump control. Default value: `False`.

- showSizeChanger (boolean; default False):
    Whether to render a page size switcher. Default value: `False`.

- showTotal (boolean; default True):
    Whether to render a description of the total number of records. Default value: `True`.

- showTotalPrefix (string; optional):
    Prefix content for the total number of records description.

- showTotalSuffix (string; optional):
    Suffix content for the total number of records description.

- simple (boolean; default False):
    Whether to enable simple mode. Default value: `False`.

- size (a value equal to: 'default', 'small'; default 'default'):
    Component size specification, with options `default`, `small`. Default value: `default`.

- style (dict; optional):
    CSS styles for the current component.

- total (number; optional):
    Total number of records.
