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

## 示例源码（demos）

### `views/AntdDescriptions/demos/basic_usage.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/column.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/extra.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDescriptions(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/item_span.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDescriptions(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/span_filled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDescriptions(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/use_items.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDescriptions(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdDescriptions/demos/vertical_layout.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdDescriptions(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```
