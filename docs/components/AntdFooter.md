# AntdFooter

## 简介源码：`views/AntdFooter/intro.py`
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
                {'title': translator.t('经典布局')},
                {'title': translator.t('AntdFooter 页尾')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdFooter 页尾'), level=2),
        fac.AntdParagraph(translator.t('用于在经典布局方案中构建页尾部分。')),
    ]

```

## API 参数说明

- children (a list of or a singular dash component, string or number; optional):
    Component type for embedded elements.

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    CSS class name for the current component, supporting [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- key (string; optional):
    Updates the `key` value of the current component to force a re-render.

- loading_state (dict; optional):
    The `loading_state` is a dictionary with the following keys:
    - component_name (string; optional):
        Holds the name of the component that is loading.
    - is_loading (boolean; optional):
        Determines whether the component is currently loading.
    - prop_name (string; optional):
        Indicates which property is currently loading.

- style (dict; optional):
    CSS styles for the current component.
