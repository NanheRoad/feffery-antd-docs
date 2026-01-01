# AntdAccordion

## 简介源码：`views/AntdAccordion/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {"title": translator.t("组件介绍")},
                {"title": translator.t("数据展示")},
                {"title": translator.t("AntdAccordion 手风琴")},
            ],
            style={"marginBottom": 8},
        ),
        fac.AntdTitle(translator.t("AntdAccordion 手风琴"), level=2),
        fac.AntdParagraph(translator.t("展示一组同级内容的特殊形式。")),
    ]

```

## 示例代码片段（仅保留演示内容）

### 关闭手风琴模式

- 说明：设置参数`accordion=False`关闭手风琴模式。

#### 代码
```python
fac.AntdAccordion(
    items=[
        {
            'title': f'手风琴项示例{i}',
            'key': i,
            'children': fac.AntdText(f'手风琴项示例{i}'),
        }
        for i in range(1, 6)
    ],
    accordion=False,
)
```

### 回调监听

- 说明：None

#### 代码
```python
[
    fac.AntdAccordion(
        id='accordion-demo',
        items=[
            {
                'title': f'手风琴项示例{i}',
                'key': i,
                'children': fac.AntdText(f'手风琴项示例{i}'),
            }
            for i in range(1, 6)
        ],
        defaultActiveKey=['2'],
    ),
    fac.AntdParagraph(id='accordion-demo-output'),
]

...

@app.callback(
    Output('accordion-demo-output', 'children'),
    Input('accordion-demo', 'activeKey'),
)
def accordion_demo(activeKey):
    return f'activeKey: {activeKey}'
```

### 基础使用

- 说明：默认的手风琴模式下，最多只能展开一个面板。

#### 代码
```python
fac.AntdAccordion(
    items=[
        {
            'title': f'手风琴项示例{i}',
            'key': i,
            'children': fac.AntdText(f'手风琴项示例{i}'),
        }
        for i in range(1, 6)
    ]
)
```

### 设置默认展开项

- 说明：设置参数`defaultActiveKey`控制默认展开项。

#### 代码
```python
[
    fac.AntdDivider('手风琴模式开', innerTextOrientation='left'),
    fac.AntdAccordion(
        items=[
            {
                'title': f'手风琴项示例{i}',
                'key': i,
                'children': fac.AntdText(f'手风琴项示例{i}'),
            }
            for i in range(1, 6)
        ],
        defaultActiveKey=['3'],
    ),
    fac.AntdDivider('手风琴模式关', innerTextOrientation='left'),
    fac.AntdAccordion(
        items=[
            {
                'title': f'手风琴项示例{i}',
                'key': i,
                'children': fac.AntdText(f'手风琴项示例{i}'),
            }
            for i in range(1, 6)
        ],
        defaultActiveKey=['1', '3', '4'],
        accordion=False,
    ),
]
```

### 展开图标靠右

- 说明：设置参数`expandIconPosition='right'`控制展开图标靠右。

#### 代码
```python
fac.AntdAccordion(
    items=[
        {
            'title': f'手风琴项示例{i}',
            'key': i,
            'children': fac.AntdText(f'手风琴项示例{i}'),
        }
        for i in range(1, 6)
    ],
    expandIconPosition='right',
)
```

### 子项额外内容

- 说明：为子项设置参数`extra`添加额外内容。

#### 代码
```python
fac.AntdAccordion(
    items=[
        {
            'title': f'手风琴项示例{i}',
            'key': i,
            'children': fac.AntdText(f'手风琴项示例{i}'),
            'extra': fac.AntdButton('额外内容', type='link', size='small'),
        }
        for i in range(1, 6)
    ],
    collapsible='header',
)
```

### 透明面板模式

- 说明：设置参数`ghost=True`开启透明面板格式。

#### 代码
```python
fac.AntdAccordion(
    items=[
        {
            'title': f'手风琴项示例{i}',
            'key': i,
            'children': fac.AntdText(f'手风琴项示例{i}'),
        }
        for i in range(1, 6)
    ],
    ghost=True,
)
```

### 不同的尺寸规格

- 说明：设置参数`size`控制尺寸规格。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAccordion(
            items=[
                {
                    'title': f'{size}手风琴项示例{i}',
                    'key': i,
                    'children': fac.AntdText(f'{size}手风琴项示例{i}'),
                }
                for i in range(1, 3)
            ],
            size=size,
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明

- id (string; optional):
  Component unique id.

- key (string; optional):
  Update the `key` value of the current component to force a re-render of the component.

- className (string | dict; optional):
  CSS class name of the current component, supports [dynamic css](/advanced-classname).

- styles (dict; optional):
  Fine-grained control of child element CSS styles.

  `styles` is a dict with keys:

  - header (dict; optional):
    CSS styles for the header element.

  - body (dict; optional):
    CSS styles for the body element.

- classNames (dict; optional):
  Fine-grained control of child element CSS class names.

  `classNames` is a dict with keys:

  - header (string; optional):
    CSS class name for the header element.

  - body (string; optional):
    CSS class name for the body element.

- items (list of dicts; optional):
  Define accordion sub-items.

  `items` is a list of dicts with keys:

  - children (a list of or a singular dash component, string or number; optional):
    Inner elements of the current sub-item.

  - className (string | dict; optional):
    CSS class name of the current sub-item, supports [dynamic css](/advanced-classname).

  - style (dict; optional):
    CSS styles of the current sub-item.

  - key (string | number; required):
    Required, unique key value of the current sub-item.

  - collapsible (a value equal to: 'header', 'disabled', 'icon'; optional):
    Collapse trigger method of the current sub-item. Options are `'header'`, `'disabled'`, `'icon'`.

  - title (a list of or a singular dash component, string or number; optional):
    Title element of the current sub-item.

  - extra (a list of or a singular dash component, string or number; optional):
    Extra element at the top right corner of the current sub-item.

  - showArrow (boolean; optional):
    Whether to display the arrow icon of the current accordion item. Default: `True`.

  - forceRender (boolean; optional):
    Whether to force render inner elements. Default: `False`.

- accordion (boolean; default True):
  Whether to enable accordion mode. Default: `True`.

- activeKey (string | list of strings | number | list of numbers; optional):
  Listen to or set the key value of the accordion item currently expanded.

- defaultActiveKey (string | list of strings | number | list of numbers; optional):
  Set the key value of the accordion item initially expanded.

- bordered (boolean; default True):
  Whether to render borders. Default: `True`.

- size (a value equal to: 'large', 'middle', 'small'; default 'middle'):
  Component size specification. Options are `'small'`, `'middle'`, `'large'`. Default: `'middle'`.

- collapsible (a value equal to: 'header', 'disabled', 'icon'; optional):
  Set the collapse trigger method for all sub-items. Options are `'header'`, `'disabled'`, `'icon'`.

- expandIconPosition (a value equal to: 'left', 'right'; default 'left'):
  Set the position of the collapse icon. Options are `'left'`, `'right'`.

- ghost (boolean; default False):
  Whether to enable transparent borderless mode. Default: `False`.

- data-_ (string; optional):
  Wildcard attributes in `data-_` format.

- aria-_ (string; optional):
  Wildcard attributes in `aria-_` format.
