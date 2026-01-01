# AntdCompact

## 简介源码：`views/AntdCompact/intro.py`
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
                {'title': translator.t('布局')},
                {'title': translator.t('AntdCompact 紧凑排列')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdCompact 紧凑排列'), level=2),
        fac.AntdParagraph(
            translator.t(
                '用于对若干内部组件进行紧凑排列，并为相邻组件之间自动合并边框。'
            )
        ),
        fac.AntdParagraph(
            translator.t(
                '注：目前支持进行紧凑布局的组件有AntdButton、AntdCascader、AntdDatePicker、AntdInput、AntdSelect、AntdTimePicker、AntdTreeSelect'
            ),
            type='secondary',
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：基于**AntdCompact**对子元素进行排列，可以实现相邻紧贴元素边框线合并效果。

#### 代码
```python
[
    fac.AntdDivider('基于AntdSpace', innerTextOrientation='left'),
    fac.AntdSpace(
        [fac.AntdButton(f'按钮{i}') for i in range(1, 6)], size=0
    ),
    fac.AntdDivider('基于AntdCompact', innerTextOrientation='left'),
    fac.AntdCompact([fac.AntdButton(f'按钮{i}') for i in range(1, 6)]),
]
```

### 经典用法

- 说明：输入框搭配其他控件是紧凑排列经典使用场景。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCompact(
            [
                fac.AntdInput(placeholder='请输入', style={'width': 150}),
                fac.AntdSelect(
                    options=[
                        {
                            'label': f'选项{i}',
                            'value': f'选项{i}',
                        }
                        for i in range(1, 4)
                    ],
                    defaultValue='选项1',
                    style={'width': 80},
                ),
            ]
        ),
        fac.AntdCompact(
            [
                fac.AntdInput(
                    placeholder='请输入', style={'width': '100%'}
                ),
                fac.AntdSelect(
                    options=[
                        {
                            'label': f'选项{i}',
                            'value': f'选项{i}',
                        }
                        for i in range(1, 4)
                    ],
                    defaultValue='选项1',
                    style={'width': 80},
                ),
            ],
            style={'width': '100%'},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
    Component type, embedded elements.

- id (string; optional):
    Unique ID for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- block (boolean; default False):
    Whether to render as a block-level element (width fills the parent container) Default value: `False`.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS class names](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- direction (a value equal to: 'vertical', 'horizontal'; default 'horizontal'):
    Direction of arrangement, options include `'vertical'`, `'horizontal'`. Default value: `'horizontal'`.

- key (string; optional):
    Updates the `key` value for the current component, which can force a redraw of the current component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is currently loading.

    - prop_name (string; optional):
        Holds which property is being loaded.

- style (dict; optional):
    The CSS styles for the current component.
