# AntdColorPicker

## 简介源码：`views/AntdColorPicker/intro.py`
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
                {'title': translator.t('AntdColorPicker 颜色选择')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdColorPicker 颜色选择'), level=2),
        fac.AntdParagraph(translator.t('提供颜色值选择功能。')),
    ]

```

## 示例源码（demos）

### `views/AntdColorPicker/demos/allow_clear.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker(allowClear=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker(allowClear=True)
"""
    }
]

```

### `views/AntdColorPicker/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdColorPicker(id='color-picker-demo'),
            fac.AntdText(id='color-picker-demo-output'),
        ]
    )

    return demo_contents


@app.callback(
    Output('color-picker-demo-output', 'children'),
    Input('color-picker-demo', 'value'),
    prevent_initial_call=True,
)
def color_picker_event(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdColorPicker(id='color-picker-demo'),
        fac.AntdText(id='color-picker-demo-output'),
    ]
)

...

@app.callback(
    Output('color-picker-demo-output', 'children'),
    Input('color-picker-demo', 'value'),
    prevent_initial_call=True,
)
def color_picker_event(value):
    return f'value: {value}'
"""
    }
]

```

### `views/AntdColorPicker/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker()

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker()
"""
    }
]

```

### `views/AntdColorPicker/demos/different_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdColorPicker(placement=placement)
            for placement in [
                'top',
                'topLeft',
                'topRight',
                'bottom',
                'bottomLeft',
                'bottomRight',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdColorPicker(placement=placement)
        for placement in [
            'top',
            'topLeft',
            'topRight',
            'bottom',
            'bottomLeft',
            'bottomRight',
        ]
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdColorPicker/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker(disabled=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker(disabled=True)
"""
    }
]

```

### `views/AntdColorPicker/demos/enable_alpha.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker(disabledAlpha=False)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker(disabledAlpha=False)
"""
    }
]

```

### `views/AntdColorPicker/demos/mode.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdSpace(
            [
                # 渐变色
                fac.AntdColorPicker(mode='gradient'),
                # 单色彩+渐变色
                fac.AntdColorPicker(mode=['single', 'gradient']),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        # construct demo contents
        demo_contents = fac.AntdSpace(
            [
                # gradient
                fac.AntdColorPicker(mode='gradient', locale='en-us'),
                # single + gradient
                fac.AntdColorPicker(
                    mode=['single', 'gradient'], locale='en-us'
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        # 渐变色
        fac.AntdColorPicker(mode='gradient'),
        # 单色彩+渐变色
        fac.AntdColorPicker(mode=['single', 'gradient']),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        # gradient
        fac.AntdColorPicker(mode='gradient', locale='en-us'),
        # single + gradient
        fac.AntdColorPicker(
            mode=['single', 'gradient'], locale='en-us'
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdColorPicker/demos/presets.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component
from palettable.colorbrewer.sequential import Blues_9, Greens_9, Reds_9


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker(
        presets=[
            {'colors': c.hex_colors, 'label': c.name, 'defaultOpen': i == 0}
            for i, c in enumerate([Blues_9, Greens_9, Reds_9])
        ]
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker(
    presets=[
        {'colors': c.hex_colors, 'label': c.name, 'defaultOpen': i == 0}
        for i, c in enumerate([Blues_9, Greens_9, Reds_9])
    ]
)
"""
    }
]

```

### `views/AntdColorPicker/demos/show_text.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdColorPicker(showText=True)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdColorPicker(showText=True)
"""
    }
]

```

### `views/AntdColorPicker/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdColorPicker(size=size)
            for size in ['small', 'middle', 'large']
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdColorPicker(size=size)
        for size in ['small', 'middle', 'large']
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdColorPicker/demos/trigger.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdColorPicker(trigger=trigger)
            for trigger in ['hover', 'click']
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdColorPicker(trigger=trigger)
        for trigger in ['hover', 'click']
    ],
    wrap=True,
)
"""
    }
]

```

## API 文档

- id (string; optional):
    Unique identifier for the component.

- key (string; optional):
    Update the `key` value of the current component to force a redraw of the component.

- style (dict; optional):
    CSS styles for the current component.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de'; default 'zh-cn'):
    Language of the component's text, options include `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German).
    Default value: `'zh-cn'`.

- name (string; optional):
    Used in conjunction with the `AntdForm` form for batch value collection/control, serving as the field name for the current form item, with `id` as the default value.

- allowClear (boolean; default False):
    Whether to allow clearing the selected color. Default value: `False`.

- arrow (dict; optional):
    Configure additional arrows for the color selection panel. Default value: `True`.

    `arrow` is a boolean | dict with keys:

    - pointAtCenter (boolean; optional):
        Whether the arrow points to the center of the panel. Default value: `False`.

- defaultValue (string; optional):
    The initial input value.

- value (string; optional):
    Listening to or setting the selected color value. Default value: `'#1677FF'`.

- format (a value equal to: 'rgb', 'hex', 'hsb'; default 'hex'):
    Listening to or setting the color format, options include `'rgb'`, `'hex'`, `'hsb'`. Default value: `'hex'`.

- mode (a value equal to: 'single', 'gradient' | list of a value equal to: 'single', 'gradient's; default 'single'):
    The selector mode, used to configure single color and gradient, options include `'single'`, `'gradient'`, supports single or multiple option combinations.
    Default value: `single`.

- disabled (boolean; default False):
    Whether to disable the current component. Default value: `False`.

- disabledAlpha (boolean; default True):
    Whether to disable the transparency selection. Default value: `True`.

- open (boolean; optional):
    Listening to or setting the expansion state of the color selection panel.

- presets (list of dicts; optional):
    Configure preset color selection options.

    `presets` is a list of dicts with keys:

    - colors (list of strings; optional):
        An array of color values included in the current preset.

    - defaultOpen (boolean; optional):
        Whether the current preset is expanded by default. Default value: `True`.

    - label (a list of or a singular dash component, string or number; optional):
        Component type, the label content of the current preset.

- placement (a value equal to: 'top', 'topLeft', 'topRight', 'bottom', 'bottomLeft', 'bottomRight'; default 'bottomLeft'):
    The expansion direction of the color selection panel, options include `'top'`, `'topLeft'`, `'topRight'`, `'bottom'`, `'bottomLeft'`, `'bottomRight'`.
    Default value: `'bottomRight'`.

- showText (boolean; default False):
    Whether to display the color value text. Default value: `False`.

- size (a value equal to: 'large', 'middle', 'small'; default 'middle'):
    Set the size specification of the trigger control, options include `'large'`, `'middle'`, `'small'`. Default value: `'middle'`.

- trigger (a value equal to: 'hover', 'click'; default 'click'):
    The trigger method of the color selection panel, options include `'hover'`, `'click'`. Default value: `'click'`.

- data-* (string; optional):
    `data-*` format attribute wildcard.

- aria-* (string; optional):
    `aria-*` format attribute wildcard.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - component_name (string; optional):
        Holds the name of the component that is loading.

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.
