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

## 示例源码（demos）

### `views/AntdAccordion/demos/accordion_off.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"手风琴项示例{i}",
                    "key": i,
                    "children": fac.AntdText(f"手风琴项示例{i}"),
                }
                for i in range(1, 6)
            ],
            accordion=False,
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"Accordion item example {i}",
                    "key": i,
                    "children": fac.AntdText(f"Accordion item example {i}"),
                }
                for i in range(1, 6)
            ],
            accordion=False,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdAccordion(
    items=[
        {
            'title': f'Accordion item example {i}',
            'key': i,
            'children': fac.AntdText(f'Accordion item example {i}'),
        }
        for i in range(1, 6)
    ],
    accordion=False,
)
"""
            }
        ]

```

### `views/AntdAccordion/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = [
            fac.AntdAccordion(
                id="accordion-demo",
                items=[
                    {
                        "title": f"手风琴项示例{i}",
                        "key": i,
                        "children": fac.AntdText(f"手风琴项示例{i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["2"],
            ),
            fac.AntdParagraph(id="accordion-demo-output"),
        ]

    elif current_locale == "en-us":
        demo_contents = [
            fac.AntdAccordion(
                id="accordion-demo",
                items=[
                    {
                        "title": f"Accordion item example {i}",
                        "key": i,
                        "children": fac.AntdText(f"Accordion item example {i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["2"],
            ),
            fac.AntdParagraph(id="accordion-demo-output"),
        ]

    return demo_contents


@app.callback(
    Output("accordion-demo-output", "children"),
    Input("accordion-demo", "activeKey"),
)
def accordion_demo(activeKey):
    # localize output prefix if desired (kept consistent with original)
    prefix = "activeKey"
    return f"{prefix}: {activeKey}"


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
[
    fac.AntdAccordion(
        id='accordion-demo',
        items=[
            {
                'title': f'Accordion item example {i}',
                'key': i,
                'children': fac.AntdText(f'Accordion item example {i}'),
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
"""
            }
        ]

```

### `views/AntdAccordion/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"手风琴项示例{i}",
                    "key": i,
                    "children": fac.AntdText(f"手风琴项示例{i}"),
                }
                for i in range(1, 6)
            ]
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"Accordion item example {i}",
                    "key": i,
                    "children": fac.AntdText(f"Accordion item example {i}"),
                }
                for i in range(1, 6)
            ]
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdAccordion(
    items=[
        {
            'title': f'Accordion item example {i}',
            'key': i,
            'children': fac.AntdText(f'Accordion item example {i}'),
        }
        for i in range(1, 6)
    ]
)
"""
            }
        ]

```

### `views/AntdAccordion/demos/default_active_key.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = [
            fac.AntdDivider("手风琴模式开", innerTextOrientation="left"),
            fac.AntdAccordion(
                items=[
                    {
                        "title": f"手风琴项示例{i}",
                        "key": i,
                        "children": fac.AntdText(f"手风琴项示例{i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["3"],
            ),
            fac.AntdDivider("手风琴模式关", innerTextOrientation="left"),
            fac.AntdAccordion(
                items=[
                    {
                        "title": f"手风琴项示例{i}",
                        "key": i,
                        "children": fac.AntdText(f"手风琴项示例{i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["1", "3", "4"],
                accordion=False,
            ),
        ]

    elif current_locale == "en-us":
        demo_contents = [
            fac.AntdDivider("Accordion mode ON", innerTextOrientation="left"),
            fac.AntdAccordion(
                items=[
                    {
                        "title": f"Accordion item example {i}",
                        "key": i,
                        "children": fac.AntdText(f"Accordion item example {i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["3"],
            ),
            fac.AntdDivider("Accordion mode OFF", innerTextOrientation="left"),
            fac.AntdAccordion(
                items=[
                    {
                        "title": f"Accordion item example {i}",
                        "key": i,
                        "children": fac.AntdText(f"Accordion item example {i}"),
                    }
                    for i in range(1, 6)
                ],
                defaultActiveKey=["1", "3", "4"],
                accordion=False,
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
[
    fac.AntdDivider('Accordion mode ON', innerTextOrientation='left'),
    fac.AntdAccordion(
        items=[
            {
                'title': f'Accordion item example {i}',
                'key': i,
                'children': fac.AntdText(f'Accordion item example {i}'),
            }
            for i in range(1, 6)
        ],
        defaultActiveKey=['3'],
    ),
    fac.AntdDivider('Accordion mode OFF', innerTextOrientation='left'),
    fac.AntdAccordion(
        items=[
            {
                'title': f'Accordion item example {i}',
                'key': i,
                'children': fac.AntdText(f'Accordion item example {i}'),
            }
            for i in range(1, 6)
        ],
        defaultActiveKey=['1', '3', '4'],
        accordion=False,
    ),
]
"""
            }
        ]

```

### `views/AntdAccordion/demos/expand_icon_right.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"手风琴项示例{i}",
                    "key": i,
                    "children": fac.AntdText(f"手风琴项示例{i}"),
                }
                for i in range(1, 6)
            ],
            expandIconPosition="right",
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"Accordion item example {i}",
                    "key": i,
                    "children": fac.AntdText(f"Accordion item example {i}"),
                }
                for i in range(1, 6)
            ],
            expandIconPosition="right",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdAccordion(
    items=[
        {
            'title': f'Accordion item example {i}',
            'key': i,
            'children': fac.AntdText(f'Accordion item example {i}'),
        }
        for i in range(1, 6)
    ],
    expandIconPosition='right',
)
"""
            }
        ]

```

### `views/AntdAccordion/demos/extra.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        # 构造演示用例相关内容
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"手风琴项示例{i}",
                    "key": i,
                    "children": fac.AntdText(f"手风琴项示例{i}"),
                    "extra": fac.AntdButton("额外内容", type="link", size="small"),
                }
                for i in range(1, 6)
            ],
            collapsible="header",
        )

    elif current_locale == "en-us":
        # construct demo contents
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"Accordion item example {i}",
                    "key": i,
                    "children": fac.AntdText(f"Accordion item example {i}"),
                    "extra": fac.AntdButton("Extra content", type="link", size="small"),
                }
                for i in range(1, 6)
            ],
            collapsible="header",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]

    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdAccordion(
    items=[
        {
            'title': f'Accordion item example {i}',
            'key': i,
            'children': fac.AntdText(f'Accordion item example {i}'),
            'extra': fac.AntdButton('Extra content', type='link', size='small'),
        }
        for i in range(1, 6)
    ],
    collapsible='header',
)
"""
            }
        ]

```

### `views/AntdAccordion/demos/ghost.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"手风琴项示例{i}",
                    "key": i,
                    "children": fac.AntdText(f"手风琴项示例{i}"),
                }
                for i in range(1, 6)
            ],
            ghost=True,
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdAccordion(
            items=[
                {
                    "title": f"Accordion item example {i}",
                    "key": i,
                    "children": fac.AntdText(f"Accordion item example {i}"),
                }
                for i in range(1, 6)
            ],
            ghost=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdAccordion(
    items=[
        {
            'title': f'Accordion item example {i}',
            'key': i,
            'children': fac.AntdText(f'Accordion item example {i}'),
        }
        for i in range(1, 6)
    ],
    ghost=True,
)
"""
            }
        ]

```

### `views/AntdAccordion/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdAccordion(
                    items=[
                        {
                            "title": f"{size}手风琴项示例{i}",
                            "key": i,
                            "children": fac.AntdText(f"{size}手风琴项示例{i}"),
                        }
                        for i in range(1, 3)
                    ],
                    size=size,
                )
                for size in ["small", "middle", "large"]
            ],
            direction="vertical",
            style={"width": "100%"},
        )

    elif current_locale == "en-us":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdAccordion(
                    items=[
                        {
                            "title": f"{size} accordion item example {i}",
                            "key": i,
                            "children": fac.AntdText(
                                f"{size} accordion item example {i}"
                            ),
                        }
                        for i in range(1, 3)
                    ],
                    size=size,
                )
                for size in ["small", "middle", "large"]
            ],
            direction="vertical",
            style={"width": "100%"},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == "zh-cn":
        return [
            {
                "code": """
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
"""
            }
        ]
    elif current_locale == "en-us":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdAccordion(
            items=[
                {
                    'title': f'{size} accordion item example {i}',
                    'key': i,
                    'children': fac.AntdText(f'{size} accordion item example {i}'),
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
"""
            }
        ]

```

## API 文档

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
