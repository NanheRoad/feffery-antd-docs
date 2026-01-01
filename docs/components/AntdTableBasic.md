# AntdTableBasic

## 简介源码：`views/AntdTableBasic/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('数据展示')},
                {'title': translator.t('AntdTable 表格')},
                {'title': translator.t('基础功能')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件主要基础功能示例。')),
    ]

```

## 示例源码（demos）

### `views/AntdTableBasic/demos/basic_usage.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': 'int型示例', 'dataIndex': 'int型示例'},
                {'title': 'float型示例', 'dataIndex': 'float型示例'},
                {'title': 'str型示例', 'dataIndex': 'str型示例'},
                {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
            ],
            data=[
                {
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now(),
                }
            ]
            * 3,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': 'int Example', 'dataIndex': 'int Example'},
                {'title': 'float Example', 'dataIndex': 'float Example'},
                {'title': 'str Example', 'dataIndex': 'str Example'},
                {'title': 'Datetime Example', 'dataIndex': 'Datetime Example'},
            ],
            data=[
                {
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now(),
                }
            ]
            * 3,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': 'int型示例', 'dataIndex': 'int型示例'},
        {'title': 'float型示例', 'dataIndex': 'float型示例'},
        {'title': 'str型示例', 'dataIndex': 'str型示例'},
        {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
    ],
    data=[
        {
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now(),
        }
    ]
    * 3,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': 'int Example', 'dataIndex': 'int Example'},
        {'title': 'float Example', 'dataIndex': 'float Example'},
        {'title': 'str Example', 'dataIndex': 'str Example'},
        {'title': 'Datetime Example', 'dataIndex': 'Datetime Example'},
    ],
    data=[
        {
            'int Example': 123,
            'float Example': 1.23,
            'str Example': 'Example string',
            'Datetime Example': datetime.now(),
        }
    ]
    * 3,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/bordered.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/column_content_align.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': align, 'dataIndex': align, 'align': align}
                for align in ['left', 'center', 'right']
            ],
            data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': align, 'dataIndex': align, 'align': align}
                for align in ['left', 'center', 'right']
            ],
            data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': align, 'dataIndex': align, 'align': align}
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': align, 'dataIndex': align, 'align': align}
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/column_header_align.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': align,
                    'dataIndex': align,
                    'headerAlign': align,
                }
                for align in ['left', 'center', 'right']
            ],
            data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': align,
                    'dataIndex': align,
                    'headerAlign': align,
                }
                for align in ['left', 'center', 'right']
            ],
            data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': align,
            'dataIndex': align,
            'headerAlign': align,
        }
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': align,
            'dataIndex': align,
            'headerAlign': align,
        }
        for align in ['left', 'center', 'right']
    ],
    data=[{align: 999 for align in ['left', 'center', 'right']}] * 3,
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/css_column_width.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'width': 'calc(100% / 5)',
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': f'Field {i}',
                    'dataIndex': f'Field {i}',
                    'width': 'calc(100% / 5)',
                }
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': f'字段{i}',
            'dataIndex': f'字段{i}',
            'width': 'calc(100% / 5)',
        }
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': f'Field {i}',
            'dataIndex': f'Field {i}',
            'width': 'calc(100% / 5)',
        }
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/dynamic_row_class_name.py`
```python
from datetime import datetime

import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fuc.FefferyStyle(
                rawStyle="""
.odd-row-class-name-demo {
    color: #f5222d;
}

.even-row-class-name-demo {
    color: #52c41a;
}
"""
            ),
            fac.AntdTable(
                columns=[
                    {'title': 'int型示例', 'dataIndex': 'int型示例'},
                    {'title': 'float型示例', 'dataIndex': 'float型示例'},
                    {'title': 'str型示例', 'dataIndex': 'str型示例'},
                    {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
                ],
                data=[
                    {
                        'int型示例': 123,
                        'float型示例': 1.23,
                        'str型示例': '示例字符',
                        '日期时间示例': datetime.now(),
                    }
                ]
                * 4,
                rowClassName={
                    'func': "(record, index) => index % 2 === 1 ? 'odd-row-class-name-demo' : 'even-row-class-name-demo'"
                },
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fuc.FefferyStyle(
                rawStyle="""
.odd-row-class-name-demo {
    color: #f5222d;
}

.even-row-class-name-demo {
    color: #52c41a;
}
"""
            ),
            fac.AntdTable(
                columns=[
                    {'title': 'int Example', 'dataIndex': 'int Example'},
                    {'title': 'float Example', 'dataIndex': 'float Example'},
                    {'title': 'str Example', 'dataIndex': 'str Example'},
                    {
                        'title': 'Datetime Example',
                        'dataIndex': 'Datetime Example',
                    },
                ],
                data=[
                    {
                        'int Example': 123,
                        'float Example': 1.23,
                        'str Example': 'Example string',
                        'Datetime Example': datetime.now(),
                    }
                ]
                * 4,
                rowClassName={
                    'func': "(record, index) => index % 2 === 1 ? 'odd-row-class-name-demo' : 'even-row-class-name-demo'"
                },
                locale='en-us',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
[
    fuc.FefferyStyle(
        rawStyle="""
.odd-row-class-name-demo {
    color: #f5222d;
}

.even-row-class-name-demo {
    color: #52c41a;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int型示例', 'dataIndex': 'int型示例'},
            {'title': 'float型示例', 'dataIndex': 'float型示例'},
            {'title': 'str型示例', 'dataIndex': 'str型示例'},
            {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
        ],
        data=[
            {
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now(),
            }
        ]
        * 4,
        rowClassName={
            'func': "(record, index) => index % 2 === 1 ? 'odd-row-class-name-demo' : 'even-row-class-name-demo'"
        },
    ),
]
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
[
    fuc.FefferyStyle(
        rawStyle="""
.odd-row-class-name-demo {
    color: #f5222d;
}

.even-row-class-name-demo {
    color: #52c41a;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int Example', 'dataIndex': 'int Example'},
            {'title': 'float Example', 'dataIndex': 'float Example'},
            {'title': 'str Example', 'dataIndex': 'str Example'},
            {'title': 'Datetime Example', 'dataIndex': 'Datetime Example'},
        ],
        data=[
            {
                'int Example': 123,
                'float Example': 1.23,
                'str Example': 'Example string',
                'Datetime Example': datetime.now(),
            }
        ]
        * 4,
        rowClassName={
            'func': "(record, index) => index % 2 === 1 ? 'odd-row-class-name-demo' : 'even-row-class-name-demo'"
        },
    ),
]
'''
            }
        ]

```

### `views/AntdTableBasic/demos/editable.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int型示例',
                    'dataIndex': 'int型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'float型示例',
                    'dataIndex': 'float型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'str型示例',
                    'dataIndex': 'str型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': '日期时间示例',
                    'dataIndex': '日期时间示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'placeholder示例',
                    'dataIndex': 'placeholder示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'placeholder': '请输入内容'},
                },
            ],
            data=[
                {
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
            ]
            * 3,
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int Example',
                    'dataIndex': 'int Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'float Example',
                    'dataIndex': 'float Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'str Example',
                    'dataIndex': 'str Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'Datetime Example',
                    'dataIndex': 'Datetime Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'Placeholder Example',
                    'dataIndex': 'Placeholder Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'placeholder': 'Please enter content'},
                },
            ],
            data=[
                {
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
            ]
            * 3,
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': '请输入内容'},
        },
    ],
    data=[
        {
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
    ]
    * 3,
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int Example',
            'dataIndex': 'int Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float Example',
            'dataIndex': 'float Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str Example',
            'dataIndex': 'str Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'Datetime Example',
            'dataIndex': 'Datetime Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'Placeholder Example',
            'dataIndex': 'Placeholder Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': 'Please enter content'},
        },
    ],
    data=[
        {
            'int Example': 123,
            'float Example': 1.23,
            'str Example': 'Example string',
            'Datetime Example': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
    ]
    * 3,
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/editable_disabled_keys.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int型示例',
                    'dataIndex': 'int型示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'float型示例',
                    'dataIndex': 'float型示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'str型示例',
                    'dataIndex': 'str型示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': '日期时间示例',
                    'dataIndex': '日期时间示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'placeholder示例',
                    'dataIndex': 'placeholder示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {
                        'placeholder': '请输入内容',
                        'disabledKeys': ['row-2'],
                    },
                },
            ],
            data=[
                {
                    'key': f'row-{i}',
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
                for i in range(1, 4)
            ],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int Example',
                    'dataIndex': 'int Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'float Example',
                    'dataIndex': 'float Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'str Example',
                    'dataIndex': 'str Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'Datetime Example',
                    'dataIndex': 'Datetime Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'disabledKeys': ['row-2']},
                },
                {
                    'title': 'Placeholder Example',
                    'dataIndex': 'Placeholder Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {
                        'placeholder': 'Please enter content',
                        'disabledKeys': ['row-2'],
                    },
                },
            ],
            data=[
                {
                    'key': f'row-{i}',
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
                for i in range(1, 4)
            ],
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {
                'placeholder': '请输入内容',
                'disabledKeys': ['row-2'],
            },
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int Example',
            'dataIndex': 'int Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'float Example',
            'dataIndex': 'float Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'str Example',
            'dataIndex': 'str Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'Datetime Example',
            'dataIndex': 'Datetime Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'disabledKeys': ['row-2']},
        },
        {
            'title': 'Placeholder Example',
            'dataIndex': 'Placeholder Example',
            'editable': True,
            'width': '20%',
            'editOptions': {
                'placeholder': 'Please enter content',
                'disabledKeys': ['row-2'],
            },
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int Example': 123,
            'float Example': 1.23,
            'str Example': 'Example string',
            'Datetime Example': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/fixed_columns.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdDivider('冻结在左侧', innerTextOrientation='left'),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'字段{i}',
                            'dataIndex': f'字段{i}',
                            'fixed': 'left' if i == 1 else None,
                        }
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
                    maxWidth=900,
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdDivider('冻结在右侧', innerTextOrientation='left'),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'字段{i}',
                            'dataIndex': f'字段{i}',
                            'fixed': 'right' if i == 5 else None,
                        }
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
                    maxWidth=900,
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdDivider('双侧同时冻结', innerTextOrientation='left'),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'字段{i}',
                            'dataIndex': f'字段{i}',
                            'fixed': (
                                'left'
                                if i == 1
                                else ('right' if i == 5 else None)
                            ),
                        }
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
                    maxWidth=900,
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdDivider('Frozen on the Left', innerTextOrientation='left'),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'Field {i}',
                            'dataIndex': f'Field {i}',
                            'fixed': 'left' if i == 1 else None,
                        }
                        for i in range(1, 6)
                    ],
                    data=[
                        {f'Field {i}': 'Example Content' for i in range(1, 6)}
                    ]
                    * 3,
                    maxWidth=900,
                    locale='en-us',
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdDivider('Frozen on the Right', innerTextOrientation='left'),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'Field {i}',
                            'dataIndex': f'Field {i}',
                            'fixed': 'right' if i == 5 else None,
                        }
                        for i in range(1, 6)
                    ],
                    data=[
                        {f'Field {i}': 'Example Content' for i in range(1, 6)}
                    ]
                    * 3,
                    locale='en-us',
                    maxWidth=900,
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdDivider(
                'Frozen on Both Sides', innerTextOrientation='left'
            ),
            html.Div(
                fac.AntdTable(
                    columns=[
                        {
                            'title': f'Field {i}',
                            'dataIndex': f'Field {i}',
                            'fixed': (
                                'left'
                                if i == 1
                                else ('right' if i == 5 else None)
                            ),
                        }
                        for i in range(1, 6)
                    ],
                    data=[
                        {f'Field {i}': 'Example Content' for i in range(1, 6)}
                    ]
                    * 3,
                    maxWidth=900,
                    locale='en-us',
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDivider('冻结在左侧', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': 'left' if i == 1 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('冻结在右侧', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': 'right' if i == 5 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('双侧同时冻结', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'字段{i}',
                    'dataIndex': f'字段{i}',
                    'fixed': (
                        'left' if i == 1 else ('right' if i == 5 else None)
                    ),
                }
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider('Frozen on the Left', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'Field {i}',
                    'dataIndex': f'Field {i}',
                    'fixed': 'left' if i == 1 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('Frozen on the Right', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'Field {i}',
                    'dataIndex': f'Field {i}',
                    'fixed': 'right' if i == 5 else None,
                }
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdDivider('Frozen on Both Sides', innerTextOrientation='left'),
    html.Div(
        fac.AntdTable(
            columns=[
                {
                    'title': f'Field {i}',
                    'dataIndex': f'Field {i}',
                    'fixed': (
                        'left' if i == 1 else ('right' if i == 5 else None)
                    ),
                }
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            maxWidth=900,
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
]
"""
            }
        ]

```

### `views/AntdTableBasic/demos/group_columns.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdDivider('单层分组', innerTextOrientation='left'),
            fac.AntdTable(
                columns=[
                    {
                        'title': '字段1-1',
                        'dataIndex': '字段1-1',
                        'group': '字段1',
                    },
                    {
                        'title': '字段1-2',
                        'dataIndex': '字段1-2',
                        'group': '字段1',
                    },
                    {'title': '字段2', 'dataIndex': '字段2'},
                    {
                        'title': '字段3-1',
                        'dataIndex': '字段3-1',
                        'group': '字段3',
                    },
                    {
                        'title': '字段3-2',
                        'dataIndex': '字段3-2',
                        'group': '字段3',
                    },
                    {
                        'title': '字段3-3',
                        'dataIndex': '字段3-3',
                        'group': '字段3',
                    },
                ],
                data=[
                    {
                        '字段1-1': 1,
                        '字段1-2': 1,
                        '字段2': 1,
                        '字段3-1': 1,
                        '字段3-2': 1,
                        '字段3-3': 1,
                    }
                ]
                * 3,
                bordered=True,
            ),
            fac.AntdDivider('更多层分组', innerTextOrientation='left'),
            fac.AntdTable(
                columns=[
                    {
                        'title': '字段1-1-1',
                        'dataIndex': '字段1-1-1',
                        'group': ['字段1', '字段1-1'],
                    },
                    {
                        'title': '字段1-1-2',
                        'dataIndex': '字段1-1-2',
                        'group': ['字段1', '字段1-1'],
                    },
                    {
                        'title': '字段1-2',
                        'dataIndex': '字段1-2',
                        'group': '字段1',
                    },
                    {'title': '字段2', 'dataIndex': '字段2'},
                ],
                data=[
                    {'字段1-1-1': 1, '字段1-1-2': 1, '字段1-2': 1, '字段2': 1}
                ]
                * 3,
                bordered=True,
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdDivider(
                'Single-level Grouping', innerTextOrientation='left'
            ),
            fac.AntdTable(
                columns=[
                    {
                        'title': 'Field1-1',
                        'dataIndex': 'Field1-1',
                        'group': 'Field1',
                    },
                    {
                        'title': 'Field1-2',
                        'dataIndex': 'Field1-2',
                        'group': 'Field1',
                    },
                    {'title': 'Field2', 'dataIndex': 'Field2'},
                    {
                        'title': 'Field3-1',
                        'dataIndex': 'Field3-1',
                        'group': 'Field3',
                    },
                    {
                        'title': 'Field3-2',
                        'dataIndex': 'Field3-2',
                        'group': 'Field3',
                    },
                    {
                        'title': 'Field3-3',
                        'dataIndex': 'Field3-3',
                        'group': 'Field3',
                    },
                ],
                data=[
                    {
                        'Field1-1': 1,
                        'Field1-2': 1,
                        'Field2': 1,
                        'Field3-1': 1,
                        'Field3-2': 1,
                        'Field3-3': 1,
                    }
                ]
                * 3,
                bordered=True,
                locale='en-us',
            ),
            fac.AntdDivider(
                'Multi-level Grouping', innerTextOrientation='left'
            ),
            fac.AntdTable(
                columns=[
                    {
                        'title': 'Field1-1-1',
                        'dataIndex': 'Field1-1-1',
                        'group': ['Field1', 'Field1-1'],
                    },
                    {
                        'title': 'Field1-1-2',
                        'dataIndex': 'Field1-1-2',
                        'group': ['Field1', 'Field1-1'],
                    },
                    {
                        'title': 'Field1-2',
                        'dataIndex': 'Field1-2',
                        'group': 'Field1',
                    },
                    {'title': 'Field2', 'dataIndex': 'Field2'},
                ],
                data=[
                    {
                        'Field1-1-1': 1,
                        'Field1-1-2': 1,
                        'Field1-2': 1,
                        'Field2': 1,
                    }
                ]
                * 3,
                bordered=True,
                locale='en-us',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDivider('单层分组', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': '字段1-1', 'dataIndex': '字段1-1', 'group': '字段1'},
            {'title': '字段1-2', 'dataIndex': '字段1-2', 'group': '字段1'},
            {'title': '字段2', 'dataIndex': '字段2'},
            {'title': '字段3-1', 'dataIndex': '字段3-1', 'group': '字段3'},
            {'title': '字段3-2', 'dataIndex': '字段3-2', 'group': '字段3'},
            {'title': '字段3-3', 'dataIndex': '字段3-3', 'group': '字段3'},
        ],
        data=[
            {
                '字段1-1': 1,
                '字段1-2': 1,
                '字段2': 1,
                '字段3-1': 1,
                '字段3-2': 1,
                '字段3-3': 1,
            }
        ]
        * 3,
        bordered=True,
    ),
    fac.AntdDivider('更多层分组', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {
                'title': '字段1-1-1',
                'dataIndex': '字段1-1-1',
                'group': ['字段1', '字段1-1'],
            },
            {
                'title': '字段1-1-2',
                'dataIndex': '字段1-1-2',
                'group': ['字段1', '字段1-1'],
            },
            {'title': '字段1-2', 'dataIndex': '字段1-2', 'group': '字段1'},
            {'title': '字段2', 'dataIndex': '字段2'},
        ],
        data=[{'字段1-1-1': 1, '字段1-1-2': 1, '字段1-2': 1, '字段2': 1}]
        * 3,
        bordered=True,
    ),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdDivider('Single-level Grouping', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': 'Field1-1', 'dataIndex': 'Field1-1', 'group': 'Field1'},
            {'title': 'Field1-2', 'dataIndex': 'Field1-2', 'group': 'Field1'},
            {'title': 'Field2', 'dataIndex': 'Field2'},
            {'title': 'Field3-1', 'dataIndex': 'Field3-1', 'group': 'Field3'},
            {'title': 'Field3-2', 'dataIndex': 'Field3-2', 'group': 'Field3'},
            {'title': 'Field3-3', 'dataIndex': 'Field3-3', 'group': 'Field3'},
        ],
        data=[
            {
                'Field1-1': 1,
                'Field1-2': 1,
                'Field2': 1,
                'Field3-1': 1,
                'Field3-2': 1,
                'Field3-3': 1,
            }
        ]
        * 3,
        bordered=True,
    ),
    fac.AntdDivider('Multi-level Grouping', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {
                'title': 'Field1-1-1',
                'dataIndex': 'Field1-1-1',
                'group': ['Field1', 'Field1-1'],
            },
            {
                'title': 'Field1-1-2',
                'dataIndex': 'Field1-1-2',
                'group': ['Field1', 'Field1-1'],
            },
            {'title': 'Field1-2', 'dataIndex': 'Field1-2', 'group': 'Field1'},
            {'title': 'Field2', 'dataIndex': 'Field2'},
        ],
        data=[{'Field1-1-1': 1, 'Field1-1-2': 1, 'Field1-2': 1, 'Field2': 1}]
        * 3,
        bordered=True,
    ),
]
"""
            }
        ]

```

### `views/AntdTableBasic/demos/listen_edit_event.py`
```python
import json
from datetime import datetime

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                id='table-editable-demo',
                columns=[
                    {
                        'title': 'int型示例',
                        'dataIndex': 'int型示例',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': 'float型示例',
                        'dataIndex': 'float型示例',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': 'str型示例',
                        'dataIndex': 'str型示例',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': '日期时间示例',
                        'dataIndex': '日期时间示例',
                        'editable': True,
                        'width': '25%',
                    },
                ],
                data=[
                    {
                        'key': f'row-{i}',
                        'int型示例': 123,
                        'float型示例': 1.23,
                        'str型示例': '示例字符',
                        '日期时间示例': datetime.now().strftime(
                            '%Y-%m-%d %H:%M:%S'
                        ),
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
            ),
            html.Pre(id='table-editable-demo-output'),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                id='table-editable-demo',
                columns=[
                    {
                        'title': 'int Example',
                        'dataIndex': 'int Example',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': 'float Example',
                        'dataIndex': 'float Example',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': 'str Example',
                        'dataIndex': 'str Example',
                        'editable': True,
                        'width': '25%',
                    },
                    {
                        'title': 'Datetime Example',
                        'dataIndex': 'Datetime Example',
                        'editable': True,
                        'width': '25%',
                    },
                ],
                data=[
                    {
                        'key': f'row-{i}',
                        'int Example': 123,
                        'float Example': 1.23,
                        'str Example': 'Example string',
                        'Datetime Example': datetime.now().strftime(
                            '%Y-%m-%d %H:%M:%S'
                        ),
                    }
                    for i in range(1, 4)
                ],
                bordered=True,
                locale='en-us',
            ),
            html.Pre(id='table-editable-demo-output'),
        ]

    return demo_contents


@app.callback(
    Output('table-editable-demo-output', 'children'),
    [
        Input('table-editable-demo', 'recentlyChangedRow'),
        Input('table-editable-demo', 'recentlyChangedColumn'),
    ],
    prevent_initial_call=True,
)
def table_editable_demo(recentlyChangedRow, recentlyChangedColumn):
    return json.dumps(
        dict(
            recentlyChangedRow=recentlyChangedRow,
            recentlyChangedColumn=recentlyChangedColumn,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-editable-demo',
        columns=[
            {
                'title': 'int型示例',
                'dataIndex': 'int型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'float型示例',
                'dataIndex': 'float型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'str型示例',
                'dataIndex': 'str型示例',
                'editable': True,
                'width': '25%',
            },
            {
                'title': '日期时间示例',
                'dataIndex': '日期时间示例',
                'editable': True,
                'width': '25%',
            },
        ],
        data=[
            {
                'key': f'row-{i}',
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now().strftime(
                    '%Y-%m-%d %H:%M:%S'
                ),
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-editable-demo-output'),
]

...

@app.callback(
    Output('table-editable-demo-output', 'children'),
    [
        Input('table-editable-demo', 'recentlyChangedRow'),
        Input('table-editable-demo', 'recentlyChangedColumn'),
    ],
    prevent_initial_call=True,
)
def table_editable_demo(recentlyChangedRow, recentlyChangedColumn):
    return json.dumps(
        dict(
            recentlyChangedRow=recentlyChangedRow,
            recentlyChangedColumn=recentlyChangedColumn,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-editable-demo',
        columns=[
            {
                'title': 'int Example',
                'dataIndex': 'int Example',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'float Example',
                'dataIndex': 'float Example',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'str Example',
                'dataIndex': 'str Example',
                'editable': True,
                'width': '25%',
            },
            {
                'title': 'Datetime Example',
                'dataIndex': 'Datetime Example',
                'editable': True,
                'width': '25%',
            },
        ],
        data=[
            {
                'key': f'row-{i}',
                'int Example': 123,
                'float Example': 1.23,
                'str Example': 'Example string',
                'Datetime Example': datetime.now().strftime(
                    '%Y-%m-%d %H:%M:%S'
                ),
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-editable-demo-output'),
]

...

@app.callback(
    Output('table-editable-demo-output', 'children'),
    [
        Input('table-editable-demo', 'recentlyChangedRow'),
        Input('table-editable-demo', 'recentlyChangedColumn'),
    ],
    prevent_initial_call=True,
)
def table_editable_demo(recentlyChangedRow, recentlyChangedColumn):
    return json.dumps(
        dict(
            recentlyChangedRow=recentlyChangedRow,
            recentlyChangedColumn=recentlyChangedColumn,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableBasic/demos/loading.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSwitch(id='table-loading', checked=False),
                fac.AntdTable(
                    id='table-loading-demo',
                    columns=[
                        {'title': 'int型示例', 'dataIndex': 'int型示例'},
                        {'title': 'float型示例', 'dataIndex': 'float型示例'},
                        {'title': 'str型示例', 'dataIndex': 'str型示例'},
                        {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
                    ],
                    data=[
                        {
                            'int型示例': 123,
                            'float型示例': 1.23,
                            'str型示例': '示例字符',
                            '日期时间示例': datetime.now(),
                        }
                    ]
                    * 3,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSwitch(id='table-loading', checked=False),
                fac.AntdTable(
                    id='table-loading-demo',
                    columns=[
                        {'title': 'int Example', 'dataIndex': 'int Example'},
                        {
                            'title': 'float Example',
                            'dataIndex': 'float Example',
                        },
                        {'title': 'str Example', 'dataIndex': 'str Example'},
                        {
                            'title': 'Datetime Example',
                            'dataIndex': 'Datetime Example',
                        },
                    ],
                    data=[
                        {
                            'int Example': 123,
                            'float Example': 1.23,
                            'str Example': 'Example string',
                            'Datetime Example': datetime.now(),
                        }
                    ]
                    * 3,
                    locale='en-us',
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


@app.callback(
    Output('table-loading-demo', 'loading'),
    Input('table-loading', 'checked'),
    prevent_initial_call=True,
)
def table_loading(checked):
    return checked


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(id='table-loading', checked=False),
        fac.AntdTable(
            id='table-loading-demo',
            columns=[
                {'title': 'int型示例', 'dataIndex': 'int型示例'},
                {'title': 'float型示例', 'dataIndex': 'float型示例'},
                {'title': 'str型示例', 'dataIndex': 'str型示例'},
                {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
            ],
            data=[
                {
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now(),
                }
            ]
            * 3,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('table-loading-demo', 'loading'),
    Input('table-loading', 'checked'),
    prevent_initial_call=True,
)
def table_loading(checked):
    return checked
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(id='table-loading', checked=False),
        fac.AntdTable(
            id='table-loading-demo',
            columns=[
                {'title': 'int Example', 'dataIndex': 'int Example'},
                {'title': 'float Example', 'dataIndex': 'float Example'},
                {'title': 'str Example', 'dataIndex': 'str Example'},
                {'title': 'Datetime Example', 'dataIndex': 'Datetime Example'},
            ],
            data=[
                {
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now(),
                }
            ]
            * 3,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('table-loading-demo', 'loading'),
    Input('table-loading', 'checked'),
    prevent_initial_call=True,
)
def table_loading(checked):
    return checked
"""
            }
        ]

```

### `views/AntdTableBasic/demos/max_height_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
            maxHeight=150,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 10,
            maxHeight=150,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    maxHeight=150,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 10,
    maxHeight=150,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/max_width_usage.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            html.Div(
                fac.AntdTable(
                    columns=[
                        {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
                    maxWidth=900,
                    title='maxWidth=900',
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdTable(
                columns=[
                    {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                    for i in range(1, 6)
                ],
                data=[{f'字段{i}': '示例内容' * 4 for i in range(1, 6)}] * 3,
                maxWidth='max-content',
                title='maxWidth="max-content"',
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            html.Div(
                fac.AntdTable(
                    columns=[
                        {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                        for i in range(1, 6)
                    ],
                    data=[
                        {f'Field {i}': 'Example Content' for i in range(1, 6)}
                    ]
                    * 3,
                    maxWidth=900,
                    title='maxWidth=900',
                    locale='en-us',
                ),
                style={'maxWidth': 700, 'margin': '0 auto'},
            ),
            fac.AntdTable(
                columns=[
                    {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                    for i in range(1, 6)
                ],
                data=[
                    {f'Field {i}': 'Example Content' * 4 for i in range(1, 6)}
                ]
                * 3,
                maxWidth='max-content',
                title='maxWidth="max-content"',
                locale='en-us',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    html.Div(
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            maxWidth=900,
            title='maxWidth=900',
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' * 4 for i in range(1, 6)}] * 3,
        maxWidth='max-content',
        title='maxWidth="max-content"',
    ),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    html.Div(
        fac.AntdTable(
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            maxWidth=900,
            title='maxWidth=900',
        ),
        style={'maxWidth': 700, 'margin': '0 auto'},
    ),
    fac.AntdTable(
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
            for i in range(1, 6)
        ],
        data=[{f'Field {i}': 'Example Content' * 4 for i in range(1, 6)}] * 3,
        maxWidth='max-content',
        title='maxWidth="max-content"',
    ),
]
"""
            }
        ]

```

### `views/AntdTableBasic/demos/nested_editable.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int型示例',
                    'dataIndex': 'int型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'float型示例',
                    'dataIndex': 'float型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'str型示例',
                    'dataIndex': 'str型示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': '日期时间示例',
                    'dataIndex': '日期时间示例',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'placeholder示例',
                    'dataIndex': 'placeholder示例',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'placeholder': '请输入内容'},
                },
            ],
            data=[
                {
                    'key': f'row-{i}',
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                    'children': [
                        {
                            'key': f'row-{i}-{j}',
                            'int型示例': 123,
                            'float型示例': 1.23,
                            'str型示例': '示例字符',
                            '日期时间示例': datetime.now().strftime(
                                '%Y-%m-%d %H:%M:%S'
                            ),
                        }
                        for j in range(1, 4)
                    ],
                }
                for i in range(1, 4)
            ],
            bordered=True,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'int Example',
                    'dataIndex': 'int Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'float Example',
                    'dataIndex': 'float Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'str Example',
                    'dataIndex': 'str Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'Datetime Example',
                    'dataIndex': 'Datetime Example',
                    'editable': True,
                    'width': '20%',
                },
                {
                    'title': 'Placeholder Example',
                    'dataIndex': 'Placeholder Example',
                    'editable': True,
                    'width': '20%',
                    'editOptions': {'placeholder': 'Please enter content'},
                },
            ],
            data=[
                {
                    'key': f'row-{i}',
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                    'children': [
                        {
                            'key': f'row-{i}-{j}',
                            'int Example': 123,
                            'float Example': 1.23,
                            'str Example': 'Example string',
                            'Datetime Example': datetime.now().strftime(
                                '%Y-%m-%d %H:%M:%S'
                            ),
                        }
                        for j in range(1, 4)
                    ],
                }
                for i in range(1, 4)
            ],
            bordered=True,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int型示例',
            'dataIndex': 'int型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float型示例',
            'dataIndex': 'float型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str型示例',
            'dataIndex': 'str型示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': '日期时间示例',
            'dataIndex': '日期时间示例',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'placeholder示例',
            'dataIndex': 'placeholder示例',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': '请输入内容'},
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int型示例': 123,
            'float型示例': 1.23,
            'str型示例': '示例字符',
            '日期时间示例': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
            'children': [
                {
                    'key': f'row-{i}-{j}',
                    'int型示例': 123,
                    'float型示例': 1.23,
                    'str型示例': '示例字符',
                    '日期时间示例': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
                for j in range(1, 4)
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'int Example',
            'dataIndex': 'int Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'float Example',
            'dataIndex': 'float Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'str Example',
            'dataIndex': 'str Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'Datetime Example',
            'dataIndex': 'Datetime Example',
            'editable': True,
            'width': '20%',
        },
        {
            'title': 'Placeholder Example',
            'dataIndex': 'Placeholder Example',
            'editable': True,
            'width': '20%',
            'editOptions': {'placeholder': 'Please enter content'},
        },
    ],
    data=[
        {
            'key': f'row-{i}',
            'int Example': 123,
            'float Example': 1.23,
            'str Example': 'Example string',
            'Datetime Example': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
            'children': [
                {
                    'key': f'row-{i}-{j}',
                    'int Example': 123,
                    'float Example': 1.23,
                    'str Example': 'Example string',
                    'Datetime Example': datetime.now().strftime(
                        '%Y-%m-%d %H:%M:%S'
                    ),
                }
                for j in range(1, 4)
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/numeric_column_width.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fac.AntdTable(
                columns=[
                    {
                        'title': f'字段{i}',
                        'dataIndex': f'字段{i}',
                        'width': width,
                    }
                    for i, width in zip(range(1, 6), [50, 100, 50, 100, 50])
                ],
                data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            ),
            fac.AntdTable(
                columns=[
                    {
                        'title': f'字段{i}',
                        'dataIndex': f'字段{i}',
                        'width': width,
                    }
                    for i, width in zip(
                        range(1, 6), [5000, 10000, 5000, 10000, 5000]
                    )
                ],
                data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fac.AntdTable(
                columns=[
                    {
                        'title': f'Field {i}',
                        'dataIndex': f'Field {i}',
                        'width': width,
                    }
                    for i, width in zip(range(1, 6), [50, 100, 50, 100, 50])
                ],
                data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}]
                * 3,
                locale='en-us',
            ),
            fac.AntdTable(
                columns=[
                    {
                        'title': f'Field {i}',
                        'dataIndex': f'Field {i}',
                        'width': width,
                    }
                    for i, width in zip(
                        range(1, 6), [5000, 10000, 5000, 10000, 5000]
                    )
                ],
                data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}]
                * 3,
                locale='en-us',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
            for i, width in zip(range(1, 6), [50, 100, 50, 100, 50])
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    ),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
            for i, width in zip(
                range(1, 6), [5000, 10000, 5000, 10000, 5000]
            )
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    ),
]
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': width}
            for i, width in zip(range(1, 6), [50, 100, 50, 100, 50])
        ],
        data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
    ),
    fac.AntdTable(
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': width}
            for i, width in zip(
                range(1, 6), [5000, 10000, 5000, 10000, 5000]
            )
        ],
        data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
    ),
]
"""
            }
        ]

```

### `views/AntdTableBasic/demos/percentage_column_width.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
                for i, width in zip(
                    range(1, 6), ['10%', '20%', '30%', '25%', '15%']
                )
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': f'Field {i}',
                    'dataIndex': f'Field {i}',
                    'width': width,
                }
                for i, width in zip(
                    range(1, 6), ['10%', '20%', '30%', '25%', '15%']
                )
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
            locale='en-us',
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': width}
        for i, width in zip(
            range(1, 6), ['10%', '20%', '30%', '25%', '15%']
        )
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
)
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': width}
        for i, width in zip(
            range(1, 6), ['10%', '20%', '30%', '25%', '15%']
        )
    ],
    data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 3,
)
"""
            }
        ]

```

### `views/AntdTableBasic/demos/row_class_name.py`
```python
from datetime import datetime

import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = [
            fuc.FefferyStyle(
                rawStyle="""
.table-row-class-name-demo {
    color: #1890ff;
    font-weight: bold;
}
"""
            ),
            fac.AntdTable(
                columns=[
                    {'title': 'int型示例', 'dataIndex': 'int型示例'},
                    {'title': 'float型示例', 'dataIndex': 'float型示例'},
                    {'title': 'str型示例', 'dataIndex': 'str型示例'},
                    {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
                ],
                data=[
                    {
                        'int型示例': 123,
                        'float型示例': 1.23,
                        'str型示例': '示例字符',
                        '日期时间示例': datetime.now(),
                    }
                ]
                * 3,
                rowClassName='table-row-class-name-demo',
            ),
        ]

    elif current_locale == 'en-us':
        demo_contents = [
            fuc.FefferyStyle(
                rawStyle="""
.table-row-class-name-demo {
    color: #1890ff;
    font-weight: bold;
}
"""
            ),
            fac.AntdTable(
                columns=[
                    {'title': 'int Example', 'dataIndex': 'int Example'},
                    {'title': 'float Example', 'dataIndex': 'float Example'},
                    {'title': 'str Example', 'dataIndex': 'str Example'},
                    {
                        'title': 'Datetime Example',
                        'dataIndex': 'Datetime Example',
                    },
                ],
                data=[
                    {
                        'int Example': 123,
                        'float Example': 1.23,
                        'str Example': 'Example string',
                        'Datetime Example': datetime.now(),
                    }
                ]
                * 3,
                rowClassName='table-row-class-name-demo',
                locale='en-us',
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
[
    fuc.FefferyStyle(
        rawStyle="""
.table-row-class-name-demo {
    color: #1890ff;
    font-weight: bold;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int型示例', 'dataIndex': 'int型示例'},
            {'title': 'float型示例', 'dataIndex': 'float型示例'},
            {'title': 'str型示例', 'dataIndex': 'str型示例'},
            {'title': '日期时间示例', 'dataIndex': '日期时间示例'},
        ],
        data=[
            {
                'int型示例': 123,
                'float型示例': 1.23,
                'str型示例': '示例字符',
                '日期时间示例': datetime.now(),
            }
        ]
        * 3,
        rowClassName='table-row-class-name-demo',
    ),
]
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
[
    fuc.FefferyStyle(
        rawStyle="""
.table-row-class-name-demo {
    color: #1890ff;
    font-weight: bold;
}
"""
    ),
    fac.AntdTable(
        columns=[
            {'title': 'int Example', 'dataIndex': 'int Example'},
            {'title': 'float Example', 'dataIndex': 'float Example'},
            {'title': 'str Example', 'dataIndex': 'str Example'},
            {'title': 'Datetime Example', 'dataIndex': 'Datetime Example'},
        ],
        data=[
            {
                'int Example': 123,
                'float Example': 1.23,
                'str Example': 'Example string',
                'Datetime Example': datetime.now(),
            }
        ]
        * 3,
        rowClassName='table-row-class-name-demo',
    ),
]
'''
            }
        ]

```

### `views/AntdTableBasic/demos/scroll_to_first_row_on_change.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdFormItem(
                    fac.AntdSwitch(
                        id='control-table-scroll-to-first-row-on-change-demo',
                        checked=True,
                    ),
                    label='scrollToFirstRowOnChange',
                ),
                fac.AntdTable(
                    id='table-scroll-to-first-row-on-change-demo',
                    columns=[
                        {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 50,
                    maxHeight=150,
                    scrollToFirstRowOnChange=False,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdFormItem(
                    fac.AntdSwitch(
                        id='control-table-scroll-to-first-row-on-change-demo',
                        checked=True,
                    ),
                    label='scrollToFirstRowOnChange',
                ),
                fac.AntdTable(
                    id='table-scroll-to-first-row-on-change-demo',
                    columns=[
                        {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                        for i in range(1, 6)
                    ],
                    data=[
                        {f'Field {i}': 'Example Content' for i in range(1, 6)}
                    ]
                    * 50,
                    maxHeight=150,
                    scrollToFirstRowOnChange=False,
                    locale='en-us',
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


@app.callback(
    Output(
        'table-scroll-to-first-row-on-change-demo', 'scrollToFirstRowOnChange'
    ),
    Input('control-table-scroll-to-first-row-on-change-demo', 'checked'),
)
def control_table_scroll_to_first_row_on_change(checked):
    return checked


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='control-table-scroll-to-first-row-on-change-demo',
                checked=True,
            ),
            label='scrollToFirstRowOnChange',
        ),
        fac.AntdTable(
            id='table-scroll-to-first-row-on-change-demo',
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 50,
            maxHeight=150,
            scrollToFirstRowOnChange=False,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output(
        'table-scroll-to-first-row-on-change-demo', 'scrollToFirstRowOnChange'
    ),
    Input('control-table-scroll-to-first-row-on-change-demo', 'checked'),
)
def control_table_scroll_to_first_row_on_change(checked):
    return checked
"""
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='control-table-scroll-to-first-row-on-change-demo',
                checked=True,
            ),
            label='scrollToFirstRowOnChange',
        ),
        fac.AntdTable(
            id='table-scroll-to-first-row-on-change-demo',
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Example Content' for i in range(1, 6)}] * 50,
            maxHeight=150,
            scrollToFirstRowOnChange=False,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output(
        'table-scroll-to-first-row-on-change-demo', 'scrollToFirstRowOnChange'
    ),
    Input('control-table-scroll-to-first-row-on-change-demo', 'checked'),
)
def control_table_scroll_to_first_row_on_change(checked):
    return checked
"""
            }
        ]

```

### `views/AntdTableBasic/demos/sizes.py`
```python
from datetime import datetime

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdDivider(
                            f'size="{size}"', innerTextOrientation='left'
                        ),
                        fac.AntdTable(
                            columns=[
                                {
                                    'title': 'int型示例',
                                    'dataIndex': 'int型示例',
                                },
                                {
                                    'title': 'float型示例',
                                    'dataIndex': 'float型示例',
                                },
                                {
                                    'title': 'str型示例',
                                    'dataIndex': 'str型示例',
                                },
                                {
                                    'title': '日期时间示例',
                                    'dataIndex': '日期时间示例',
                                },
                            ],
                            data=[
                                {
                                    'int型示例': 123,
                                    'float型示例': 1.23,
                                    'str型示例': '示例字符',
                                    '日期时间示例': datetime.now(),
                                }
                            ],
                            size=size,
                            bordered=True,
                        ),
                    ],
                    direction='vertical',
                    style={'width': '100%'},
                )
                for size in ['small', 'middle', 'large']
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdDivider(
                            f'size="{size}"', innerTextOrientation='left'
                        ),
                        fac.AntdTable(
                            columns=[
                                {
                                    'title': 'int Example',
                                    'dataIndex': 'int Example',
                                },
                                {
                                    'title': 'float Example',
                                    'dataIndex': 'float Example',
                                },
                                {
                                    'title': 'str Example',
                                    'dataIndex': 'str Example',
                                },
                                {
                                    'title': 'Datetime Example',
                                    'dataIndex': 'Datetime Example',
                                },
                            ],
                            data=[
                                {
                                    'int Example': 123,
                                    'float Example': 1.23,
                                    'str Example': 'Example string',
                                    'Datetime Example': datetime.now(),
                                }
                            ],
                            size=size,
                            bordered=True,
                            locale='en-us',
                        ),
                    ],
                    direction='vertical',
                    style={'width': '100%'},
                )
                for size in ['small', 'middle', 'large']
            ],
            direction='vertical',
            style={'width': '100%'},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    f'size="{size}"', innerTextOrientation='left'
                ),
                fac.AntdTable(
                    columns=[
                        {'title': 'int型示例', 'dataIndex': 'int型示例'},
                        {
                            'title': 'float型示例',
                            'dataIndex': 'float型示例',
                        },
                        {'title': 'str型示例', 'dataIndex': 'str型示例'},
                        {
                            'title': '日期时间示例',
                            'dataIndex': '日期时间示例',
                        },
                    ],
                    data=[
                        {
                            'int型示例': 123,
                            'float型示例': 1.23,
                            'str型示例': '示例字符',
                            '日期时间示例': datetime.now(),
                        }
                    ],
                    size=size,
                    bordered=True,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for size in ['small', 'middle', 'large']
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
        fac.AntdSpace(
            [
                fac.AntdDivider(
                    f'size="{size}"', innerTextOrientation='left'
                ),
                fac.AntdTable(
                    columns=[
                        {'title': 'int Example', 'dataIndex': 'int Example'},
                        {
                            'title': 'float Example',
                            'dataIndex': 'float Example',
                        },
                        {'title': 'str Example', 'dataIndex': 'str Example'},
                        {
                            'title': 'Datetime Example',
                            'dataIndex': 'Datetime Example',
                        },
                    ],
                    data=[
                        {
                            'int Example': 123,
                            'float Example': 1.23,
                            'str Example': 'Example string',
                            'Datetime Example': datetime.now(),
                        }
                    ],
                    size=size,
                    bordered=True,
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
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
