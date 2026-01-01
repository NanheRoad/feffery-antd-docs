# AntdCheckbox

## 简介源码：`views/AntdCheckbox/intro.py`
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
                {'title': translator.t('AntdCheckbox 选择框')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCheckbox 选择框'), level=2),
        fac.AntdParagraph(translator.t('用于在两种状态之间进行切换。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCheckbox(id='checkbox-demo', label='开启'),
        fac.AntdText(id='checkbox-demo-output'),
    ]
)

...

@app.callback(
    Output('checkbox-demo-output', 'children'),
    Input('checkbox-demo', 'checked'),
)
def checkbox_demo(checked):
    return f'checked: {checked}'
```

### 基础使用

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCheckbox(label='选择框1'),
        fac.AntdCheckbox(label='选择框2', checked=True),
    ]
)
```

### 禁用状态

- 说明：None

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCheckbox(label='选择框', disabled=True),
        fac.AntdCheckbox(label='选择框', checked=True, disabled=True),
        fac.AntdCheckbox(label='选择框', indeterminate=True, disabled=True),
    ]
)
```

### 半选中状态

- 说明：开启半选中状态后，仅改变勾选框显示样式，与实际勾选状态无关。

#### 代码
```python
fac.AntdCheckbox(label='选择框', indeterminate=True)
```

### 只读状态

- 说明：只读状态适用于单纯的数据展示场景。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCheckbox(label='选择框', readOnly=True),
        fac.AntdCheckbox(label='选择框', checked=True, readOnly=True),
        fac.AntdCheckbox(label='选择框', indeterminate=True, readOnly=True),
    ]
)
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- style (dict; optional):
    CSS styles for the current component.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- name (string; optional):
    Used in conjunction with the `AntdForm` form for batch value collection/control, serving as the field name for the current form item, with `id` as the default value.

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- label (a list of or a singular dash component, string or number; optional):
    Component type, label content.

- autoFocus (boolean; default False):
    Whether to automatically gain focus. Default value: `False`.

- checked (boolean; default False):
    To monitor or set whether the current checkbox is checked. Default value: `False`.

- indeterminate (boolean; default False):
    Whether to force rendering in an indeterminate state, which only affects the style and is unrelated to the checked state. Default value: `False`.

- readOnly (boolean; default False):
    Whether to render in read-only state. Default value: `False`.

- batchPropsNames (list of strings; optional):
    A list of property names to be included in [batch property monitoring](/batch-props-values).

- batchPropsValues (dict; optional):
    Monitor the values of several properties specified in `batchPropsNames`.

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

- persisted_props (list of a value equal to: 'checked's; default ['checked']):
    A list of property names for the enabled property persistence feature, with the option of `'checked'`. Default value: `['checked']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    The type of property persistence storage, with options of `'local'` (local persistence), `'session'` (session persistence), `'memory'` (memory persistence).
    Default value: `'local'`.
