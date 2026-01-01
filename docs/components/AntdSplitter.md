# AntdSplitter

## 简介源码：`views/AntdSplitter/intro.py`
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
                {'title': translator.t('AntdSplitter 分隔面板')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdSplitter 分隔面板'), level=2),
        fac.AntdParagraph(
            translator.t('对指定区域进行切分，并添加交互性的尺寸调整。')
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：默认情况下，每个子项会自动均等分所在分隔面板容器。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    )
                }
                for i in range(1, 3)
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    )
                }
                for i in range(1, 4)
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 可折叠

- 说明：控制子项区域开启快捷折叠功能。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    ),
                    'collapsible': True,
                }
                for i in range(1, 3)
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    ),
                    'collapsible': True,
                }
                for i in range(1, 3)
            ],
            layout='vertical',
            style={
                'height': 300,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 默认尺寸

- 说明：为子项设置默认尺寸。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        '30%', style={'height': '100%'}
                    ),
                    'defaultSize': '30%',
                },
                {
                    'children': fac.AntdCenter(
                        '70%', style={'height': '100%'}
                    ),
                    'defaultSize': '70%',
                },
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        '30%', style={'height': '100%'}
                    ),
                    'defaultSize': '30%',
                },
                {
                    'children': fac.AntdCenter(
                        '70%', style={'height': '100%'}
                    ),
                    'defaultSize': '70%',
                },
            ],
            layout='vertical',
            style={
                'height': 300,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 延迟渲染模式

- 说明：设置`lazy=True`启用延迟渲染模式，即在每次拖拽调整结束后才会更新布局。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    )
                }
                for i in range(1, 3)
            ],
            lazy=True,
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        f'item{i}', style={'height': '100%'}
                    )
                }
                for i in range(1, 4)
            ],
            lazy=True,
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 嵌套组合

- 说明：通过嵌套组合分隔面板组件，实现更复杂的布局。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        'item1', style={'height': '100%'}
                    ),
                    'defaultSize': '30%',
                },
                {
                    'children': fac.AntdSplitter(
                        items=[
                            {
                                'children': fac.AntdCenter(
                                    'item2', style={'height': '100%'}
                                ),
                                'defaultSize': '30%',
                            },
                            {
                                'children': fac.AntdCenter(
                                    'item3', style={'height': '100%'}
                                ),
                                'defaultSize': '70%',
                            },
                        ],
                        layout='vertical',
                        style={'height': '100%'},
                    ),
                    'defaultSize': '70%',
                },
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        )
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 限制尺寸调整范围

- 说明：为子项设置允许调整的尺寸范围，支持数值像素或百分比格式。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        'min: 50 max: 90%', style={'height': '100%'}
                    ),
                    'defaultSize': '30%',
                    'min': 50,
                    'max': '90%',
                },
                {
                    'children': fac.AntdCenter(
                        '70%', style={'height': '100%'}
                    ),
                    'defaultSize': '70%',
                },
            ],
            style={
                'height': 200,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
        fac.AntdSplitter(
            items=[
                {
                    'children': fac.AntdCenter(
                        'min: 50 max: 90%', style={'height': '100%'}
                    ),
                    'defaultSize': '30%',
                    'min': 50,
                    'max': '90%',
                },
                {
                    'children': fac.AntdCenter(
                        '70%', style={'height': '100%'}
                    ),
                    'defaultSize': '70%',
                },
            ],
            layout='vertical',
            style={
                'height': 300,
                'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### 垂直布局

- 说明：设置参数`layout='vertical'`启用垂直布局。

#### 代码
```python
fac.AntdSplitter(
    items=[
        {'children': fac.AntdCenter(f'item{i}', style={'height': '100%'})}
        for i in range(1, 3)
    ],
    layout='vertical',
    style={
        'height': 300,
        'boxShadow': '0 0 10px rgba(0, 0, 0, 0.1)',
    },
)
```

## API 参数说明


- id (string; optional):
    The unique identifier for the component.

- key (string; optional):
    Updates the `key` value of the current component, which can force a redraw of the current component.

- style (dict; optional):
    The CSS styles for the current component.

- className (string | dict; optional):
    The CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- layout (a value equal to: 'horizontal', 'vertical'; default 'horizontal'):
    The layout direction, options include `'horizontal'`, `'vertical'`. Default value: `'horizontal'`.

- items (list of dicts; required):
    Configures the subitems of the split panel, with higher priority than `children`.

    `items` is a list of dictionaries with keys:

    - key (string; optional):
        The key for the panel.

    - children (a list of or a singular dash component, string or number; optional):
        The component type, embedded elements.

    - style (dict; optional):
        The CSS styles for the current component.

    - className (string or dict; optional):
        The CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

    - defaultSize (number | string; optional):
        The initial panel size, supports numeric `px` or textual `'percentage%'` types.

    - min (number | string; optional):
        The minimum threshold, supports numeric `px` or textual `'percentage%'` types.

    - max (number | string; optional):
        The maximum threshold, supports numeric `px` or textual `'percentage%'` types.

    - size (number | string; optional):
        The panel size, supports numeric `px` or textual `'percentage%'` types.

    - collapsible (dict; optional):
        Whether it is collapsible. Default value: `False`.

        `collapsible` is a boolean | dict with keys:

        - start (boolean; optional)

        - end (boolean; optional)

    - resizable (boolean; optional):
        Whether to enable drag-to-resize. Default value: `True`.

- currentSizes (list of dicts; optional):
    Listens for changes in the current panel size information.

    `currentSizes` is a list of dictionaries with keys:

    - key (string; optional):
        The key for the panel.

    - size (number | string; optional):
        The size of the panel.

- data-* (string; optional):
    A wildcard for `data-*` format attributes.

- aria-* (string; optional):
    A wildcard for `aria-*` format attributes.

- loading_state (dict; optional)

    `loading_state` is a dictionary with keys:

    - is_loading (boolean; optional):
        Determines whether the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.
