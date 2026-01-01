# AntdCheckCardGroup

## 简介源码：`views/AntdCheckCardGroup/intro.py`
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
                {'title': translator.t('数据录入')},
                {'title': translator.t('AntdCheckCardGroup 组合选择卡片')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCheckCardGroup 组合选择卡片'), level=2),
        fac.AntdParagraph(translator.t('用于监听一组选择卡片的选择情况。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 限制必须有选中值

- 说明：设置`allowNoValue=False`后，将会阻止用户对唯一选中值的取消选择行为。

#### 代码
```python
[
    fac.AntdDivider('单选', innerTextOrientation='left'),
    fac.AntdCheckCardGroup(
        [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
        defaultValue=3,
        allowNoValue=False,
    ),
    fac.AntdDivider('多选', innerTextOrientation='left'),
    fac.AntdCheckCardGroup(
        [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
        defaultValue=[3],
        multiple=True,
        allowNoValue=False,
    ),
]
```

### 回调监听

- 说明：通过回调监听已选中卡片对应值。

#### 代码
```python
[
    fac.AntdCheckCardGroup(
        [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
        id='check-card-group-demo',
        size='small',
        multiple=True,
        defaultValue=[1, 2],
    ),
    fac.AntdParagraph(id='check-card-group-demo-output'),
]

...

@app.callback(
    Output('check-card-group-demo-output', 'children'),
    Input('check-card-group-demo', 'value'),
)
def check_card_group_demo(value):
    return f'value: {value}'
```

### 基础使用

- 说明：None

#### 代码
```python
fac.AntdCheckCardGroup(
    [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
    defaultValue=3,
)
```

### 自定义选项样式

- 说明：None

#### 代码
```python
[
    fuc.FefferyStyle(
        rawStyle="""
.check-card-group-custom-style-demo .ant-pro-checkcard-content {
    padding: 5px 12px;
}
"""
    ),
    fac.AntdCheckCardGroup(
        [
            fac.AntdCheckCard(
                f'选项{i}',
                value=i,
                style={
                    'width': 'auto',
                    'marginRight': 3,
                    'marginBottom': 3,
                    'borderRadius': 5,
                },
            )
            for i in range(1, 26)
        ],
        className='check-card-group-custom-style-demo',
        defaultValue=[4, 8, 9, 15],
        multiple=True,
    ),
]
```

### 禁用状态

- 说明：None

#### 代码
```python
fac.AntdCheckCardGroup(
    [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
    defaultValue=3,
    disabled=True,
)
```

### 多选模式

- 说明：None

#### 代码
```python
fac.AntdCheckCardGroup(
    [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
    defaultValue=[2, 3, 4],
    multiple=True,
)
```

### 只读状态

- 说明：只读状态适用于单纯的数据展示场景。

#### 代码
```python
fac.AntdCheckCardGroup(
    [fac.AntdCheckCard(f'选项{i}', value=i) for i in range(1, 6)],
    defaultValue=3,
    readOnly=True,
)
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Updates the `key` value of the current component to force a redraw.

- children (a list of or a singular dash component, string or number; optional):
    Component type, containing several `AntdCheckCard` related components.

- style (dict; optional):
    CSS styles for the current component.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- name (string; optional):
    Used in conjunction with the `AntdForm` form for batch value collection and control, serving as the field name for the current form item, with `id` as the default value.

- multiple (boolean; default False):
    Whether to enable multiple selection. Default value: `False`.

- allowNoValue (boolean; default True):
    Whether to allow the last option in the current group of selection cards to be deselected. Default value: `True`.

- bordered (boolean; default True):
    Whether to display a border. Default value: `True`.

- value (number | string | list of number | strings; optional):
    Listens to or sets the value of the selected card(s).

- defaultValue (number | string | list of number | strings; optional):
    Initializes the value of the selected card(s).

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- size (a value equal to: 'small', 'default', 'large'; default 'default'):
    The size specification of the current component, with options `'small'`, `'default'`, `'large'`. Default value: `'default'`.

- readOnly (boolean; default False):
    Whether to render as read-only. Default value: `False`.

- data-* (string; optional):
    Wildcard for `data-*` format attributes.

- aria-* (string; optional):
    Wildcard for `aria-*` format attributes.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

- persistence (boolean | string | number; optional):
    Whether to enable [property persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; default ['value']):
    The names of several properties that are enabled for property persistence, with the option `'value'`. Default value: `['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The storage type for property persistence, with options `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence).
    Default value: `'local'`.
