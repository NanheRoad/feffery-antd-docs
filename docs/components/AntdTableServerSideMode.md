# AntdTableServerSideMode

## 简介源码：`views/AntdTableServerSideMode/intro.py`
```python
import feffery_antd_components as fac
import feffery_markdown_components as fmc
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
                {'title': translator.t('服务端数据加载模式')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        *[
            fac.AntdParagraph(
                translator.t('表格组件适用于大数据场景的服务端数据加载模式。')
            ),
            fac.AntdDivider(isDashed=True),
            fac.AntdParagraph(
                [
                    translator.t('本页文档展示了'),
                    fac.AntdText(' AntdTable ', strong=True),
                    translator.t(
                        '组件基于服务端数据加载模式，对大量数据的展示需求进行性能优化，本质上是在设置参数'
                    ),
                    fac.AntdText('mode="server-side"', code=True),
                    translator.t('后，通过监听'),
                    fac.AntdText(' AntdTable ', strong=True),
                    translator.t(
                        '中翻页、排序、筛选等常见交互行为对应的监听参数变化，进而通过回调函数传递到后端进行对应数据帧的生成，并传回'
                    ),
                    fac.AntdText(' AntdTable ', strong=True),
                    translator.t(
                        '中进行展示，相当于任意时刻下，表格中实际加载的数据只有用户所看到的当页数据'
                    ),
                ],
                style={'textIndent': '2rem'},
            ),
            fac.AntdParagraph(
                [
                    fac.AntdText(translator.t('注意'), strong=True),
                    translator.t('，本页文档后续所有与'),
                    fac.AntdText(' demo_df ', code=True),
                    translator.t('有关的示例中，'),
                    fac.AntdText(' demo_df ', code=True),
                    translator.t('均为同一个'),
                    fac.AntdText(' pandas ', strong=True),
                    translator.t('数据框，由下列代码生成：'),
                ],
                style={'textIndent': '2rem', 'marginBottom': 0},
            ),
            fac.AntdCollapse(
                fmc.FefferySyntaxHighlighter(
                    showCopyButton=True,
                    showLineNumbers=True,
                    language='python',
                    codeTheme='coy-without-shadows',
                    codeString="""
import pandas as pd

# 生成演示用数据框
demo_df = (
    pd
    .DataFrame(
        {
            'id': list(range(1, 100001)),
            '字段1': np.random.choice(
                [
                    f'{s}{n}'
                    for s in list('abcdefghij')
                    for n in range(1, 10001)
                ],
                100000,
                replace=False
            ),
            '字段2': np.random.choice(
                [
                    f'类型{t}'
                    for t in range(1, 11)
                    for n in range(10000)
                ],
                100000,
                replace=False
            )
        }
    )
    # 打乱顺序
    .sample(frac=1, replace=False)
)
""",
                ),
                isOpen=False,
                title=translator.t('演示用数据框生成代码'),
                ghost=True,
            ),
            fac.AntdParagraph(
                [
                    translator.t('本页文档后续所有与'),
                    fac.AntdText('DemoTable', code=True),
                    translator.t('有关的示例中，'),
                    fac.AntdText('DemoTable', code=True),
                    translator.t('均为同一个基于'),
                    fac.AntdText('peewee', strong=True),
                    translator.t('定义的'),
                    fac.AntdText('ORM', strong=True),
                    translator.t('模型类，由下列代码定义：'),
                ],
                style={'textIndent': '2rem', 'marginBottom': 0},
            ),
            fac.AntdCollapse(
                fmc.FefferySyntaxHighlighter(
                    showCopyButton=True,
                    showLineNumbers=True,
                    language='python',
                    codeTheme='coy-without-shadows',
                    codeString="""
from peewee import (
    SqliteDatabase,
    CharField,
    IntegerField,
    Model,
    fn
)

...

# 构造演示用数据库表模型类，基于sqlite+peewee
db = SqliteDatabase('./demo_table.db')


class DemoTable(Model):

    id = IntegerField()

    字段1 = CharField()

    字段2 = CharField()

    class Meta:

        table_name = 'demo_table'
        database = db


# 创建表格并插入示例数据
db.create_tables([DemoTable])

# 为方便调试，先检查数据表中是否已有记录，若有则跳过数据插入
with db.atomic():

    if (
        DemoTable
        .select(fn.count(DemoTable.id))
        .scalar()
    ) == 0:

        # 分批插入
        for batch in range(10):
            (
                DemoTable
                .insert_many(
                    demo_df
                    .iloc[batch*10000:(batch+1)*10000, :]
                    .to_dict('records')
                )
                .execute()
            )
""",
                ),
                isOpen=False,
                title=translator.t('演示用数据库表模型生成代码'),
                ghost=True,
            ),
        ],
        fac.AntdDivider(isDashed=True),
    ]

```

## 示例源码（demos）

### `views/AntdTableServerSideMode/demos/database_pagination.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from peewee import fn

from i18n import get_current_locale
from server import app

from .mock_data import DemoTable


def _en_title(name: str) -> str:
    return (
        f'Field {name[2:]}'
        if name.startswith('字段') and name[2:].isdigit()
        else name
    )


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()
    field_names = list(DemoTable._meta.fields.keys())
    col_width = f'calc(100% / {len(field_names)})'

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination-demo-sql',
                columns=[
                    {
                        'title': column,
                        'dataIndex': column,
                        'width': col_width,
                    }
                    for column in field_names
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination-demo-sql',
                locale='en-us',
                columns=[
                    {
                        'title': _en_title(column),
                        'dataIndex': column,  # keep raw keys in dataIndex
                        'width': col_width,
                    }
                    for column in field_names
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination-demo-sql', 'data'),
    Input('table-server-side-mode-pagination-demo-sql', 'pagination'),
)
def table_server_side_mode_pagination_demo_sql(pagination):
    if pagination:
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        time.sleep(0.5)
        return list(data_frame)

    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination-demo-sql',
        columns=[
            {
                'title': column,
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination-demo-sql', 'data'),
    Input('table-server-side-mode-pagination-demo-sql', 'pagination'),
)
def table_server_side_mode_pagination_demo_sql(pagination):
    if pagination:
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        time.sleep(0.5)
        return list(data_frame)

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination-demo-sql',
        locale="en-us",
        columns=[
            {
                'title': (f"Field {column[2:]}" if column.startswith('字段') and column[2:].isdigit() else column),
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination-demo-sql', 'data'),
    Input('table-server-side-mode-pagination-demo-sql', 'pagination'),
)
def table_server_side_mode_pagination_demo_sql(pagination):
    if pagination:
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        time.sleep(0.5)
        return list(data_frame)

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/database_pagination_filter.py`
```python
import time
import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State
from peewee import fn

from i18n import get_current_locale
from server import app

from .mock_data import DemoTable


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()
    field_names = list(DemoTable._meta.fields.keys())
    col_width = f'calc(100% / {len(field_names)})'

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+filter-demo-sql',
                columns=[
                    {
                        'title': column,
                        'dataIndex': column,
                        'width': col_width,
                    }
                    for column in field_names
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                filterOptions={
                    '字段1': {'filterMode': 'keyword'},
                    '字段2': {
                        'filterCustomItems': [
                            item.字段2
                            for item in (
                                DemoTable.select(DemoTable.字段2).distinct()
                            )
                        ],
                        'filterMultiple': True,
                        'filterSearch': True,
                    },
                },
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+filter-demo-sql',
                locale='en-us',
                columns=[
                    {
                        'title': (
                            f'Field {column[2:]}'
                            if column.startswith('字段')
                            and column[2:].isdigit()
                            else column
                        ),
                        'dataIndex': column,
                        'width': 'calc(100% / {})'.format(
                            len(DemoTable._meta.fields)
                        ),
                    }
                    for column in DemoTable._meta.fields.keys()
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                # filterOptions 的键必须与 dataIndex 完全一致（保留底层字段名）
                filterOptions={
                    '字段1': {'filterMode': 'keyword'},
                    '字段2': {
                        'filterCustomItems': [
                            item.字段2
                            for item in (
                                DemoTable.select(DemoTable.字段2).distinct()
                            )
                        ],
                        'filterMultiple': True,
                        'filterSearch': True,
                    },
                },
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-sql', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-sql', 'filter'),
    ],
    State('table-server-side-mode-pagination+filter-demo-sql', 'filterOptions'),
)
def table_server_side_mode_pagination_filter_demo_sql(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        # 若存在至少一项有效的筛选操作
        if filter_ and any([value for value in filter_.values()]):
            # 根据当前分页，从 DemoTable 中抽取对应记录
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                getattr(DemoTable, valid_filters[0][0]) << valid_filters[0][1]
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else getattr(DemoTable, valid_filters[0][0]).contains(
                    valid_filters[0][1][0]
                )
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions = filter_conditions & (
                    getattr(DemoTable, valid_filter[0]) << valid_filter[1]
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else getattr(DemoTable, valid_filter[0]).contains(
                        valid_filter[1][0]
                    )
                )

            match_records_count = (
                DemoTable.select(fn.count(DemoTable.id))
                .where(filter_conditions)
                .scalar()
            )

            data_frame = (
                DemoTable.select()
                .where(filter_conditions)
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )

            return [
                list(data_frame),
                {**pagination, 'total': match_records_count},
            ]

        # 无筛选：按分页直接返回
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )

        return [
            list(data_frame),
            {
                **pagination,
                'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            },
        ]

    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+filter-demo-sql',
        columns=[
            {
                'title': column,
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        filterOptions={
            '字段1': {'filterMode': 'keyword'},
            '字段2': {
                'filterCustomItems': [
                    item.字段2
                    for item in (DemoTable.select(DemoTable.字段2).distinct())
                ],
                'filterMultiple': True,
                'filterSearch': True,
            },
        },
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-sql', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-sql', 'filter'),
    ],
    State('table-server-side-mode-pagination+filter-demo-sql', 'filterOptions'),
)
def table_server_side_mode_pagination_filter_demo_sql(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        # 若存在至少一项有效的筛选操作
        if filter_ and any([value for value in filter_.values()]):
            # 根据当前分页，从 DemoTable 中抽取对应记录
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                getattr(DemoTable, valid_filters[0][0]) << valid_filters[0][1]
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else getattr(DemoTable, valid_filters[0][0]).contains(
                    valid_filters[0][1][0]
                )
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions = filter_conditions & (
                    getattr(DemoTable, valid_filter[0]) << valid_filter[1]
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else getattr(DemoTable, valid_filter[0]).contains(
                        valid_filter[1][0]
                    )
                )

            match_records_count = (
                DemoTable.select(fn.count(DemoTable.id))
                .where(filter_conditions)
                .scalar()
            )

            data_frame = (
                DemoTable.select()
                .where(filter_conditions)
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )

            return [
                list(data_frame),
                {**pagination, 'total': match_records_count},
            ]

        # 无筛选：按分页直接返回
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )

        return [
            list(data_frame),
            {
                **pagination,
                'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            },
        ]

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+filter-demo-sql',
        locale='en-us',
        columns=[
            {
                'title': (
                    f'Field {column[2:]}'
                    if column.startswith('字段')
                    and column[2:].isdigit()
                    else column
                ),
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (
                DemoTable.select(fn.count(DemoTable.id)).scalar()
            ),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        # filterOptions 的键必须与 dataIndex 完全一致（保留底层字段名）
        filterOptions={
            '字段1': {'filterMode': 'keyword'},
            '字段2': {
                'filterCustomItems': [
                    item.字段2
                    for item in (
                        DemoTable.select(DemoTable.字段2).distinct()
                    )
                ],
                'filterMultiple': True,
                'filterSearch': True,
            },
        },
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-sql', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-sql', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-sql', 'filter'),
    ],
    State('table-server-side-mode-pagination+filter-demo-sql', 'filterOptions'),
)
def table_server_side_mode_pagination_filter_demo_sql(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        # 若存在至少一项有效的筛选操作
        if filter_ and any([value for value in filter_.values()]):
            # 根据当前分页，从 DemoTable 中抽取对应记录
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                getattr(DemoTable, valid_filters[0][0]) << valid_filters[0][1]
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else getattr(DemoTable, valid_filters[0][0]).contains(
                    valid_filters[0][1][0]
                )
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions = filter_conditions & (
                    getattr(DemoTable, valid_filter[0]) << valid_filter[1]
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else getattr(DemoTable, valid_filter[0]).contains(
                        valid_filter[1][0]
                    )
                )

            match_records_count = (
                DemoTable.select(fn.count(DemoTable.id))
                .where(filter_conditions)
                .scalar()
            )

            data_frame = (
                DemoTable.select()
                .where(filter_conditions)
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )

            return [
                list(data_frame),
                {**pagination, 'total': match_records_count},
            ]

        # 无筛选：按分页直接返回
        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )

        return [
            list(data_frame),
            {
                **pagination,
                'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            },
        ]

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/database_pagination_multiple_sort.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from peewee import fn

from i18n import get_current_locale
from server import app

from .mock_data import DemoTable


def render() -> Component:
    current_locale = get_current_locale()
    field_names = list(DemoTable._meta.fields.keys())
    col_width = f'calc(100% / {len(field_names)})'

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+multi-sort-demo-sql',
                columns=[
                    {
                        'title': column,
                        'dataIndex': column,
                        'width': col_width,
                    }
                    for column in field_names
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={
                    'sortDataIndexes': field_names,
                    'multiple': 'auto',
                },
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+multi-sort-demo-sql',
                locale='en-us',
                columns=[
                    {
                        'title': (
                            f'Field {column[2:]}'
                            if column.startswith('字段')
                            and column[2:].isdigit()
                            else column
                        ),
                        'dataIndex': column,
                        'width': 'calc(100% / {})'.format(
                            len(DemoTable._meta.fields)
                        ),
                    }
                    for column in DemoTable._meta.fields.keys()
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={
                    'sortDataIndexes': list(DemoTable._meta.fields.keys()),
                    'multiple': 'auto',
                },
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-sql', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    *[
                        (
                            getattr(DemoTable, column)
                            if order == 'ascend'
                            else getattr(DemoTable, column).desc()
                        )
                        for column, order in zip(
                            sorter['columns'], sorter['orders']
                        )
                    ]
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update


def code_string() -> list:
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+multi-sort-demo-sql',
        columns=[
            {
                'title': column,
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': list(DemoTable._meta.fields.keys()),
            'multiple': 'auto',
        },
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-sql', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    *[
                        (
                            getattr(DemoTable, column)
                            if order == 'ascend'
                            else getattr(DemoTable, column).desc()
                        )
                        for column, order in zip(
                            sorter['columns'], sorter['orders']
                        )
                    ]
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+multi-sort-demo-sql',
        locale='en-us',
        columns=[
            {
                'title': (
                    f'Field {column[2:]}'
                    if column.startswith('字段')
                    and column[2:].isdigit()
                    else column
                ),
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (
                DemoTable.select(fn.count(DemoTable.id)).scalar()
            ),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': list(DemoTable._meta.fields.keys()),
            'multiple': 'auto',
        },
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-sql', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-sql', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    *[
                        (
                            getattr(DemoTable, column)
                            if order == 'ascend'
                            else getattr(DemoTable, column).desc()
                        )
                        for column, order in zip(
                            sorter['columns'], sorter['orders']
                        )
                    ]
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/database_pagination_single_sort.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output
from peewee import fn

from i18n import get_current_locale
from server import app

from .mock_data import DemoTable


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()
    field_names = list(DemoTable._meta.fields.keys())
    col_width = f'calc(100% / {len(field_names)})'

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+sort-demo-sql',
                columns=[
                    {
                        'title': column,
                        'dataIndex': column,
                        'width': col_width,
                    }
                    for column in field_names
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={'sortDataIndexes': field_names},
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+sort-demo-sql',
                locale='en-us',
                columns=[
                    {
                        'title': (
                            f'Field {column[2:]}'
                            if column.startswith('字段')
                            and column[2:].isdigit()
                            else column
                        ),
                        'dataIndex': column,
                        'width': 'calc(100% / {})'.format(
                            len(DemoTable._meta.fields)
                        ),
                    }
                    for column in DemoTable._meta.fields.keys()
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': (
                        DemoTable.select(fn.count(DemoTable.id)).scalar()
                    ),
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={
                    'sortDataIndexes': list(DemoTable._meta.fields.keys())
                },
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-sql', 'data'),
    [
        Input('table-server-side-mode-pagination+sort-demo-sql', 'pagination'),
        Input('table-server-side-mode-pagination+sort-demo-sql', 'sorter'),
    ],
)
def table_server_side_mode_pagination_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    getattr(DemoTable, sorter['columns'][0])
                    if sorter['orders'][0] == 'ascend'
                    else getattr(DemoTable, sorter['columns'][0]).desc()
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+sort-demo-sql',
        columns=[
            {
                'title': column,
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (DemoTable.select(fn.count(DemoTable.id)).scalar()),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': list(DemoTable._meta.fields.keys())
        },
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-sql', 'data'),
    [
        Input('table-server-side-mode-pagination+sort-demo-sql', 'pagination'),
        Input('table-server-side-mode-pagination+sort-demo-sql', 'sorter'),
    ],
)
def table_server_side_mode_pagination_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    getattr(DemoTable, sorter['columns'][0])
                    if sorter['orders'][0] == 'ascend'
                    else getattr(DemoTable, sorter['columns'][0]).desc()
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+sort-demo-sql',
        locale='en-us',
        columns=[
            {
                'title': (
                    f'Field {column[2:]}'
                    if column.startswith('字段')
                    and column[2:].isdigit()
                    else column
                ),
                'dataIndex': column,
                'width': 'calc(100% / {})'.format(
                    len(DemoTable._meta.fields)
                ),
            }
            for column in DemoTable._meta.fields.keys()
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': (
                DemoTable.select(fn.count(DemoTable.id)).scalar()
            ),
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': list(DemoTable._meta.fields.keys())
        },
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-sql', 'data'),
    [
        Input('table-server-side-mode-pagination+sort-demo-sql', 'pagination'),
        Input('table-server-side-mode-pagination+sort-demo-sql', 'sorter'),
    ],
)
def table_server_side_mode_pagination_sort_demo_sql(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = (
                DemoTable.select()
                .order_by(
                    getattr(DemoTable, sorter['columns'][0])
                    if sorter['orders'][0] == 'ascend'
                    else getattr(DemoTable, sorter['columns'][0]).desc()
                )
                .limit(pagination['pageSize'])
                .offset((pagination['current'] - 1) * pagination['pageSize'])
                .dicts()
            )
            return list(data_frame)

        data_frame = (
            DemoTable.select()
            .limit(pagination['pageSize'])
            .offset((pagination['current'] - 1) * pagination['pageSize'])
            .dicts()
        )
        return list(data_frame)

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/mock_data.py`
```python
import numpy as np
import pandas as pd
from peewee import CharField, IntegerField, Model, SqliteDatabase, fn

# 生成演示用数据框
demo_df = (
    pd.DataFrame(
        {
            'id': list(range(1, 100001)),
            '字段1': np.random.choice(
                [
                    f'{s}{n}'
                    for s in list('abcdefghij')
                    for n in range(1, 10001)
                ],
                100000,
                replace=False,
            ),
            '字段2': np.random.choice(
                [f'类型{t}' for t in range(1, 11) for n in range(10000)],
                100000,
                replace=False,
            ),
        }
    )
    # 打乱顺序
    .sample(frac=1, replace=False)
)


# 构造演示用数据库表模型类，基于sqlite+peewee
db = SqliteDatabase('./demo_table.db')


class DemoTable(Model):
    id = IntegerField()

    字段1 = CharField()

    字段2 = CharField()

    class Meta:
        table_name = 'demo_table'
        database = db


# 创建表格并插入示例数据
db.create_tables([DemoTable])

# 为方便调试，先检查数据表中是否已有记录，若有则跳过数据插入
with db.atomic():
    if (DemoTable.select(fn.count(DemoTable.id)).scalar()) == 0:
        # 分批插入
        for batch in range(10):
            (
                DemoTable.insert_many(
                    demo_df.iloc[
                        batch * 10000 : (batch + 1) * 10000, :
                    ].to_dict('records')
                ).execute()
            )

```

### `views/AntdTableServerSideMode/demos/pandas_pagination.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app

from .mock_data import demo_df


def _en_title(name: str) -> str:
    return (
        f'Field {name[2:]}'
        if name.startswith('字段') and name[2:].isdigit()
        else name
    )


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination-demo-pandas',
                columns=[
                    {'title': column, 'dataIndex': column}
                    for column in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                tableLayout='fixed',
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination-demo-pandas',
                locale='en-us',
                # translate titles; keep dataIndex as original keys
                columns=[
                    {'title': _en_title(col), 'dataIndex': col}
                    for col in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                tableLayout='fixed',
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination-demo-pandas', 'data'),
    Input('table-server-side-mode-pagination-demo-pandas', 'pagination'),
)
def table_server_side_mode_pagination_demo_pandas(pagination):
    if pagination:
        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]

        time.sleep(0.5)  # 渲染加载动画更好看 ^_^
        return data_frame.to_dict('records')

    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination-demo-pandas',
        columns=[
            {
                'title': column,
                'dataIndex': column,
            }
            for column in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        tableLayout='fixed',
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination-demo-pandas', 'data'),
    Input('table-server-side-mode-pagination-demo-pandas', 'pagination'),
)
def table_server_side_mode_pagination_demo_pandas(pagination):
    if pagination:
        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize']
            : pagination['current'] * pagination['pageSize'],
            :,
        ]

        time.sleep(0.5)
        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination-demo-pandas',
        locale="en-us",
        columns=[
            {
                'title': (f"Field {col[2:]}" if col.startswith('字段') and col[2:].isdigit() else col),
                'dataIndex': col,
            }
            for col in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        tableLayout='fixed',
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination-demo-pandas', 'data'),
    Input('table-server-side-mode-pagination-demo-pandas', 'pagination'),
)
def table_server_side_mode_pagination_demo_pandas(pagination):
    if pagination:
        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize']
            : pagination['current'] * pagination['pageSize'],
            :,
        ]

        time.sleep(0.5)
        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/pandas_pagination_filter.py`
```python
import time
import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from i18n import get_current_locale
from server import app

from .mock_data import demo_df


def _en_title(name: str) -> str:
    return (
        f'Field {name[2:]}'
        if name.startswith('字段') and name[2:].isdigit()
        else name
    )


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+filter-demo-pandas',
                columns=[
                    {'title': column, 'dataIndex': column}
                    for column in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                filterOptions={
                    '字段1': {'filterMode': 'keyword'},
                    '字段2': {
                        'filterCustomItems': demo_df['字段2'].unique(),
                        'filterMultiple': True,
                        'filterSearch': True,
                    },
                },
                tableLayout='fixed',
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+filter-demo-pandas',
                locale='en-us',
                # Titles translated; dataIndex must remain the original column keys
                columns=[
                    {'title': _en_title(col), 'dataIndex': col}
                    for col in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                # filterOptions keys must match dataIndex (original column names)
                filterOptions={
                    '字段1': {'filterMode': 'keyword'},
                    '字段2': {
                        'filterCustomItems': demo_df['字段2'].unique(),
                        'filterMultiple': True,
                        'filterSearch': True,
                    },
                },
                tableLayout='fixed',
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-pandas', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-pandas', 'filter'),
    ],
    State(
        'table-server-side-mode-pagination+filter-demo-pandas', 'filterOptions'
    ),
)
def table_server_side_mode_pagination_filter_demo_pandas(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        if filter_ and any([value for value in filter_.values()]):
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                f'`{valid_filters[0][0]}` == {valid_filters[0][1]}'
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else f'`{valid_filters[0][0]}`.str.contains("{valid_filters[0][1][0]}")'
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions += ' and '
                filter_conditions += (
                    f'`{valid_filter[0]}` == {valid_filter[1]}'
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else f'`{valid_filter[0]}`.str.contains("{valid_filter[1][0]}")'
                )

            match_records_count = demo_df.query(filter_conditions).shape[0]

            data_frame = demo_df.query(filter_conditions).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]

            return [
                data_frame.to_dict('records'),
                {**pagination, 'total': match_records_count},
            ]

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]

        return [
            data_frame.to_dict('records'),
            {**pagination, 'total': demo_df.shape[0]},
        ]

    return dash.no_update


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+filter-demo-pandas',
        columns=[
            {
                'title': column,
                'dataIndex': column,
            }
            for column in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        filterOptions={
            '字段1': {'filterMode': 'keyword'},
            '字段2': {
                'filterCustomItems': demo_df['字段2'].unique(),
                'filterMultiple': True,
                'filterSearch': True,
            },
        },
        tableLayout='fixed',
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-pandas', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-pandas', 'filter'),
    ],
    State(
        'table-server-side-mode-pagination+filter-demo-pandas', 'filterOptions'
    ),
)
def table_server_side_mode_pagination_filter_demo_pandas(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        if filter_ and any([value for value in filter_.values()]):
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                f'`{valid_filters[0][0]}` == {valid_filters[0][1]}'
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else f'`{valid_filters[0][0]}`.str.contains("{valid_filters[0][1][0]}")'
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions += ' and '
                filter_conditions += (
                    f'`{valid_filter[0]}` == {valid_filter[1]}'
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else f'`{valid_filter[0]}`.str.contains("{valid_filter[1][0]}")'
                )

            match_records_count = demo_df.query(filter_conditions).shape[0]

            data_frame = demo_df.query(filter_conditions).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]

            return [
                data_frame.to_dict('records'),
                {**pagination, 'total': match_records_count},
            ]

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]

        return [
            data_frame.to_dict('records'),
            {**pagination, 'total': demo_df.shape[0]},
        ]

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+filter-demo-pandas',
        locale="en-us",
        columns=[
            {
                'title': (f"Field {col[2:]}" if col.startswith('字段') and col[2:].isdigit() else col),
                'dataIndex': col,
            }
            for col in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        # filterOptions keys must match the original dataIndex values
        filterOptions={
            '字段1': {'filterMode': 'keyword'},
            '字段2': {
                'filterCustomItems': demo_df['字段2'].unique(),
                'filterMultiple': True,
                'filterSearch': True,
            },
        },
        tableLayout='fixed',
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    [
        Output('table-server-side-mode-pagination+filter-demo-pandas', 'data'),
        Output(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
    ],
    [
        Input(
            'table-server-side-mode-pagination+filter-demo-pandas', 'pagination'
        ),
        Input('table-server-side-mode-pagination+filter-demo-pandas', 'filter'),
    ],
    State(
        'table-server-side-mode-pagination+filter-demo-pandas', 'filterOptions'
    ),
)
def table_server_side_mode_pagination_filter_demo_pandas(
    pagination, filter_, filterOptions
):
    if pagination:
        time.sleep(0.5)  # 渲染加载动画更好看 ^_^

        if filter_ and any([value for value in filter_.values()]):
            valid_filters = [
                (key, value) for key, value in filter_.items() if value
            ]

            filter_conditions = (
                f'`{valid_filters[0][0]}` == {valid_filters[0][1]}'
                if filterOptions[valid_filters[0][0]].get('filterMode')
                != 'keyword'
                else f'`{valid_filters[0][0]}`.str.contains("{valid_filters[0][1][0]}")'
            )

            for valid_filter in valid_filters[1:]:
                filter_conditions += ' and '
                filter_conditions += (
                    f'`{valid_filter[0]}` == {valid_filter[1]}'
                    if filterOptions[valid_filter[0]].get('filterMode')
                    != 'keyword'
                    else f'`{valid_filter[0]}`.str.contains("{valid_filter[1][0]}")'
                )

            match_records_count = demo_df.query(filter_conditions).shape[0]

            data_frame = demo_df.query(filter_conditions).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]

            return [
                data_frame.to_dict('records'),
                {**pagination, 'total': match_records_count},
            ]

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]

        return [
            data_frame.to_dict('records'),
            {**pagination, 'total': demo_df.shape[0]},
        ]

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/pandas_pagination_multiple_sort.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app

from .mock_data import demo_df


def _en_title(name: str) -> str:
    return (
        f'Field {name[2:]}'
        if name.startswith('字段') and name[2:].isdigit()
        else name
    )


def render() -> Component:
    """渲染当前演示用例"""

    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+multi-sort-demo-pandas',
                columns=[
                    {'title': column, 'dataIndex': column}
                    for column in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={
                    'sortDataIndexes': list(demo_df.columns),
                    'multiple': 'auto',
                },
                tableLayout='fixed',
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+multi-sort-demo-pandas',
                locale='en-us',
                columns=[
                    {'title': _en_title(col), 'dataIndex': col}
                    for col in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={
                    'sortDataIndexes': list(demo_df.columns),
                    'multiple': 'auto',
                },
                tableLayout='fixed',
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-pandas', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_pandas(
    pagination, sorter
):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = demo_df.sort_values(
                sorter['columns'],
                ascending=[item == 'ascend' for item in sorter['orders']],
            ).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]
            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]
        return data_frame.to_dict('records')

    return dash.no_update


def code_string() -> list:
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+multi-sort-demo-pandas',
        columns=[
            {
                'title': column,
                'dataIndex': column,
            }
            for column in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': demo_df.columns,
            'multiple': 'auto',
        },
        tableLayout='fixed',
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-pandas', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_pandas(
    pagination, sorter
):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = demo_df.sort_values(
                sorter['columns'],
                ascending=[item == 'ascend' for item in sorter['orders']],
            ).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]
            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]
        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+multi-sort-demo-pandas',
        locale="en-us",
        columns=[
            {
                'title': (f"Field {col[2:]}" if col.startswith('字段') and col[2:].isdigit() else col),
                'dataIndex': col,
            }
            for col in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={
            'sortDataIndexes': demo_df.columns,
            'multiple': 'auto',
        },
        tableLayout='fixed',
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+multi-sort-demo-pandas', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas',
            'pagination',
        ),
        Input(
            'table-server-side-mode-pagination+multi-sort-demo-pandas', 'sorter'
        ),
    ],
)
def table_server_side_mode_pagination_multi_sort_demo_pandas(
    pagination, sorter
):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = demo_df.sort_values(
                sorter['columns'],
                ascending=[item == 'ascend' for item in sorter['orders']],
            ).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]
            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]
        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]

```

### `views/AntdTableServerSideMode/demos/pandas_pagination_single_sort.py`
```python
import time

import dash
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app

from .mock_data import demo_df


def _en_title(name: str) -> str:
    return (
        f'Field {name[2:]}'
        if name.startswith('字段') and name[2:].isdigit()
        else name
    )


def render() -> Component:
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+sort-demo-pandas',
                columns=[
                    {'title': column, 'dataIndex': column}
                    for column in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={'sortDataIndexes': list(demo_df.columns)},
                tableLayout='fixed',
            ),
            text='数据加载中',
            size='small',
        )

    elif current_locale == 'en-us':
        demo_contents = fac.AntdSpin(
            fac.AntdTable(
                id='table-server-side-mode-pagination+sort-demo-pandas',
                locale='en-us',
                columns=[
                    {'title': _en_title(col), 'dataIndex': col}
                    for col in demo_df.columns
                ],
                bordered=True,
                mode='server-side',
                pagination={
                    'total': demo_df.shape[0],
                    'current': 1,
                    'pageSize': 5,
                    'showSizeChanger': True,
                    'pageSizeOptions': [5, 10],
                    'position': 'topCenter',
                    'showQuickJumper': True,
                },
                sortOptions={'sortDataIndexes': list(demo_df.columns)},
                tableLayout='fixed',
            ),
            text='Loading data',
            size='small',
        )

    return demo_contents


@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-pandas', 'data'),
    [
        Input(
            'table-server-side-mode-pagination+sort-demo-pandas', 'pagination'
        ),
        Input('table-server-side-mode-pagination+sort-demo-pandas', 'sorter'),
    ],
)
def table_server_side_mode_pagination_filter_demo_pandas(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = demo_df.sort_values(
                sorter['columns'][0],
                ascending=(sorter['orders'][0] == 'ascend'),
            ).iloc[
                (pagination['current'] - 1)
                * pagination['pageSize'] : pagination['current']
                * pagination['pageSize'],
                :,
            ]
            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize'] : pagination[
                'current'
            ]
            * pagination['pageSize'],
            :,
        ]
        return data_frame.to_dict('records')

    return dash.no_update


def code_string() -> list:
    current_locale = get_current_locale()

    if current_locale == 'zh-cn':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+sort-demo-pandas',
        columns=[
            {
                'title': column,
                'dataIndex': column,
            }
            for column in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={'sortDataIndexes': demo_df.columns},
        tableLayout='fixed',
    ),
    text='数据加载中',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-pandas', 'data'),
    [
        Input('table-server-side-mode-pagination+sort-demo-pandas', 'pagination'),
        Input('table-server-side-mode-pagination+sort-demo-pandas', 'sorter'),
    ],
)
def table_server_side_mode_pagination_filter_demo_pandas(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter['columns']:
            data_frame = demo_df.sort_values(
                sorter['columns'][0], ascending=sorter['orders'][0] == 'ascend'
            ).iloc[
                (pagination['current'] - 1) * pagination['pageSize']
                : pagination['current'] * pagination['pageSize'],
                :,
            ]

            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize']
            : pagination['current'] * pagination['pageSize'],
            :,
        ]

        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]
    elif current_locale == 'en-us':
        return [
            {
                'code': """
fac.AntdSpin(
    fac.AntdTable(
        id='table-server-side-mode-pagination+sort-demo-pandas',
        locale="en-us",
        columns=[
            {
                'title': (f"Field {col[2:]}" if col.startswith('字段') and col[2:].isdigit() else col),
                'dataIndex': col,
            }
            for col in demo_df.columns
        ],
        bordered=True,
        mode='server-side',
        pagination={
            'total': demo_df.shape[0],
            'current': 1,
            'pageSize': 5,
            'showSizeChanger': True,
            'pageSizeOptions': [5, 10],
            'position': 'topCenter',
            'showQuickJumper': True,
        },
        sortOptions={'sortDataIndexes': demo_df.columns},
        tableLayout='fixed',
    ),
    text='Loading data',
    size='small',
)

...

@app.callback(
    Output('table-server-side-mode-pagination+sort-demo-pandas', 'data'),
    [
        Input('table-server-side-mode-pagination+sort-demo-pandas', 'pagination'),
        Input('table-server-side-mode-pagination+sort-demo-pandas', 'sorter'),
    ],
)
def table_server_side_mode_pagination_filter_demo_pandas(pagination, sorter):
    if pagination:
        time.sleep(0.5)

        if sorter and sorter.get('columns'):
            data_frame = demo_df.sort_values(
                sorter['columns'][0], ascending=(sorter['orders'][0] == 'ascend')
            ).iloc[
                (pagination['current'] - 1) * pagination['pageSize']
                : pagination['current'] * pagination['pageSize'],
                :,
            ]

            return data_frame.to_dict('records')

        data_frame = demo_df.iloc[
            (pagination['current'] - 1) * pagination['pageSize']
            : pagination['current'] * pagination['pageSize'],
            :,
        ]

        return data_frame.to_dict('records')

    return dash.no_update
"""
            }
        ]

```
