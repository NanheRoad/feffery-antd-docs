# AntdDescriptions

## 简介源码：`views/AntdDescriptions/intro.py`
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
                {'title': '描述列表'},
                {'title': 'AntdDescriptions 描述列表'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDescriptions 描述列表', level=2),
        fac.AntdParagraph('用于配合AntdDescriptionItem进行一组属性的展示。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdDivider('默认无边框', innerTextOrientation='left'),
    fac.AntdDescriptions(
        [
            fac.AntdDescriptionItem('费弗里', label='姓名'),
            fac.AntdDescriptionItem(
                html.A(
                    'https://github.com/CNFeffery',
                    href='https://github.com/CNFeffery',
                ),
                label='个人Github地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'https://www.cnblogs.com/feffery/',
                    href='https://www.cnblogs.com/feffery/',
                ),
                label='个人博客地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'http://fac.feffery.tech/',
                    href='http://fac.feffery.tech/',
                ),
                label='fac框架官网',
            ),
        ],
        title='描述列表示例',
        styles={'label': {'fontWeight': 'bold'}},
    ),
    fac.AntdDivider('添加边框', innerTextOrientation='left'),
    fac.AntdDescriptions(
        [
            fac.AntdDescriptionItem('费弗里', label='姓名'),
            fac.AntdDescriptionItem(
                html.A(
                    'https://github.com/CNFeffery',
                    href='https://github.com/CNFeffery',
                ),
                label='个人Github地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'https://www.cnblogs.com/feffery/',
                    href='https://www.cnblogs.com/feffery/',
                ),
                label='个人博客地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'http://fac.feffery.tech/',
                    href='http://fac.feffery.tech/',
                ),
                label='fac框架官网',
            ),
        ],
        title='描述列表示例',
        bordered=True,
        styles={'label': {'fontWeight': 'bold'}},
    ),
]
```

### column

- 说明：演示 column 的用法。

#### 代码
```python
[
    fac.AntdDivider('column=2', innerTextOrientation='left'),
    fac.AntdDescriptions(
        [
            fac.AntdDescriptionItem('费弗里', label='姓名'),
            fac.AntdDescriptionItem(
                html.A(
                    'https://github.com/CNFeffery',
                    href='https://github.com/CNFeffery',
                ),
                label='个人Github地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'https://www.cnblogs.com/feffery/',
                    href='https://www.cnblogs.com/feffery/',
                ),
                label='个人博客地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'http://fac.feffery.tech/',
                    href='http://fac.feffery.tech/',
                ),
                label='fac框架官网',
            ),
        ],
        title='描述列表示例',
        bordered=True,
        column=2,
        styles={'label': {'fontWeight': 'bold'}},
    ),
    fac.AntdDivider('column=4', innerTextOrientation='left'),
    fac.AntdDescriptions(
        [
            fac.AntdDescriptionItem('费弗里', label='姓名'),
            fac.AntdDescriptionItem(
                html.A(
                    'https://github.com/CNFeffery',
                    href='https://github.com/CNFeffery',
                ),
                label='个人Github地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'https://www.cnblogs.com/feffery/',
                    href='https://www.cnblogs.com/feffery/',
                ),
                label='个人博客地址',
            ),
            fac.AntdDescriptionItem(
                html.A(
                    'http://fac.feffery.tech/',
                    href='http://fac.feffery.tech/',
                ),
                label='fac框架官网',
            ),
        ],
        title='描述列表示例',
        bordered=True,
        column=4,
        styles={'label': {'fontWeight': 'bold'}},
    ),
]
```

### extra

- 说明：演示 extra 的用法。

#### 代码
```python
fac.AntdDescriptions(
    items=[
        {'label': fac.AntdText('姓名'), 'children': '费弗里'},
        {
            'label': fac.AntdText('个人Github地址'),
            'children': html.A(
                'https://github.com/CNFeffery',
                href='https://github.com/CNFeffery',
            ),
        },
        {
            'label': fac.AntdText('个人博客地址'),
            'children': html.A(
                'https://www.cnblogs.com/feffery/',
                href='https://www.cnblogs.com/feffery/',
            ),
        },
        {
            'label': fac.AntdText('fac框架官网'),
            'children': html.A(
                'http://fac.feffery.tech/', href='http://fac.feffery.tech/'
            ),
        },
    ],
    title='描述列表示例',
    styles={'label': {'fontWeight': 'bold'}},
    bordered=True,
    extra=fac.AntdButton(
        '额外内容',
        type='primary',
    ),
)
```

### item_span

- 说明：演示 item_span 的用法。

#### 代码
```python
fac.AntdDescriptions(
    [
        fac.AntdDescriptionItem('费弗里', label='姓名', span=2),
        fac.AntdDescriptionItem(
            html.A(
                'https://github.com/CNFeffery',
                href='https://github.com/CNFeffery',
            ),
            label='个人Github地址',
        ),
        fac.AntdDescriptionItem(
            html.A(
                'https://www.cnblogs.com/feffery/',
                href='https://www.cnblogs.com/feffery/',
            ),
            label='个人博客地址',
        ),
        fac.AntdDescriptionItem(
            html.A(
                'http://fac.feffery.tech/', href='http://fac.feffery.tech/'
            ),
            label='fac框架官网',
        ),
    ],
    title='描述列表示例',
    bordered=True,
    styles={'label': {'fontWeight': 'bold'}},
)
```

### span_filled

- 说明：演示 span_filled 的用法。

#### 代码
```python
fac.AntdDescriptions(
    items=[
        {
            'label': 'item1',
            'children': 'default span',
        },
        {
            'label': 'item2',
            'children': 'span="filled"',
            'span': 'filled',
        },
        {
            'label': 'item3',
            'children': 'span="filled"',
            'span': 'filled',
        },
        {
            'label': 'item4',
            'children': 'default span',
        },
    ],
    bordered=True,
)
```

### use_items

- 说明：演示 use_items 的用法。

#### 代码
```python
fac.AntdDescriptions(
    items=[
        {'label': fac.AntdText('姓名'), 'children': '费弗里'},
        {
            'label': fac.AntdText('个人Github地址'),
            'children': html.A(
                'https://github.com/CNFeffery',
                href='https://github.com/CNFeffery',
            ),
        },
        {
            'label': fac.AntdText('个人博客地址'),
            'children': html.A(
                'https://www.cnblogs.com/feffery/',
                href='https://www.cnblogs.com/feffery/',
            ),
        },
        {
            'label': fac.AntdText('fac框架官网'),
            'children': html.A(
                'http://fac.feffery.tech/', href='http://fac.feffery.tech/'
            ),
        },
    ],
    title='描述列表示例',
    styles={'label': {'fontWeight': 'bold'}},
    bordered=True,
)
```

### vertical_layout

- 说明：演示 vertical_layout 的用法。

#### 代码
```python
fac.AntdDescriptions(
    [
        fac.AntdDescriptionItem('费弗里', label='姓名'),
        fac.AntdDescriptionItem(
            html.A(
                'https://github.com/CNFeffery',
                href='https://github.com/CNFeffery',
            ),
            label='个人Github地址',
        ),
        fac.AntdDescriptionItem(
            html.A(
                'https://www.cnblogs.com/feffery/',
                href='https://www.cnblogs.com/feffery/',
            ),
            label='个人博客地址',
        ),
        fac.AntdDescriptionItem(
            html.A(
                'http://fac.feffery.tech/', href='http://fac.feffery.tech/'
            ),
            label='fac框架官网',
        ),
    ],
    title='描述列表示例',
    bordered=True,
    layout='vertical',
    styles={'label': {'fontWeight': 'bold'}},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，传入内部各描述列表子项.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素css样式.

    - header (dict; optional):
        头部元素css样式.

    - title (dict; optional):
        标题元素css样式.

    - extra (dict; optional):
        额外内容css样式.

    - label (dict; optional):
        标签元素css样式.

    - content (dict; optional):
        内容元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素css类名.

    - header (string; optional):
        头部元素css类名.

    - title (string; optional):
        标题元素css类名.

    - extra (string; optional):
        额外内容css类名.

    - label (string; optional):
        标签元素css类名.

    - content (string; optional):
        内容元素css类名.

- items (list of dicts; optional):
    配置描述列表子项，优先级高于`children`.

    `items` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，子项标题内容.

    - span (number | a value equal to: 'filled'; optional):
        子项所占宽度份数，当设置为`'filled'`时会自适应占满当前行剩余可用空间  默认值：`1`.

    - children (a list of or a singular dash component, string or number; optional):
        组件型，子项内容.

    - style (dict; optional):
        子项css样式.

    - className (string; optional):
        子项css类名.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- column (dict; default 3):
    每行显示的字段项数量，支持响应式  默认值：`3`.

    `column` is a number | dict with keys:

    - xxl (number; optional)

    - xl (number; optional)

    - lg (number; optional)

    - md (number; optional)

    - sm (number; optional)

    - xs (number; optional)

- bordered (boolean; default False):
    是否显示边框  默认值：`False`.

- size (a value equal to: 'small', 'default', 'large'; default 'default'):
    整体尺寸规格，可选项有`'small'`、`'default'`、`'large'`  默认值：`'default'`.

- layout (a value equal to: 'horizontal', 'vertical'; default 'horizontal'):
    布局方式，可选项有`'horizontal'`、`'vertical'`  默认值：`'horizontal'`.

- extra (a list of or a singular dash component, string or number; optional):
    组件型，设置操作区域，显示在右上方.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
