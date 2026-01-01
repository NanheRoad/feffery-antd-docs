# AntdCollapse

## 简介源码：`views/AntdCollapse/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdCollapse 折叠面板'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCollapse 折叠面板', level=2),
        fac.AntdParagraph('可折叠展开的特殊容器。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            id='collapse-demo',
            isOpen=True,
            title='回调示例',
            style={'width': 300},
        ),
        fac.AntdText(id='collapse-demo-output'),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('collapse-demo-output', 'children'), Input('collapse-demo', 'isOpen')
)
def collapse_demo(isOpen):
    return f'isOpen={isOpen}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    title='折叠面板示例',
    style={'width': 300},
)
```

### collapsible

- 说明：演示 collapsible 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="header"',
            collapsible='header',
            isOpen=False,
            style={'width': 300},
        ),
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="disabled"',
            collapsible='disabled',
            isOpen=False,
            style={'width': 300},
        ),
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title='collapsible="icon"',
            collapsible='icon',
            isOpen=False,
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### force_render

- 说明：演示 force_render 的用法。

#### 代码
```python
[
    fac.AntdDivider(
        'forceRender=False（默认）', innerTextOrientation='left'
    ),
    fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdInput(
                    id='collapse-child-demo1',
                    defaultValue='内容测试',
                    style={'width': '100%'},
                ),
                isOpen=False,
                style={'width': 300},
            ),
            fac.AntdText(id='collapse-child-demo1-output'),
        ]
    ),
    fac.AntdDivider('forceRender=True', innerTextOrientation='left'),
    fac.AntdSpace(
        [
            fac.AntdCollapse(
                fac.AntdInput(
                    id='collapse-child-demo2',
                    defaultValue='内容测试',
                    style={'width': '100%'},
                ),
                isOpen=False,
                forceRender=True,
                style={'width': 300},
            ),
            fac.AntdText(id='collapse-child-demo2-output'),
        ]
    ),
]

...

@app.callback(
    Output('collapse-child-demo1-output', 'children'),
    Input('collapse-child-demo1', 'value'),
)
def collapse_child_demo1(value):
    return value


@app.callback(
    Output('collapse-child-demo2-output', 'children'),
    Input('collapse-child-demo2', 'value'),
)
def collapse_child_demo2(value):
    return value
```

### ghost

- 说明：演示 ghost 的用法。

#### 代码
```python
html.Div(
    fac.AntdCollapse(
        fac.AntdParagraph('内容示例' * 20), ghost=True, title='折叠面板示例'
    ),
    style={'background': '#e7f5ff', 'width': 300},
)
```

### is_open

- 说明：演示 is_open 的用法。

#### 代码
```python
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    isOpen=False,
    title='折叠面板示例',
    style={'width': 300},
)
```

### non_bordered

- 说明：演示 non_bordered 的用法。

#### 代码
```python
fac.AntdCollapse(
    fac.AntdParagraph('内容示例' * 20),
    bordered=False,
    title='折叠面板示例',
    style={'width': 300},
)
```

### size

- 说明：演示 size 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCollapse(
            fac.AntdParagraph('内容示例' * 20),
            title=f'size="{size}"',
            style={'width': 300},
        )
        for size in ['small', 'middle', 'large']
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - header (dict; optional):
        头部元素css样式.

    - body (dict; optional):
        内容元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - header (string; optional):
        头部元素css类名.

    - body (string; optional):
        内容元素css类名.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- isOpen (boolean; default True):
    是否展开  默认值：`True`.

- size (a value equal to: 'large', 'middle', 'small'; default 'middle'):
    组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- bordered (boolean; default True):
    是否渲染边框  默认值：`True`.

- showArrow (boolean; default True):
    是否渲染箭头  默认值：`True`.

- ghost (boolean; default False):
    是否开启透明背景模式  默认值：`False`.

- collapsible (a value equal to: 'header', 'disabled', 'icon'; optional):
    折叠交互触发行为，可选项有`'header'`（仅标题区域）、`'disabled'`（禁用折叠）、`'icon'`（仅图标区域）.

- forceRender (boolean; default False):
    初始化未展开时，是否强制渲染内部元素  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'isOpen's; optional):
    开启属性持久化功能的若干属性名，可选项有`'isOpen'`  默认值：`['isOpen']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
