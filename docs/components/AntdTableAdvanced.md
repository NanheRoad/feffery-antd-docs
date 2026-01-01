# AntdTableAdvanced

## 简介源码：`views/AntdTableAdvanced/intro.py`
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
                {'title': translator.t('进阶功能')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件主要进阶功能示例。')),
    ]

```

## 示例源码（demos）

### `views/AntdTableAdvanced/demos/columns_format_constraint.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': '纯数字约束',
                    'dataIndex': '纯数字约束',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': '纯字母约束',
                    'dataIndex': '纯字母约束',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': '日期格式约束',
                    'dataIndex': '日期格式约束',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': '纯汉字约束',
                    'dataIndex': '纯汉字约束',
                    'editable': True,
                    'width': '25%',
                },
            ],
            data=[
                {
                    '纯数字约束': '12345',
                    '纯字母约束': 'fac',
                    '日期格式约束': '2099-01-01',
                    '纯汉字约束': '测试',
                }
            ],
            columnsFormatConstraint={
                '纯数字约束': {
                    'rule': '^[0-9]+$',
                    'content': '不符合纯数字输入要求',
                },
                '纯字母约束': {
                    'rule': '^[a-zA-Z]+$',
                    'content': '不符合纯字母输入要求',
                },
                '日期格式约束': {
                    'rule': '^\\d{4}-\\d{2}-\\d{2}$',
                    'content': '不符合日期格式输入要求',
                },
                '纯汉字约束': {
                    'rule': '^[一-龥]+$',
                    'content': '不符合纯汉字输入要求',
                },
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents (dataIndex translated too)
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'Digits-only Constraint',
                    'dataIndex': 'Digits-only Constraint',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': 'Letters-only Constraint',
                    'dataIndex': 'Letters-only Constraint',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': 'Date Format Constraint',
                    'dataIndex': 'Date Format Constraint',
                    'editable': True,
                    'width': '25%',
                },
                {
                    'title': 'Chinese-characters-only Constraint',
                    'dataIndex': 'Chinese-characters-only Constraint',
                    'editable': True,
                    'width': '25%',
                },
            ],
            data=[
                {
                    'Digits-only Constraint': '12345',
                    'Letters-only Constraint': 'fac',
                    'Date Format Constraint': '2099-01-01',
                    'Chinese-characters-only Constraint': '测试',
                }
            ],
            columnsFormatConstraint={
                'Digits-only Constraint': {
                    'rule': '^[0-9]+$',
                    'content': 'Input must be digits-only.',
                },
                'Letters-only Constraint': {
                    'rule': '^[a-zA-Z]+$',
                    'content': 'Input must be letters-only.',
                },
                'Date Format Constraint': {
                    'rule': '^\\d{4}-\\d{2}-\\d{2}$',
                    'content': 'Input must match the date format YYYY-MM-DD.',
                },
                'Chinese-characters-only Constraint': {
                    'rule': '^[一-龥]+$',
                    'content': 'Input must be Chinese characters only.',
                },
            },
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
        {'title': '纯数字约束', 'dataIndex': '纯数字约束', 'editable': True, 'width': '25%'},
        {'title': '纯字母约束', 'dataIndex': '纯字母约束', 'editable': True, 'width': '25%'},
        {'title': '日期格式约束', 'dataIndex': '日期格式约束', 'editable': True, 'width': '25%'},
        {'title': '纯汉字约束', 'dataIndex': '纯汉字约束', 'editable': True, 'width': '25%'},
    ],
    data=[
        {'纯数字约束': '12345', '纯字母约束': 'fac', '日期格式约束': '2099-01-01', '纯汉字约束': '测试'}
    ],
    columnsFormatConstraint={
        '纯数字约束': {'rule': '^[0-9]+$', 'content': '不符合纯数字输入要求'},
        '纯字母约束': {'rule': '^[a-zA-Z]+$', 'content': '不符合纯字母输入要求'},
        '日期格式约束': {'rule': '^\\\\d{4}-\\\\d{2}-\\\\d{2}$', 'content': '不符合日期格式输入要求'},
        '纯汉字约束': {'rule': '^[一-龥]+$', 'content': '不符合纯汉字输入要求'},
    },
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
        {'title': 'Digits-only Constraint', 'dataIndex': 'Digits-only Constraint', 'editable': True, 'width': '25%'},
        {'title': 'Letters-only Constraint', 'dataIndex': 'Letters-only Constraint', 'editable': True, 'width': '25%'},
        {'title': 'Date Format Constraint', 'dataIndex': 'Date Format Constraint', 'editable': True, 'width': '25%'},
        {'title': 'Chinese-characters-only Constraint', 'dataIndex': 'Chinese-characters-only Constraint', 'editable': True, 'width': '25%'},
    ],
    data=[
        {'Digits-only Constraint': '12345', 'Letters-only Constraint': 'fac', 'Date Format Constraint': '2099-01-01', 'Chinese-characters-only Constraint': '测试'}
    ],
    columnsFormatConstraint={
        'Digits-only Constraint': {'rule': '^[0-9]+$', 'content': 'Input must be digits-only.'},
        'Letters-only Constraint': {'rule': '^[a-zA-Z]+$', 'content': 'Input must be letters-only.'},
        'Date Format Constraint': {'rule': '^\\\\d{4}-\\\\d{2}-\\\\d{2}$', 'content': 'Input must match the date format YYYY-MM-DD.'},
        'Chinese-characters-only Constraint': {'rule': '^[一-龥]+$', 'content': 'Input must be Chinese characters only.'},
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/conditional_style.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 构造演示用例相关内容
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': '示例字段1',
                    'dataIndex': '示例字段1',
                    'width': '100',
                },
                {
                    'title': '示例字段2',
                    'dataIndex': '示例字段2',
                    'width': '100',
                },
                {
                    'title': '示例字段3',
                    'dataIndex': '示例字段3',
                    'width': '100',
                },
            ],
            data=[
                {
                    '示例字段1': i,
                    '示例字段2': i,
                    '示例字段3': round(np.random.rand(), 3),
                }
                for i in range(10)
            ],
            bordered=True,
            conditionalStyleFuncs={
                '示例字段1': """
(record, index) => {
    if ( index % 2 === 1 ) {
        return {
            style: {
                backgroundColor: "#ebfbee"
            }
        }
    }
}
""",
                '示例字段2': """
(record, index) => {
    if ( index % 2 === 1 ) {
        return {
            style: {
                color: "red"
            }
        }
    }
}
""",
                '示例字段3': """
(record, index) => {
    if ( record['示例字段3'] <= 0.5 ) {
        return {
            style: {
                background: `linear-gradient(90deg, rgb(61, 153, 112) 0%, rgb(61, 153, 112) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
                backgroundClip: 'padding-box'
            }
        };
    }
    return {
        style: {
            background: `linear-gradient(90deg, rgb(255, 65, 54) 0%, rgb(255, 65, 54) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
            backgroundClip: 'padding-box'
        }
    };
}
""",
            },
        )

    elif current_locale == 'en-us':
        # construct demo contents (dataIndex translated too)
        demo_contents = fac.AntdTable(
            columns=[
                {
                    'title': 'Example Field 1',
                    'dataIndex': 'Example Field 1',
                    'width': '100',
                },
                {
                    'title': 'Example Field 2',
                    'dataIndex': 'Example Field 2',
                    'width': '100',
                },
                {
                    'title': 'Example Field 3',
                    'dataIndex': 'Example Field 3',
                    'width': '100',
                },
            ],
            data=[
                {
                    'Example Field 1': i,
                    'Example Field 2': i,
                    'Example Field 3': round(np.random.rand(), 3),
                }
                for i in range(10)
            ],
            bordered=True,
            conditionalStyleFuncs={
                'Example Field 1': """
(record, index) => {
    if ( index % 2 === 1 ) {
        return {
            style: {
                backgroundColor: "#ebfbee"
            }
        }
    }
}
""",
                'Example Field 2': """
(record, index) => {
    if ( index % 2 === 1 ) {
        return {
            style: {
                color: "red"
            }
        }
    }
}
""",
                'Example Field 3': """
(record, index) => {
    if ( record['Example Field 3'] <= 0.5 ) {
        return {
            style: {
                background: `linear-gradient(90deg, rgb(61, 153, 112) 0%, rgb(61, 153, 112) ${record['Example Field 3']*100}%, white ${record['Example Field 3']*100}%, white 100%)`,
                backgroundClip: 'padding-box'
            }
        };
    }
    return {
        style: {
            background: `linear-gradient(90deg, rgb(255, 65, 54) 0%, rgb(255, 65, 54) ${record['Example Field 3']*100}%, white ${record['Example Field 3']*100}%, white 100%)`,
            backgroundClip: 'padding-box'
        }
    };
}
""",
            },
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
import numpy as np
fac.AntdTable(
    columns=[
        {"title": "示例字段1", "dataIndex": "示例字段1", "width": "100"},
        {"title": "示例字段2", "dataIndex": "示例字段2", "width": "100"},
        {"title": "示例字段3", "dataIndex": "示例字段3", "width": "100"},
    ],
    data=[
        {"示例字段1": i, "示例字段2": i, "示例字段3": round(np.random.rand(), 3)}
        for i in range(10)
    ],
    bordered=True,
    conditionalStyleFuncs={{
        "示例字段1": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { backgroundColor: "#ebfbee" } }
    }
}
""",
        "示例字段2": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { color: "red" } }
    }
}
""",
        "示例字段3": """
(record, index) => {
    if ( record['示例字段3'] <= 0.5 ) {
        return {
            style: {
                background: `linear-gradient(90deg, rgb(61, 153, 112) 0%, rgb(61, 153, 112) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
                backgroundClip: 'padding-box'
            }
        };
    }
    return {
        style: {
            background: `linear-gradient(90deg, rgb(255, 65, 54) 0%, rgb(255, 65, 54) ${record['示例字段3']*100}%, white ${record['示例字段3']*100}%, white 100%)`,
            backgroundClip: 'padding-box'
        }
    };
}
""",
    }},
)
'''
            }
        ]

    elif current_locale == 'en-us':
        return [
            {
                'code': '''
import numpy as np
fac.AntdTable(
    columns=[
        {"title": "Example Field 1", "dataIndex": "Example Field 1", "width": "100"},
        {"title": "Example Field 2", "dataIndex": "Example Field 2", "width": "100"},
        {"title": "Example Field 3", "dataIndex": "Example Field 3", "width": "100"},
    ],
    data=[
        {"Example Field 1": i, "Example Field 2": i, "Example Field 3": round(np.random.rand(), 3)}
        for i in range(10)
    ],
    bordered=True,
    conditionalStyleFuncs={{
        "Example Field 1": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { backgroundColor: "#ebfbee" } }
    }
}
""",
        "Example Field 2": """
(record, index) => {
    if ( index % 2 === 1 ) {
        return { style: { color: "red" } }
    }
}
""",
        "Example Field 3": """
(record, index) => {
    if ( record['Example Field 3'] <= 0.5 ) {
        return {
            style: {
                background: `linear-gradient(90deg, rgb(61, 153, 112) 0%, rgb(61, 153, 112) ${record['Example Field 3']*100}%, white ${record['Example Field 3']*100}%, white 100%)`,
                backgroundClip: 'padding-box'
            }
        };
    }
    return {
        style: {
            background: `linear-gradient(90deg, rgb(255, 65, 54) 0%, rgb(255, 65, 54) ${record['Example Field 3']*100}%, white ${record['Example Field 3']*100}%, white 100%)`,
            backgroundClip: 'padding-box'
        }
    };
}
""",
    }},
)
'''
            }
        ]

```

### `views/AntdTableAdvanced/demos/container_id.py`
```python
import feffery_antd_components as fac
import numpy as np
from dash import html
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    # Locale-dependent labels and keys
    if current_locale == 'zh-cn':
        title_text = '左例（未设置） 右例（设置containerId参数）'
        column_label = lambda i: f'字段{i}'
        data_key = lambda j: f'字段{j}'
        filter_key1 = '字段1'
        filter_key3 = '字段3'
    elif current_locale == 'en-us':
        title_text = 'Left (unset)  Right (set containerId parameter)'
        column_label = lambda i: f'Field {i}'
        data_key = lambda j: f'Field {j}'
        filter_key1 = 'Field 1'
        filter_key3 = 'Field 3'
    else:
        # Fallback to Chinese
        title_text = '左例（未设置） 右例（设置containerId参数）'
        column_label = lambda i: f'字段{i}'
        data_key = lambda j: f'字段{j}'
        filter_key1 = '字段1'
        filter_key3 = '字段3'

    def make_table(with_container: bool) -> Component:
        base = dict(
            columns=[
                {'title': column_label(i), 'dataIndex': column_label(i)}
                for i in range(1, 6)
            ],
            data=[
                {
                    data_key(j): np.random.choice(list('abc'))
                    for j in range(1, 6)
                }
                for _ in range(10)
            ],
            filterOptions={
                filter_key1: {'filterMode': 'keyword'},
                filter_key3: {
                    'filterMode': 'checkbox',
                    'filterCustomItems': ['a', 'b', 'c'],
                },
            },
        )
        if with_container:
            base['containerId'] = 'containerId-container-demo'
        return fac.AntdTable(**base)

    demo_contents = [
        fac.AntdTitle(title_text, level=5),
        html.Div(
            [
                html.Div(
                    [
                        make_table(with_container=False),
                        html.Div(style={'height': '400px'}),
                    ],
                    style={
                        'flex': '1',
                        'padding': '20px',
                        'maxHeight': '400px',
                        'overflowY': 'auto',
                    },
                ),
                html.Div(
                    [
                        make_table(with_container=True),
                        html.Div(style={'height': '400px'}),
                    ],
                    id='containerId-container-demo',
                    style={
                        'flex': '1',
                        'padding': '20px',
                        'maxHeight': '400px',
                        'overflowY': 'auto',
                        'position': 'relative',
                    },
                ),
            ],
            style={'display': 'flex'},
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
    fac.AntdTitle('左例（未设置） 右例（设置containerId参数）', level=5),
    html.Div(
        [
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'字段{j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            '字段1': {'filterMode': 'keyword'},
                            '字段3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                },
            ),
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'字段{j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            '字段1': {'filterMode': 'keyword'},
                            '字段3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                        containerId='containerId-container-demo',
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                id='containerId-container-demo',
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                    'position': 'relative',
                },
            ),
        ],
        style={'display': 'flex'},
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
    fac.AntdTitle('Left (unset)  Right (set containerId parameter)', level=5),
    html.Div(
        [
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'Field {j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            'Field 1': {'filterMode': 'keyword'},
                            'Field 3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                },
            ),
            html.Div(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                            for i in range(1, 6)
                        ],
                        data=[
                            {
                                f'Field {j}': np.random.choice(list('abc'))
                                for j in range(1, 6)
                            }
                            for i in range(10)
                        ],
                        filterOptions={
                            'Field 1': {'filterMode': 'keyword'},
                            'Field 3': {
                                'filterMode': 'checkbox',
                                'filterCustomItems': ['a', 'b', 'c'],
                            },
                        },
                        containerId='containerId-container-demo',
                    ),
                    html.Div(style={'height': '400px'}),
                ],
                id='containerId-container-demo',
                style={
                    'flex': '1',
                    'padding': '20px',
                    'maxHeight': '400px',
                    'overflowY': 'auto',
                    'position': 'relative',
                },
            ),
        ],
        style={'display': 'flex'},
    ),
]
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/custom_empty_content.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        empty_desc = fac.AntdText('没有数据哦~', type='secondary')
    elif current_locale == 'en-us':
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        empty_desc = fac.AntdText('No data ~', type='secondary')
    else:
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        empty_desc = fac.AntdText('没有数据哦~', type='secondary')

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        emptyContent=fac.AntdEmpty(
            image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
            description=empty_desc,
            styles={'image': {'height': 150}},
        ),
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    emptyContent=fac.AntdEmpty(
        image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
        description=fac.AntdText('没有数据哦~', type='secondary'),
        styles={'image': {'height': 150}},
    ),
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
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    emptyContent=fac.AntdEmpty(
        image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
        description=fac.AntdText('No data ~', type='secondary'),
        styles={'image': {'height': 150}},
    ),
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/expand_basic.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'
    elif current_locale == 'en-us':
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        btn_text = lambda i: f'Expanded content for row {i}'
    else:
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': 400}
            for i in range(5)
        ],
        data=[
            {**{data_key(j): i for j in range(5)}, 'key': f'row-{i}'}
            for i in range(10)
        ],
        bordered=True,
        expandedRowKeyToContent=[
            {
                'key': f'row-{i}',
                'content': fac.AntdButton(btn_text(i), type='primary'),
            }
            for i in range(0, 10, 2)
        ],
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
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
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'Field {j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'Expanded content for row {i}', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/expand_by_click.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'
    elif current_locale == 'en-us':
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        btn_text = lambda i: f'Expanded content for row {i}'
    else:
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': 400}
            for i in range(5)
        ],
        data=[
            {**{data_key(j): i for j in range(5)}, 'key': f'row-{i}'}
            for i in range(10)
        ],
        bordered=True,
        expandedRowKeyToContent=[
            {
                'key': f'row-{i}',
                'content': fac.AntdButton(btn_text(i), type='primary'),
            }
            for i in range(0, 10, 2)
        ],
        expandRowByClick=True,
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    expandRowByClick=True,
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
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'Field {j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'Expanded content for row {i}', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    expandRowByClick=True,
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/expand_default.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'
    elif current_locale == 'en-us':
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        btn_text = lambda i: f'Expanded content for row {i}'
    else:
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        btn_text = lambda i: f'第{i}行展开内容示例'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': 400}
            for i in range(5)
        ],
        data=[
            {**{data_key(j): i for j in range(5)}, 'key': f'row-{i}'}
            for i in range(10)
        ],
        bordered=True,
        expandedRowKeyToContent=[
            {
                'key': f'row-{i}',
                'content': fac.AntdButton(btn_text(i), type='primary'),
            }
            for i in range(0, 10, 2)
        ],
        defaultExpandedRowKeys=['row-2', 'row-6'],
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'字段{j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'第{i}行展开内容示例', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    defaultExpandedRowKeys=['row-2', 'row-6'],
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
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': 400}
        for i in range(5)
    ],
    data=[
        {**{f'Field {j}': i for j in range(5)}, 'key': f'row-{i}'}
        for i in range(10)
    ],
    bordered=True,
    expandedRowKeyToContent=[
        {
            'key': f'row-{i}',
            'content': fac.AntdButton(
                f'Expanded content for row {i}', type='primary'
            ),
        }
        for i in range(0, 10, 2)
    ],
    defaultExpandedRowKeys=['row-2', 'row-6'],
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/filter_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        # 列名 & 键
        titles = [
            '基础示例',
            '自定义选项',
            '单选模式',
            '启用搜索框',
            '搜索型筛选',
        ]
        keys = titles  # 与标题一致
    elif current_locale == 'en-us':
        titles = [
            'Basic Example',
            'Custom Options',
            'Single Selection',
            'Enable Search Box',
            'Search Filter',
        ]
        keys = titles
    else:
        titles = [
            '基础示例',
            '自定义选项',
            '单选模式',
            '启用搜索框',
            '搜索型筛选',
        ]
        keys = titles

    columns = [
        {'title': t, 'dataIndex': k, 'width': '20%'}
        for t, k in zip(titles, keys)
    ]
    data = [
        {keys[0]: s, keys[1]: s, keys[2]: s, keys[3]: s, keys[4]: s}
        for s in list('abced')
    ]
    filter_options = {
        keys[0]: {},
        keys[1]: {'filterCustomItems': list('abcdefghijk')},
        keys[2]: {'filterMultiple': False},
        keys[3]: {'filterSearch': True},
        keys[4]: {'filterMode': 'keyword'},
    }

    demo_contents = [
        fac.AntdTable(
            id='table-filter-demo',
            columns=columns,
            data=data,
            filterOptions=filter_options,
        ),
        html.Pre(id='table-filter-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('table-filter-demo-output', 'children'),
    Input('table-filter-demo', 'filter'),
    prevent_initial_call=True,
)
def table_filter_demo(filter_):
    return json.dumps(filter_, indent=4, ensure_ascii=False)


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-filter-demo',
        columns=[
            {'title': '基础示例', 'dataIndex': '基础示例', 'width': '20%'},
            {'title': '自定义选项', 'dataIndex': '自定义选项', 'width': '20%'},
            {'title': '单选模式', 'dataIndex': '单选模式', 'width': '20%'},
            {'title': '启用搜索框', 'dataIndex': '启用搜索框', 'width': '20%'},
            {'title': '搜索型筛选', 'dataIndex': '搜索型筛选', 'width': '20%'},
        ],
        data=[
            {
                '基础示例': s,
                '自定义选项': s,
                '单选模式': s,
                '启用搜索框': s,
                '搜索型筛选': s,
            }
            for s in list('abced')
        ],
        filterOptions={{
            '基础示例': {{}},
            '自定义选项': {{'filterCustomItems': list('abcdefghijk')}},
            '单选模式': {{'filterMultiple': False}},
            '启用搜索框': {{'filterSearch': True}},
            '搜索型筛选': {{'filterMode': 'keyword'}},
        }},
    ),
    html.Pre(id='table-filter-demo-output'),
]

# ...

@app.callback(
    Output('table-filter-demo-output', 'children'),
    Input('table-filter-demo', 'filter'),
    prevent_initial_call=True,
)
def table_filter_demo(filter_):
    return json.dumps(filter_, indent=4, ensure_ascii=False)
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-filter-demo',
        columns=[
            {'title': 'Basic Example', 'dataIndex': 'Basic Example', 'width': '20%'},
            {'title': 'Custom Options', 'dataIndex': 'Custom Options', 'width': '20%'},
            {'title': 'Single Selection', 'dataIndex': 'Single Selection', 'width': '20%'},
            {'title': 'Enable Search Box', 'dataIndex': 'Enable Search Box', 'width': '20%'},
            {'title': 'Search Filter', 'dataIndex': 'Search Filter', 'width': '20%'},
        ],
        data=[
            {
                'Basic Example': s,
                'Custom Options': s,
                'Single Selection': s,
                'Enable Search Box': s,
                'Search Filter': s,
            }
            for s in list('abced')
        ],
        filterOptions={{
            'Basic Example': {{}},
            'Custom Options': {{'filterCustomItems': list('abcdefghijk')}},
            'Single Selection': {{'filterMultiple': False}},
            'Enable Search Box': {{'filterSearch': True}},
            'Search Filter': {{'filterMode': 'keyword'}},
        }},
    ),
    html.Pre(id='table-filter-demo-output'),
]

# ...

@app.callback(
    Output('table-filter-demo-output', 'children'),
    Input('table-filter-demo', 'filter'),
    prevent_initial_call=True,
)
def table_filter_demo(filter_):
    return json.dumps(filter_, indent=4, ensure_ascii=False)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/filter_checkbox.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        titles = [
            '基础示例',
            '自定义选项',
            '单选模式',
            '启用搜索框',
            '树形筛选',
        ]
        keys = titles
    elif current_locale == 'en-us':
        titles = [
            'Basic Example',
            'Custom Options',
            'Single Selection',
            'Enable Search Box',
            'Tree Filter',
        ]
        keys = titles
    else:
        titles = [
            '基础示例',
            '自定义选项',
            '单选模式',
            '启用搜索框',
            '树形筛选',
        ]
        keys = titles

    columns = [
        {'title': t, 'dataIndex': k, 'width': '20%'}
        for t, k in zip(titles, keys)
    ]
    data = [
        {keys[0]: s, keys[1]: s, keys[2]: s, keys[3]: s, keys[4]: s}
        for s in list('abced')
    ]
    filter_options = {
        keys[0]: {},
        keys[1]: {'filterCustomItems': list('abcdefghijk')},
        keys[2]: {'filterMultiple': False},
        keys[3]: {'filterSearch': True},
        keys[4]: {
            'filterMode': 'tree',
            'filterCustomTreeItems': [
                {
                    'text': 'a-c',
                    'children': [{'text': s, 'value': s} for s in list('abc')],
                },
                {'text': 'd', 'value': 'd'},
                {'text': 'e', 'value': 'e'},
            ],
        },
    }

    demo_contents = fac.AntdTable(
        columns=columns, data=data, filterOptions=filter_options
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
        {'title': '基础示例', 'dataIndex': '基础示例', 'width': '20%'},
        {'title': '自定义选项', 'dataIndex': '自定义选项', 'width': '20%'},
        {'title': '单选模式', 'dataIndex': '单选模式', 'width': '20%'},
        {'title': '启用搜索框', 'dataIndex': '启用搜索框', 'width': '20%'},
        {'title': '树形筛选', 'dataIndex': '树形筛选', 'width': '20%'},
    ],
    data=[
        {
            '基础示例': s,
            '自定义选项': s,
            '单选模式': s,
            '启用搜索框': s,
            '树形筛选': s,
        }
        for s in list('abced')
    ],
    filterOptions={
        '基础示例': {},
        '自定义选项': {'filterCustomItems': list('abcdefghijk')},
        '单选模式': {'filterMultiple': False},
        '启用搜索框': {'filterSearch': True},
        '树形筛选': {
            'filterMode': 'tree',
            'filterCustomTreeItems': [
                {'text': 'a-c', 'children': [{'text': s, 'value': s} for s in list('abc')]},
                {'text': 'd', 'value': 'd'},
                {'text': 'e', 'value': 'e'},
            ],
        },
    },
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
        {'title': 'Basic Example', 'dataIndex': 'Basic Example', 'width': '20%'},
        {'title': 'Custom Options', 'dataIndex': 'Custom Options', 'width': '20%'},
        {'title': 'Single Selection', 'dataIndex': 'Single Selection', 'width': '20%'},
        {'title': 'Enable Search Box', 'dataIndex': 'Enable Search Box', 'width': '20%'},
        {'title': 'Tree Filter', 'dataIndex': 'Tree Filter', 'width': '20%'},
    ],
    data=[
        {
            'Basic Example': s,
            'Custom Options': s,
            'Single Selection': s,
            'Enable Search Box': s,
            'Tree Filter': s,
        }
        for s in list('abced')
    ],
    filterOptions={
        'Basic Example': {},
        'Custom Options': {'filterCustomItems': list('abcdefghijk')},
        'Single Selection': {'filterMultiple': False},
        'Enable Search Box': {'filterSearch': True},
        'Tree Filter': {
            'filterMode': 'tree',
            'filterCustomTreeItems': [
                {'text': 'a-c', 'children': [{'text': s, 'value': s} for s in list('abc')]},
                {'text': 'd', 'value': 'd'},
                {'text': 'e', 'value': 'e'},
            ],
        },
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/filter_default_filtered_values.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        col_title = '基础示例'
        data_key = '基础示例'
    elif current_locale == 'en-us':
        col_title = 'Basic Example'
        data_key = 'Basic Example'
    else:
        col_title = '基础示例'
        data_key = '基础示例'

    demo_contents = fac.AntdTable(
        columns=[{'title': col_title, 'dataIndex': data_key}],
        data=[{data_key: s} for s in list('abced')],
        filterOptions={data_key: {}},
        defaultFilteredValues={data_key: ['a', 'c', 'e']},
        style={'width': 200},
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
    columns=[{'title': '基础示例', 'dataIndex': '基础示例'}],
    data=[{'基础示例': s} for s in list('abced')],
    filterOptions={'基础示例': {}},
    defaultFilteredValues={'基础示例': ['a', 'c', 'e']},
    style={'width': 200},
)
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[{'title': 'Basic Example', 'dataIndex': 'Basic Example'}],
    data=[{'Basic Example': s} for s in list('abced')],
    filterOptions={'Basic Example': {}},
    defaultFilteredValues={'Basic Example': ['a', 'c', 'e']},
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/filter_keyword.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        col_title = '搜索型筛选'
        data_key = '搜索型筛选'
    elif current_locale == 'en-us':
        col_title = 'Search Filter'
        data_key = 'Search Filter'
    else:
        col_title = '搜索型筛选'
        data_key = '搜索型筛选'

    demo_contents = fac.AntdTable(
        columns=[{'title': col_title, 'dataIndex': data_key}],
        data=[{data_key: s} for s in list('abced')],
        filterOptions={data_key: {'filterMode': 'keyword'}},
        style={'width': 200},
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
    columns=[{'title': '搜索型筛选', 'dataIndex': '搜索型筛选'}],
    data=[{'搜索型筛选': s} for s in list('abced')],
    filterOptions={'搜索型筛选': {'filterMode': 'keyword'}},
    style={'width': 200},
)
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[{'title': 'Search Filter', 'dataIndex': 'Search Filter'}],
    data=[{'Search Filter': s} for s in list('abced')],
    filterOptions={'Search Filter': {'filterMode': 'keyword'}},
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/listen_cell_click.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        col_label = lambda i: f'字段{i}'
        cell_value = lambda i, row: f'字段{i}第{row}行'
    else:  # en-us (fallback to en)
        col_label = lambda i: f'Field {i}'
        cell_value = lambda i, row: f'Field {i} Row {row}'

    columns = [
        {'title': col_label(i), 'dataIndex': col_label(i), 'width': '20%'}
        for i in range(1, 6)
    ]

    data = [
        {
            'key': f'row-{row}',
            **{col_label(i): cell_value(i, row) for i in range(1, 6)},
        }
        for row in range(1, 6)
    ]

    demo_contents = [
        fac.AntdTable(
            id='table-click-event-demo',
            columns=columns,
            data=data,
            bordered=True,
            # listen on 1,3,5
            enableCellClickListenColumns=[col_label(i) for i in range(1, 6, 2)],
        ),
        html.Pre(id='table-click-event-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('table-click-event-demo-output', 'children'),
    [
        Input('table-click-event-demo', 'nClicksCell'),
        Input('table-click-event-demo', 'nDoubleClicksCell'),
    ],
    [
        State('table-click-event-demo', 'enableCellClickListenColumns'),
        State('table-click-event-demo', 'recentlyCellClickColumn'),
        State('table-click-event-demo', 'recentlyCellClickRecord'),
        State('table-click-event-demo', 'recentlyCellDoubleClickColumn'),
        State('table-click-event-demo', 'recentlyCellDoubleClickRecord'),
    ],
    prevent_initial_call=True,
)
def table_click_event_demo(
    nClicksCell,
    nDoubleClicksCell,
    enableCellClickListenColumns,
    recentlyCellClickColumn,
    recentlyCellClickRecord,
    recentlyCellDoubleClickColumn,
    recentlyCellDoubleClickRecord,
):
    return json.dumps(
        dict(
            enableCellClickListenColumns=enableCellClickListenColumns,
            nClicksCell=nClicksCell,
            recentlyCellClickColumn=recentlyCellClickColumn,
            recentlyCellClickRecord=recentlyCellClickRecord,
            nDoubleClicksCell=nDoubleClicksCell,
            recentlyCellDoubleClickColumn=recentlyCellDoubleClickColumn,
            recentlyCellDoubleClickRecord=recentlyCellDoubleClickRecord,
        ),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    from i18n import get_current_locale

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-click-event-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {
                'key': f'row-{row}',
                **{f'字段{i}': f'字段{i}第{row}行' for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableCellClickListenColumns=[f'字段{i}' for i in range(1, 6, 2)],
    ),
    html.Pre(id='table-click-event-demo-output'),
]

# ...

@app.callback(
    Output('table-click-event-demo-output', 'children'),
    [
        Input('table-click-event-demo', 'nClicksCell'),
        Input('table-click-event-demo', 'nDoubleClicksCell'),
    ],
    [
        State('table-click-event-demo', 'enableCellClickListenColumns'),
        State('table-click-event-demo', 'recentlyCellClickColumn'),
        State('table-click-event-demo', 'recentlyCellClickRecord'),
        State('table-click-event-demo', 'recentlyCellDoubleClickColumn'),
        State('table-click-event-demo', 'recentlyCellDoubleClickRecord'),
    ],
    prevent_initial_call=True,
)
def table_click_event_demo(
    nClicksCell,
    nDoubleClicksCell,
    enableCellClickListenColumns,
    recentlyCellClickColumn,
    recentlyCellClickRecord,
    recentlyCellDoubleClickColumn,
    recentlyCellDoubleClickRecord,
):
    return json.dumps(
        dict(
            enableCellClickListenColumns=enableCellClickListenColumns,
            nClicksCell=nClicksCell,
            recentlyCellClickColumn=recentlyCellClickColumn,
            recentlyCellClickRecord=recentlyCellClickRecord,
            nDoubleClicksCell=nDoubleClicksCell,
            recentlyCellDoubleClickColumn=recentlyCellDoubleClickColumn,
            recentlyCellDoubleClickRecord=recentlyCellDoubleClickRecord,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-click-event-demo',
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {
                'key': f'row-{row}',
                **{f'Field {i}': f'Field {i} Row {row}' for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableCellClickListenColumns=[f'Field {i}' for i in range(1, 6, 2)],
    ),
    html.Pre(id='table-click-event-demo-output'),
]

# ...

@app.callback(
    Output('table-click-event-demo-output', 'children'),
    [
        Input('table-click-event-demo', 'nClicksCell'),
        Input('table-click-event-demo', 'nDoubleClicksCell'),
    ],
    [
        State('table-click-event-demo', 'enableCellClickListenColumns'),
        State('table-click-event-demo', 'recentlyCellClickColumn'),
        State('table-click-event-demo', 'recentlyCellClickRecord'),
        State('table-click-event-demo', 'recentlyCellDoubleClickColumn'),
        State('table-click-event-demo', 'recentlyCellDoubleClickRecord'),
    ],
    prevent_initial_call=True,
)
def table_click_event_demo(
    nClicksCell,
    nDoubleClicksCell,
    enableCellClickListenColumns,
    recentlyCellClickColumn,
    recentlyCellClickRecord,
    recentlyCellDoubleClickColumn,
    recentlyCellDoubleClickRecord,
):
    return json.dumps(
        dict(
            enableCellClickListenColumns=enableCellClickListenColumns,
            nClicksCell=nClicksCell,
            recentlyCellClickColumn=recentlyCellClickColumn,
            recentlyCellClickRecord=recentlyCellClickRecord,
            nDoubleClicksCell=nDoubleClicksCell,
            recentlyCellDoubleClickColumn=recentlyCellDoubleClickColumn,
            recentlyCellDoubleClickRecord=recentlyCellDoubleClickRecord,
        ),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/listen_mouse_enter.py`
```python
import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        col_label = lambda i: f'字段{i}'
        cell_value = lambda i, row: f'字段{i}第{row}行'
    else:  # en-us fallback
        col_label = lambda i: f'Field {i}'
        cell_value = lambda i, row: f'Field {i} Row {row}'

    columns = [
        {'title': col_label(i), 'dataIndex': col_label(i), 'width': '20%'}
        for i in range(1, 6)
    ]

    data = [
        {
            'key': f'row-{row}',
            **{col_label(i): cell_value(i, row) for i in range(1, 6)},
        }
        for row in range(1, 6)
    ]

    demo_contents = [
        fac.AntdTable(
            id='table-hover-event-demo',
            columns=columns,
            data=data,
            bordered=True,
            enableHoverListen=True,
        ),
        html.Pre(id='table-hover-event-demo-output'),
    ]

    return demo_contents


app.clientside_callback(
    """( recentlyMouseEnterColumnDataIndex,
         recentlyMouseEnterRowKey,
         recentlyMouseEnterRow ) => {
        return JSON.stringify(
            {
                recentlyMouseEnterColumnDataIndex,
                recentlyMouseEnterRowKey,
                recentlyMouseEnterRow
            },
            null,
            4
        );
    }""",
    Output('table-hover-event-demo-output', 'children'),
    [
        Input('table-hover-event-demo', 'recentlyMouseEnterColumnDataIndex'),
        Input('table-hover-event-demo', 'recentlyMouseEnterRowKey'),
        Input('table-hover-event-demo', 'recentlyMouseEnterRow'),
    ],
    prevent_initial_call=True,
)


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': '''
[
    fac.AntdTable(
        id="table-hover-event-demo",
        columns=[
            {"title": f"字段{i}", "dataIndex": f"字段{i}", "width": "20%"}
            for i in range(1, 6)
        ],
        data=[
            {
                "key": f"row-{row}",
                **{f"字段{i}": f"字段{i}第{row}行" for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableHoverListen=True,
    ),
    html.Pre(id="table-hover-event-demo-output"),
]

# ...

app.clientside_callback(
    """( recentlyMouseEnterColumnDataIndex,
         recentlyMouseEnterRowKey,
         recentlyMouseEnterRow ) => {
        return JSON.stringify(
            {
                recentlyMouseEnterColumnDataIndex,
                recentlyMouseEnterRowKey,
                recentlyMouseEnterRow
            },
            null,
            4
        );
    }""",
    Output("table-hover-event-demo-output", "children"),
    [
        Input("table-hover-event-demo", "recentlyMouseEnterColumnDataIndex"),
        Input("table-hover-event-demo", "recentlyMouseEnterRowKey"),
        Input("table-hover-event-demo", "recentlyMouseEnterRow"),
    ],
    prevent_initial_call=True,
)
'''
            }
        ]
    else:  # en-us
        return [
            {
                'code': '''
[
    fac.AntdTable(
        id="table-hover-event-demo",
        columns=[
            {"title": f"Field {i}", "dataIndex": f"Field {i}", "width": "20%"}
            for i in range(1, 6)
        ],
        data=[
            {
                "key": f"row-{row}",
                **{f"Field {i}": f"Field {i} Row {row}" for i in range(1, 6)},
            }
            for row in range(1, 6)
        ],
        bordered=True,
        enableHoverListen=True,
    ),
    html.Pre(id="table-hover-event-demo-output"),
]

# ...

app.clientside_callback(
    """( recentlyMouseEnterColumnDataIndex,
         recentlyMouseEnterRowKey,
         recentlyMouseEnterRow ) => {
        return JSON.stringify(
            {
                recentlyMouseEnterColumnDataIndex,
                recentlyMouseEnterRowKey,
                recentlyMouseEnterRow
            },
            null,
            4
        );
    }""",
    Output("table-hover-event-demo-output", "children"),
    [
        Input("table-hover-event-demo", "recentlyMouseEnterColumnDataIndex"),
        Input("table-hover-event-demo", "recentlyMouseEnterRowKey"),
        Input("table-hover-event-demo", "recentlyMouseEnterRow"),
    ],
    prevent_initial_call=True,
)
'''
            }
        ]

```

### `views/AntdTableAdvanced/demos/nested_data.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        level1 = '第一层'
        level2 = '第二层'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        level1 = 'First Level'
        level2 = 'Second Level'

    demo_contents = fac.AntdTable(
        columns=[
            {
                'title': title(i),
                'dataIndex': data_key(i),
                'width': 'calc(100% / 3)',
            }
            for i in range(1, 4)
        ],
        data=[
            {
                'key': f'row-{i}',
                data_key(1): level1,
                data_key(2): level1,
                data_key(3): level1,
                'children': [
                    {
                        'key': f'row-{i}{j}',
                        data_key(1): level2,
                        data_key(2): level2,
                        data_key(3): level2,
                    }
                    for j in range(3)
                ],
            }
            for i in range(3)
        ],
        bordered=True,
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': 'calc(100% / 3)'}
        for i in range(1, 4)
    ],
    data=[
        {
            'key': f'row-{i}',
            '字段1': '第一层',
            '字段2': '第一层',
            '字段3': '第一层',
            'children': [
                {
                    'key': f'row-{i}{j}',
                    '字段1': '第二层',
                    '字段2': '第二层',
                    '字段3': '第二层',
                }
                for j in range(3)
            ],
        }
        for i in range(3)
    ],
    bordered=True,
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': 'calc(100% / 3)'}
        for i in range(1, 4)
    ],
    data=[
        {
            'key': f'row-{i}',
            'Field 1': 'First Level',
            'Field 2': 'First Level',
            'Field 3': 'First Level',
            'children': [
                {
                    'key': f'row-{i}{j}',
                    'Field 1': 'Second Level',
                    'Field 2': 'Second Level',
                    'Field 3': 'Second Level',
                }
                for j in range(3)
            ],
        }
        for i in range(3)
    ],
    bordered=True,
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{data_key(i): cell_value for i in range(1, 6)}] * 20,
        pagination={'disabled': True, 'pageSize': 5},
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination={'disabled': True, 'pageSize': 5},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 20,
    pagination={'disabled': True, 'pageSize': 5},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_false.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{data_key(i): cell_value for i in range(1, 6)}] * 20,
        pagination=False,
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination=False,
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 20,
    pagination=False,
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_hide_on_single_page.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{data_key(i): cell_value for i in range(1, 6)}] * 3,
        pagination={'pageSize': 10, 'hideOnSinglePage': True},
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 3,
    pagination={'pageSize': 10, 'hideOnSinglePage': True},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 3,
    pagination={'pageSize': 10, 'hideOnSinglePage': True},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_page_size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{data_key(i): cell_value for i in range(1, 6)}] * 10,
        pagination={'pageSize': 7},
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 7},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 7},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_page_size_options.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': data_key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{data_key(i): cell_value for i in range(1, 6)}] * 20,
        pagination={
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10, 20],
        },
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
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
    pagination={
        'pageSize': 5,
        'showSizeChanger': True,
        'pageSizeOptions': [5, 10, 20],
    },
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 20,
    pagination={
        'pageSize': 5,
        'showSizeChanger': True,
        'pageSizeOptions': [5, 10, 20],
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        data_key = lambda i: f'字段{i}'
        cell_value = '示例内容'
        divider_label = lambda placement: f'位置="{placement}"'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        data_key = lambda i: f'Field {i}'
        cell_value = 'Sample Content'
        divider_label = lambda placement: f'placement="{placement}"'

    placements = [
        'topLeft',
        'topCenter',
        'topRight',
        'bottomLeft',
        'bottomCenter',
        'bottomRight',
    ]

    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdDivider(
                        divider_label(placement), innerTextOrientation='left'
                    ),
                    fac.AntdTable(
                        columns=[
                            {
                                'title': title(i),
                                'dataIndex': data_key(i),
                                'width': '20%',
                            }
                            for i in range(1, 6)
                        ],
                        data=[{data_key(i): cell_value for i in range(1, 6)}],
                        pagination={'position': placement},
                    ),
                ],
                direction='vertical',
                style={'width': '100%'},
            )
            for placement in placements
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
                fac.AntdDivider(f'位置="{placement}"', innerTextOrientation='left'),
                fac.AntdTable(
                    columns=[
                        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                        for i in range(1, 6)
                    ],
                    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}],
                    pagination={'position': placement},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for placement in [
            'topLeft', 'topCenter', 'topRight',
            'bottomLeft', 'bottomCenter', 'bottomRight'
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDivider(f'placement="{placement}"', innerTextOrientation='left'),
                fac.AntdTable(
                    columns=[
                        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
                        for i in range(1, 6)
                    ],
                    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}],
                    pagination={'position': placement},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
        for placement in [
            'topLeft', 'topCenter', 'topRight',
            'bottomLeft', 'bottomCenter', 'bottomRight'
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_show_less_items.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        div_top = 'showLessItems=False（默认）'
        div_bottom = 'showLessItems=True'
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        div_top = 'showLessItems=False (default)'
        div_bottom = 'showLessItems=True'
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    table_cols = [
        {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
        for i in range(1, 6)
    ]
    table_data = [{key(i): cell for i in range(1, 6)}] * 20

    demo_contents = [
        fac.AntdDivider(div_top, innerTextOrientation='left'),
        fac.AntdTable(
            columns=table_cols,
            data=table_data,
            pagination={'pageSize': 2, 'current': 5},
        ),
        fac.AntdDivider(div_bottom, innerTextOrientation='left'),
        fac.AntdTable(
            columns=table_cols,
            data=table_data,
            pagination={'pageSize': 2, 'showLessItems': True, 'current': 5},
        ),
    ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdDivider('showLessItems=False（默认）', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'current': 5},
    ),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'showLessItems': True, 'current': 5},
    ),
]
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
[
    fac.AntdDivider('showLessItems=False (default)', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'current': 5},
    ),
    fac.AntdDivider('showLessItems=True', innerTextOrientation='left'),
    fac.AntdTable(
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 20,
        pagination={'pageSize': 2, 'showLessItems': True, 'current': 5},
    ),
]
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_show_quick_jumper.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 10,
        pagination={'pageSize': 2, 'showQuickJumper': True},
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'showQuickJumper': True},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'showQuickJumper': True},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/pagination_simple.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 10,
        pagination={'pageSize': 2, 'simple': True},
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'simple': True},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 10,
    pagination={'pageSize': 2, 'simple': True},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/row_select_callbacks.py`
```python
import json

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    columns = [{'title': title(i), 'dataIndex': key(i)} for i in range(1, 4)]
    data = [
        {**{key(i): cell for i in range(1, 4)}, 'key': f'row-{row + 1}'}
        for row in range(3)
    ]

    demo_contents = [
        fac.AntdTable(
            id='table-row-selection-demo',
            columns=columns,
            data=data,
            rowSelectionType='checkbox',
        ),
        html.Pre(id='table-row-selection-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('table-row-selection-demo-output', 'children'),
    [
        Input('table-row-selection-demo', 'selectedRowKeys'),
        Input('table-row-selection-demo', 'selectedRows'),
    ],
    prevent_initial_call=True,
)
def table_row_selection_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-row-selection-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
            for i in range(1, 4)
        ],
        data=[
            {
                **{f'字段{i}': '示例内容' for i in range(1, 4)},
                'key': f'row-{row+1}',
            }
            for row in range(3)
        ],
        rowSelectionType='checkbox',
    ),
    html.Pre(id='table-row-selection-demo-output'),
]

# ...

@app.callback(
    Output('table-row-selection-demo-output', 'children'),
    [
        Input('table-row-selection-demo', 'selectedRowKeys'),
        Input('table-row-selection-demo', 'selectedRows'),
    ],
    prevent_initial_call=True,
)
def table_row_selection_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-row-selection-demo',
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
            for i in range(1, 4)
        ],
        data=[
            {
                **{f'Field {i}': 'Sample Content' for i in range(1, 4)},
                'key': f'row-{row+1}',
            }
            for row in range(3)
        ],
        rowSelectionType='checkbox',
    ),
    html.Pre(id='table-row-selection-demo-output'),
]

# ...

@app.callback(
    Output('table-row-selection-demo-output', 'children'),
    [
        Input('table-row-selection-demo', 'selectedRowKeys'),
        Input('table-row-selection-demo', 'selectedRows'),
    ],
    prevent_initial_call=True,
)
def table_row_selection_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/row_select_checkbox.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[{'title': title(i), 'dataIndex': key(i)} for i in range(1, 6)],
        data=[
            {**{key(i): cell for i in range(1, 6)}, 'key': f'row-{row + 1}'}
            for row in range(3)
        ],
        rowSelectionType='checkbox',
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='checkbox',
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'Field {i}': 'Sample Content' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='checkbox',
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/row_select_radio.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'

    demo_contents = fac.AntdTable(
        columns=[{'title': title(i), 'dataIndex': key(i)} for i in range(1, 6)],
        data=[
            {**{key(i): cell for i in range(1, 6)}, 'key': f'row-{row + 1}'}
            for row in range(3)
        ],
        rowSelectionType='radio',
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='radio',
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'Field {i}': 'Sample Content' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    rowSelectionType='radio',
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/row_select_sync_data.py`
```python
import json
import random

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        btn_text = '刷新数据'
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
    else:  # en-us fallback
        btn_text = 'Refresh Data'
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'

    columns = [{'title': title(i), 'dataIndex': key(i)} for i in range(1, 4)]
    data = [
        {
            **{key(i): round(random.uniform(0, 10), 3) for i in range(1, 4)},
            'key': f'row-{row + 1}',
        }
        for row in range(3)
    ]

    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(
                btn_text,
                id='table-row-selection-sync-selected-rows-demo-update-data',
                type='primary',
            ),
            fac.AntdTable(
                id='table-row-selection-sync-selected-rows-demo',
                columns=columns,
                data=data,
                rowSelectionType='checkbox',
                selectedRowsSyncWithData=True,
            ),
            html.Pre(id='table-row-selection-sync-selected-rows-demo-output'),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    Output('table-row-selection-sync-selected-rows-demo', 'data'),
    Input('table-row-selection-sync-selected-rows-demo-update-data', 'nClicks'),
    prevent_initial_call=True,
)
def table_row_selection_sync_selected_rows_demo_update_data(nClicks):
    # Keep keys aligned with whatever was rendered (Chinese or English)
    locale = get_current_locale()
    key_fn = (
        (lambda i: f'字段{i}')
        if locale == 'zh-cn'
        else (lambda i: f'Field {i}')
    )

    return [
        {
            **{key_fn(i): round(random.uniform(0, 10), 3) for i in range(1, 4)},
            'key': f'row-{row + 1}',
        }
        for row in range(3)
    ]


@app.callback(
    Output('table-row-selection-sync-selected-rows-demo-output', 'children'),
    [
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRowKeys'),
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRows'),
    ],
)
def table_row_selection_sync_selected_rows_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            '刷新数据',
            id='table-row-selection-sync-selected-rows-demo-update-data',
            type='primary',
        ),
        fac.AntdTable(
            id='table-row-selection-sync-selected-rows-demo',
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}'}
                for i in range(1, 4)
            ],
            data=[
                {
                    **{f'字段{i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
                    'key': f'row-{row+1}',
                }
                for row in range(3)
            ],
            rowSelectionType='checkbox',
            selectedRowsSyncWithData=True,
        ),
        html.Pre(id='table-row-selection-sync-selected-rows-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

# ...

@app.callback(
    Output('table-row-selection-sync-selected-rows-demo', 'data'),
    Input('table-row-selection-sync-selected-rows-demo-update-data', 'nClicks'),
    prevent_initial_call=True,
)
def table_row_selection_sync_selected_rows_demo_update_data(nClicks):
    return [
        {
            **{f'字段{i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ]


@app.callback(
    Output('table-row-selection-sync-selected-rows-demo-output', 'children'),
    [
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRowKeys'),
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRows'),
    ],
)
def table_row_selection_sync_selected_rows_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            'Refresh Data',
            id='table-row-selection-sync-selected-rows-demo-update-data',
            type='primary',
        ),
        fac.AntdTable(
            id='table-row-selection-sync-selected-rows-demo',
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}'}
                for i in range(1, 4)
            ],
            data=[
                {
                    **{f'Field {i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
                    'key': f'row-{row+1}',
                }
                for row in range(3)
            ],
            rowSelectionType='checkbox',
            selectedRowsSyncWithData=True,
        ),
        html.Pre(id='table-row-selection-sync-selected-rows-demo-output'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

# ...

@app.callback(
    Output('table-row-selection-sync-selected-rows-demo', 'data'),
    Input('table-row-selection-sync-selected-rows-demo-update-data', 'nClicks'),
    prevent_initial_call=True,
)
def table_row_selection_sync_selected_rows_demo_update_data(nClicks):
    return [
        {
            **{f'Field {i}': round(random.uniform(0, 10), 3) for i in range(1, 4)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ]


@app.callback(
    Output('table-row-selection-sync-selected-rows-demo-output', 'children'),
    [
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRowKeys'),
        Input('table-row-selection-sync-selected-rows-demo', 'selectedRows'),
    ],
)
def table_row_selection_sync_selected_rows_demo(selectedRowKeys, selectedRows):
    return json.dumps(
        dict(selectedRowKeys=selectedRowKeys, selectedRows=selectedRows),
        indent=4,
        ensure_ascii=False,
    )
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/sort_callbacks.py`
```python
import json
import random

import feffery_antd_components as fac
from dash import html
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        label = lambda i: f'字段{i}'
        sort_keys = [label(1), label(2), label(4), label(5)]
    else:  # en-us fallback
        label = lambda i: f'Field {i}'
        sort_keys = [label(1), label(2), label(4), label(5)]

    columns = [
        {'title': label(i), 'dataIndex': label(i), 'width': '20%'}
        for i in range(1, 6)
    ]
    data = [
        {label(j): random.randint(1, 4) for j in range(1, 6)} for _ in range(10)
    ]

    demo_contents = [
        fac.AntdTable(
            id='table-sort-demo',
            columns=columns,
            data=data,
            bordered=True,
            sortOptions={
                'sortDataIndexes': sort_keys,
                'multiple': True,
            },
        ),
        html.Pre(id='table-sort-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('table-sort-demo-output', 'children'),
    Input('table-sort-demo', 'sorter'),
    prevent_initial_call=True,
)
def table_sort_demo(sorter):
    return json.dumps(sorter, indent=4, ensure_ascii=False)


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-sort-demo',
        columns=[
            {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
            for _ in range(10)
        ],
        bordered=True,
        sortOptions={
            'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
            'multiple': True,
        },
    ),
    html.Pre(id='table-sort-demo-output'),
]

# ...

@app.callback(
    Output('table-sort-demo-output', 'children'),
    Input('table-sort-demo', 'sorter'),
    prevent_initial_call=True,
)
def table_sort_demo(sorter):
    return json.dumps(sorter, indent=4, ensure_ascii=False)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
[
    fac.AntdTable(
        id='table-sort-demo',
        columns=[
            {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[
            {f'Field {j}': random.randint(1, 4) for j in range(1, 6)}
            for _ in range(10)
        ],
        bordered=True,
        sortOptions={
            'sortDataIndexes': ['Field 1', 'Field 2', 'Field 4', 'Field 5'],
            'multiple': True,
        },
    ),
    html.Pre(id='table-sort-demo-output'),
]

# ...

@app.callback(
    Output('table-sort-demo-output', 'children'),
    Input('table-sort-demo', 'sorter'),
    prevent_initial_call=True,
)
def table_sort_demo(sorter):
    return json.dumps(sorter, indent=4, ensure_ascii=False)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/sort_multiple.py`
```python
import random

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        label = lambda i: f'字段{i}'
    else:  # en-us fallback
        label = lambda i: f'Field {i}'

    columns = [
        {'title': label(i), 'dataIndex': label(i), 'width': '20%'}
        for i in range(1, 6)
    ]
    data = [
        {label(j): random.randint(1, 4) for j in range(1, 6)} for _ in range(10)
    ]
    sort_data_indexes = [label(1), label(2), label(4), label(5)]

    demo_contents = fac.AntdTable(
        columns=columns,
        data=data,
        bordered=True,
        sortOptions={
            'sortDataIndexes': sort_data_indexes,
            'multiple': True,
        },
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
        'multiple': True,
    },
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'Field {j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['Field 1', 'Field 2', 'Field 4', 'Field 5'],
        'multiple': True,
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/sort_multiple_dynamic.py`
```python
import random

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        label = lambda i: f'字段{i}'
    else:  # en-us fallback
        label = lambda i: f'Field {i}'

    columns = [
        {'title': label(i), 'dataIndex': label(i), 'width': '20%'}
        for i in range(1, 6)
    ]
    data = [
        {label(j): random.randint(1, 4) for j in range(1, 6)} for _ in range(10)
    ]
    sort_data_indexes = [label(1), label(2), label(4), label(5)]

    demo_contents = fac.AntdTable(
        columns=columns,
        data=data,
        bordered=True,
        sortOptions={
            'sortDataIndexes': sort_data_indexes,
            'multiple': 'auto',
        },
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'字段{j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['字段1', '字段2', '字段4', '字段5'],
        'multiple': 'auto',
    },
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
import random
import feffery_antd_components as fac

fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[
        {f'Field {j}': random.randint(1, 4) for j in range(1, 6)}
        for _ in range(10)
    ],
    bordered=True,
    sortOptions={
        'sortDataIndexes': ['Field 1', 'Field 2', 'Field 4', 'Field 5'],
        'multiple': 'auto',
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/sort_single.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        label = {
            'int': 'int型示例',
            'float': 'float型示例',
            'str': 'str型示例',
            'dt': '日期时间示例',
        }
        sample_str = lambda i: f'示例字符{i}'
    else:  # en-us fallback
        label = {
            'int': 'Integer Example',
            'float': 'Float Example',
            'str': 'String Example',
            'dt': 'Datetime Example',
        }
        sample_str = lambda i: f'Sample Text {i}'

    columns = [
        {'title': label['int'], 'dataIndex': label['int'], 'width': '25%'},
        {'title': label['float'], 'dataIndex': label['float'], 'width': '25%'},
        {'title': label['str'], 'dataIndex': label['str'], 'width': '25%'},
        {'title': label['dt'], 'dataIndex': label['dt'], 'width': '25%'},
    ]

    data = [
        {
            label['int']: i,
            label['float']: round(i * 0.1, 1),
            label['str']: sample_str(i),
            label['dt']: f'2099-01-0{i}',
        }
        for i in [4, 2, 1, 5, 3]
    ]

    demo_contents = fac.AntdTable(
        columns=columns,
        data=data,
        sortOptions={
            'sortDataIndexes': [
                label['int'],
                label['float'],
                label['str'],
                label['dt'],
            ]
        },
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': 'int型示例', 'dataIndex': 'int型示例', 'width': '25%'},
        {'title': 'float型示例', 'dataIndex': 'float型示例', 'width': '25%'},
        {'title': 'str型示例', 'dataIndex': 'str型示例', 'width': '25%'},
        {'title': '日期时间示例', 'dataIndex': '日期时间示例', 'width': '25%'},
    ],
    data=[
        {
            'int型示例': i,
            'float型示例': round(i * 0.1, 1),
            'str型示例': f'示例字符{i}',
            '日期时间示例': f'2099-01-0{i}',
        }
        for i in [4, 2, 1, 5, 3]
    ],
    sortOptions={
        'sortDataIndexes': ['int型示例', 'float型示例', 'str型示例', '日期时间示例'],
    },
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': 'Integer Example', 'dataIndex': 'Integer Example', 'width': '25%'},
        {'title': 'Float Example', 'dataIndex': 'Float Example', 'width': '25%'},
        {'title': 'String Example', 'dataIndex': 'String Example', 'width': '25%'},
        {'title': 'Datetime Example', 'dataIndex': 'Datetime Example', 'width': '25%'},
    ],
    data=[
        {
            'Integer Example': i,
            'Float Example': round(i * 0.1, 1),
            'String Example': f'Sample Text {i}',
            'Datetime Example': f'2099-01-0{i}',
        }
        for i in [4, 2, 1, 5, 3]
    ],
    sortOptions={
        'sortDataIndexes': ['Integer Example', 'Float Example', 'String Example', 'Datetime Example'],
    },
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/sort_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        label = {
            'int': 'int型示例',
            'float': 'float型示例',
            'str': 'str型示例',
            'dt': '日期时间示例',
        }
        sample_str = lambda i: f'示例字符{i}'
    else:  # en-us fallback
        label = {
            'int': 'Integer Example',
            'float': 'Float Example',
            'str': 'String Example',
            'dt': 'Datetime Example',
        }
        sample_str = lambda i: f'Sample Text {i}'

    columns = [
        {'title': label['int'], 'dataIndex': label['int'], 'width': '25%'},
        {'title': label['float'], 'dataIndex': label['float'], 'width': '25%'},
        {'title': label['str'], 'dataIndex': label['str'], 'width': '25%'},
        {'title': label['dt'], 'dataIndex': label['dt'], 'width': '25%'},
    ]

    data = [
        {
            label['int']: i,
            label['float']: round(i * 0.1, 1),
            label['str']: sample_str(i),
            label['dt']: f'2099-01-0{i}',
        }
        for i in [4, 2, 1, 5, 3]
    ]

    demo_contents = fac.AntdSpace(
        [
            fac.AntdFormItem(
                fac.AntdSwitch(
                    id='table-sort-tooltip-demo-show-sorter-tooltip',
                    checked=True,
                ),
                label='showSorterTooltip',
                layout='horizontal',
                style={'margin': 0},
            ),
            fac.AntdFormItem(
                fac.AntdRadioGroup(
                    id='table-sort-tooltip-demo-show-sorter-tooltip-target',
                    options=['full-header', 'sorter-icon'],
                    value='full-header',
                ),
                label='showSorterTooltipTarget',
                layout='horizontal',
                style={'margin': 0},
            ),
            fac.AntdTable(
                id='table-sort-tooltip-demo',
                columns=columns,
                data=data,
                sortOptions={
                    'sortDataIndexes': [
                        label['int'],
                        label['float'],
                        label['str'],
                        label['dt'],
                    ]
                },
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


app.clientside_callback(
    """(showSorterTooltip, showSorterTooltipTarget) => [showSorterTooltip, showSorterTooltipTarget]""",
    [
        Output('table-sort-tooltip-demo', 'showSorterTooltip'),
        Output('table-sort-tooltip-demo', 'showSorterTooltipTarget'),
    ],
    [
        Input('table-sort-tooltip-demo-show-sorter-tooltip', 'checked'),
        Input('table-sort-tooltip-demo-show-sorter-tooltip-target', 'value'),
    ],
)


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    from i18n import get_current_locale

    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': '''
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='table-sort-tooltip-demo-show-sorter-tooltip',
                checked=True,
            ),
            label='showSorterTooltip',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='table-sort-tooltip-demo-show-sorter-tooltip-target',
                options=['full-header', 'sorter-icon'],
                value='full-header',
            ),
            label='showSorterTooltipTarget',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdTable(
            id='table-sort-tooltip-demo',
            columns=[
                {'title': 'int型示例', 'dataIndex': 'int型示例', 'width': '25%'},
                {'title': 'float型示例', 'dataIndex': 'float型示例', 'width': '25%'},
                {'title': 'str型示例', 'dataIndex': 'str型示例', 'width': '25%'},
                {'title': '日期时间示例', 'dataIndex': '日期时间示例', 'width': '25%'},
            ],
            data=[
                {
                    'int型示例': i,
                    'float型示例': round(i * 0.1, 1),
                    'str型示例': f'示例字符{i}',
                    '日期时间示例': f'2099-01-0{i}',
                }
                for i in [4, 2, 1, 5, 3]
            ],
            sortOptions={
                'sortDataIndexes': ['int型示例', 'float型示例', 'str型示例', '日期时间示例']
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

app.clientside_callback(
    """(showSorterTooltip, showSorterTooltipTarget) => [showSorterTooltip, showSorterTooltipTarget]""",
    [
        Output('table-sort-tooltip-demo', 'showSorterTooltip'),
        Output('table-sort-tooltip-demo', 'showSorterTooltipTarget'),
    ],
    [
        Input('table-sort-tooltip-demo-show-sorter-tooltip', 'checked'),
        Input('table-sort-tooltip-demo-show-sorter-tooltip-target', 'value'),
    ],
)
'''
            }
        ]
    else:  # en-us
        return [
            {
                'code': '''
fac.AntdSpace(
    [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='table-sort-tooltip-demo-show-sorter-tooltip',
                checked=True,
            ),
            label='showSorterTooltip',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='table-sort-tooltip-demo-show-sorter-tooltip-target',
                options=['full-header', 'sorter-icon'],
                value='full-header',
            ),
            label='showSorterTooltipTarget',
            layout='horizontal',
            style={'margin': 0},
        ),
        fac.AntdTable(
            id='table-sort-tooltip-demo',
            columns=[
                {'title': 'Integer Example', 'dataIndex': 'Integer Example', 'width': '25%'},
                {'title': 'Float Example', 'dataIndex': 'Float Example', 'width': '25%'},
                {'title': 'String Example', 'dataIndex': 'String Example', 'width': '25%'},
                {'title': 'Datetime Example', 'dataIndex': 'Datetime Example', 'width': '25%'},
            ],
            data=[
                {
                    'Integer Example': i,
                    'Float Example': round(i * 0.1, 1),
                    'String Example': f'Sample Text {i}',
                    'Datetime Example': f'2099-01-0{i}',
                }
                for i in [4, 2, 1, 5, 3]
            ],
            sortOptions={
                'sortDataIndexes': ['Integer Example', 'Float Example', 'String Example', 'Datetime Example']
            },
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

app.clientside_callback(
    """(showSorterTooltip, showSorterTooltipTarget) => [showSorterTooltip, showSorterTooltipTarget]""",
    [
        Output('table-sort-tooltip-demo', 'showSorterTooltip'),
        Output('table-sort-tooltip-demo', 'showSorterTooltipTarget'),
    ],
    [
        Input('table-sort-tooltip-demo-show-sorter-tooltip', 'checked'),
        Input('table-sort-tooltip-demo-show-sorter-tooltip-target', 'value'),
    ],
)
'''
            }
        ]

```

### `views/AntdTableAdvanced/demos/sticky.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        col = lambda i: f'字段{i}'
        cell = '示例内容'
        table_title = '请点击本示例下方的“在新窗口打开”按钮，以查看无页首遮挡干扰的完整效果。'
    else:  # en-us fallback
        col = lambda i: f'Field {i}'
        cell = 'Sample Content'
        table_title = 'Click the “Open in new window” button below to view the full effect without the header overlapping.'

    demo_contents = fac.AntdTable(
        columns=[{'title': col(i), 'dataIndex': col(i)} for i in range(1, 4)],
        data=[{col(i): cell for i in range(1, 4)} for _ in range(30)],
        sticky=True,
        size='large',
        pagination={'pageSize': 999},
        title=table_title,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 4)
    ],
    data=[
        {f'字段{i}': '示例内容' for i in range(1, 4)} for row in range(30)
    ],
    sticky=True,
    size='large',
    pagination={'pageSize': 999},
    title='请点击本示例下方的“在新窗口打开”按钮，以查看无页首遮挡干扰的完整效果。',
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 4)
    ],
    data=[
        {f'Field {i}': 'Sample Content' for i in range(1, 4)} for _ in range(30)
    ],
    sticky=True,
    size='large',
    pagination={'pageSize': 999},
    title='Click the “Open in new window” button below to view the full effect without the header overlapping.',
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_basic.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
        summary = [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'
        summary = [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 5,
        bordered=True,
        summaryRowContents=summary,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': 'Summary of Col 1'},
        {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
        {'content': 'Summary of Col 5', 'align': 'right'},
    ],
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_blank_columns.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
        summary_one = [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
        summary_two = summary_one + [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'
        summary_one = [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]
        summary_two = summary_one + [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]

    demo_contents = fac.AntdSpace(
        [
            fac.AntdTable(
                columns=[
                    {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
                    for i in range(1, 6)
                ],
                data=[{key(i): cell for i in range(1, 6)}] * 5,
                bordered=True,
                summaryRowContents=summary_one,
                rowSelectionType='radio',
                summaryRowBlankColumns=1,
            ),
            fac.AntdTable(
                columns=[
                    {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
                    for i in range(1, 6)
                ],
                data=[{key(i): cell for i in range(1, 6)}] * 5,
                bordered=True,
                summaryRowContents=summary_two,
                rowSelectionType='radio',
                summaryRowBlankColumns=1,
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
        fac.AntdTable(
            columns=[
                {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
                {'content': '第1列总结'},
                {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
                {'content': '第5列总结', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdSpace(
    [
        fac.AntdTable(
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': 'Summary of Col 1'},
                {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
                {'content': 'Summary of Col 5', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
        fac.AntdTable(
            columns=[
                {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
                for i in range(1, 6)
            ],
            data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 5,
            bordered=True,
            summaryRowContents=[
                {'content': 'Summary of Col 1'},
                {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
                {'content': 'Summary of Col 5', 'align': 'right'},
                {'content': 'Summary of Col 1'},
                {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
                {'content': 'Summary of Col 5', 'align': 'right'},
            ],
            rowSelectionType='radio',
            summaryRowBlankColumns=1,
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_fixed_bottom.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
        summary = [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'
        summary = [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 10,
        bordered=True,
        summaryRowContents=summary,
        summaryRowFixed=True,
        maxHeight=150,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
    summaryRowFixed=True,
    maxHeight=150,
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': 'Summary of Col 1'},
        {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
        {'content': 'Summary of Col 5', 'align': 'right'},
    ],
    summaryRowFixed=True,
    maxHeight=150,
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_fixed_top.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
        summary = [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
    else:  # en-us fallback
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'
        summary = [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 10,
        bordered=True,
        summaryRowContents=summary,
        summaryRowFixed='top',
        maxHeight=150,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
    summaryRowFixed='top',
    maxHeight=150,
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 10,
    bordered=True,
    summaryRowContents=[
        {'content': 'Summary of Col 1'},
        {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
        {'content': 'Summary of Col 5', 'align': 'right'},
    ],
    summaryRowFixed='top',
    maxHeight=150,
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_multiple.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        title = lambda i: f'字段{i}'
        key = lambda i: f'字段{i}'
        cell = '示例内容'
        summary = [
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
            {'content': '第1列总结'},
            {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
            {'content': '第5列总结', 'align': 'right'},
        ]
    else:  # en-us
        title = lambda i: f'Field {i}'
        key = lambda i: f'Field {i}'
        cell = 'Sample Content'
        summary = [
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
            {'content': 'Summary of Col 1'},
            {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
            {'content': 'Summary of Col 5', 'align': 'right'},
        ]

    demo_contents = fac.AntdTable(
        columns=[
            {'title': title(i), 'dataIndex': key(i), 'width': '20%'}
            for i in range(1, 6)
        ],
        data=[{key(i): cell for i in range(1, 6)}] * 5,
        bordered=True,
        summaryRowContents=summary,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'字段{i}': '示例内容' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
        {'content': '第1列总结'},
        {'content': '第2到4列总结', 'colSpan': 3, 'align': 'center'},
        {'content': '第5列总结', 'align': 'right'},
    ],
)
"""
            }
        ]
    else:
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}', 'width': '20%'}
        for i in range(1, 6)
    ],
    data=[{f'Field {i}': 'Sample Content' for i in range(1, 6)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': 'Summary of Col 1'},
        {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
        {'content': 'Summary of Col 5', 'align': 'right'},
        {'content': 'Summary of Col 1'},
        {'content': 'Summary of Cols 2–4', 'colSpan': 3, 'align': 'center'},
        {'content': 'Summary of Col 5', 'align': 'right'},
    ],
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/summary_with_multi_level_header.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        col = lambda i: f'字段{i}'
        grp = '组1'
        cell = lambda i: f'示例内容{i}'
        summary = [
            {'content': '第1列总结', 'align': 'center'},
            {'content': '第2到3列总结', 'colSpan': 2, 'align': 'center'},
            {'content': '第4列总结', 'align': 'center'},
            {'content': '第5到6列总结', 'colSpan': 2, 'align': 'center'},
            {'content': 'xxx', 'align': 'center'},
            {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
            {'content': 'xxx', 'align': 'center'},
            {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
        ]
    else:  # en-us fallback
        col = lambda i: f'Field {i}'
        grp = 'Group 1'
        cell = lambda i: f'Sample Content {i}'
        summary = [
            {'content': 'Summary of Col 1', 'align': 'center'},
            {'content': 'Summary of Cols 2–3', 'colSpan': 2, 'align': 'center'},
            {'content': 'Summary of Col 4', 'align': 'center'},
            {'content': 'Summary of Cols 5–6', 'colSpan': 2, 'align': 'center'},
            {'content': 'xxx', 'align': 'center'},
            {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
            {'content': 'xxx', 'align': 'center'},
            {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
        ]

    columns = [
        {'title': col(1), 'dataIndex': col(1)},
        {'title': col(2), 'dataIndex': col(2)},
        {'title': col(3), 'dataIndex': col(3), 'group': grp},
        {'title': col(4), 'dataIndex': col(4), 'group': grp},
        {'title': col(5), 'dataIndex': col(5)},
        {'title': col(6), 'dataIndex': col(6)},
    ]

    data = [{col(i): cell(i) for i in range(1, 7)}] * 5

    demo_contents = fac.AntdTable(
        columns=columns,
        data=data,
        bordered=True,
        summaryRowContents=summary,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': '字段1', 'dataIndex': '字段1'},
        {'title': '字段2', 'dataIndex': '字段2'},
        {'title': '字段3', 'dataIndex': '字段3', 'group': '组1'},
        {'title': '字段4', 'dataIndex': '字段4', 'group': '组1'},
        {'title': '字段5', 'dataIndex': '字段5'},
        {'title': '字段6', 'dataIndex': '字段6'},
    ],
    data=[{f'字段{i}': f'示例内容{i}' for i in range(1, 7)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': '第1列总结', 'align': 'center'},
        {'content': '第2到3列总结', 'colSpan': 2, 'align': 'center'},
        {'content': '第4列总结', 'align': 'center'},
        {'content': '第5到6列总结', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
    ],
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': 'Field 1', 'dataIndex': 'Field 1'},
        {'title': 'Field 2', 'dataIndex': 'Field 2'},
        {'title': 'Field 3', 'dataIndex': 'Field 3', 'group': 'Group 1'},
        {'title': 'Field 4', 'dataIndex': 'Field 4', 'group': 'Group 1'},
        {'title': 'Field 5', 'dataIndex': 'Field 5'},
        {'title': 'Field 6', 'dataIndex': 'Field 6'},
    ],
    data=[{f'Field {i}': f'Sample Content {i}' for i in range(1, 7)}] * 5,
    bordered=True,
    summaryRowContents=[
        {'content': 'Summary of Col 1', 'align': 'center'},
        {'content': 'Summary of Cols 2–3', 'colSpan': 2, 'align': 'center'},
        {'content': 'Summary of Col 4', 'align': 'center'},
        {'content': 'Summary of Cols 5–6', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
        {'content': 'xxx', 'align': 'center'},
        {'content': 'xxx', 'colSpan': 2, 'align': 'center'},
    ],
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/text_area_editable.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        col_title = '文本域编辑示例'
        data_key = '文本域编辑示例'
        sample_value = '内容示例'
    else:  # en-us fallback
        col_title = 'Text Area Edit Example'
        data_key = 'Text Area Edit Example'
        sample_value = 'Content Example'

    demo_contents = fac.AntdTable(
        columns=[
            {
                'title': col_title,
                'dataIndex': data_key,
                'editable': True,
                'editOptions': {
                    'mode': 'text-area',  # text-area edit mode
                    'autoSize': {'minRows': 1, 'maxRows': 3},
                },
            }
        ],
        data=[{data_key: sample_value}] * 3,
        bordered=True,
        style={'width': 200},
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': '文本域编辑示例',
            'dataIndex': '文本域编辑示例',
            'editable': True,
            'editOptions': {
                'mode': 'text-area',  # 开启文本域编辑模式
                'autoSize': {'minRows': 1, 'maxRows': 3},
            },
        }
    ],
    data=[{'文本域编辑示例': '内容示例'}] * 3,
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {
            'title': 'Text Area Edit Example',
            'dataIndex': 'Text Area Edit Example',
            'editable': True,
            'editOptions': {
                'mode': 'text-area',  # enable text-area edit mode
                'autoSize': {'minRows': 1, 'maxRows': 3},
            },
        }
    ],
    data=[{'Text Area Edit Example': 'Content Example'}] * 3,
    bordered=True,
    style={'width': 200},
)
"""
            }
        ]

```

### `views/AntdTableAdvanced/demos/title_popover_info.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == 'zh-cn':
        col = lambda i: f'字段{i}'
        cell = '示例内容'
        pop_title = lambda i: f'字段{i}说明'
        pop_content = lambda i: f'这是字段{i}的说明巴拉巴拉巴拉'
    else:  # en-us fallback
        col = lambda i: f'Field {i}'
        cell = 'Sample Content'
        pop_title = lambda i: f'About Field {i}'
        pop_content = (
            lambda i: f'This is a description for Field {i} (placeholder).'
        )

    columns = [{'title': col(i), 'dataIndex': col(i)} for i in range(1, 6)]
    data = [
        {**{col(i): cell for i in range(1, 6)}, 'key': f'row-{row + 1}'}
        for row in range(3)
    ]

    title_popover_info = {
        col(i): {
            'title': pop_title(i),
            'content': pop_content(i),
            'placement': 'top',
        }
        for i in range(1, 6)
    }

    demo_contents = fac.AntdTable(
        columns=columns,
        data=data,
        titlePopoverInfo=title_popover_info,
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'字段{i}', 'dataIndex': f'字段{i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'字段{i}': '示例内容' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    titlePopoverInfo={
        f'字段{i}': {
            'title': f'字段{i}说明',
            'content': f'这是字段{i}的说明巴拉巴拉巴拉',
            'placement': 'top',
        }
        for i in range(1, 6)
    },
)
"""
            }
        ]
    else:  # en-us
        return [
            {
                'code': """
fac.AntdTable(
    columns=[
        {'title': f'Field {i}', 'dataIndex': f'Field {i}'} for i in range(1, 6)
    ],
    data=[
        {
            **{f'Field {i}': 'Sample Content' for i in range(1, 6)},
            'key': f'row-{row+1}',
        }
        for row in range(3)
    ],
    titlePopoverInfo={
        f'Field {i}': {
            'title': f'About Field {i}',
            'content': f'This is a description for Field {i} (placeholder).',
            'placement': 'top',
        }
        for i in range(1, 6)
    },
)
"""
            }
        ]

```
