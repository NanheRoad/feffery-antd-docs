# 高级用法

## `views/advanced_usage/advanced_classname.py`
```python
from dash import html
import feffery_antd_components as fac
import feffery_utils_components as fuc
import feffery_markdown_components as fmc
from dash.dependencies import Component


def render() -> Component:
    """渲染“进阶className的使用”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[
                            {'title': '进阶使用'},
                            {'title': '进阶className的使用'},
                        ]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            '从',
                            fac.AntdText('0.2.x', code=True),
                            '版本开始，',
                            fac.AntdText('fac', strong=True),
                            '为常用的',
                            fac.AntdText('className', code=True),
                            '类参数全新引入“动态css类”的概念，使得我们可以以更加自由灵活的方式为组件配置css样式，具体用法说明如下：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdParagraph(
                        '注：此特性针对所有可接受dict型输入的className相关参数均可用',
                        type='secondary',
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdParagraph(
                        [
                            '在之前版本的',
                            fac.AntdText('fac', strong=True),
                            '中，参数',
                            fac.AntdText('className', code=True),
                            '只接受字符型输入，从而配合外部真实存在的css样式文件，或由',
                            fac.AntdText('fuc.FefferyStyle', code=True),
                            '定义的临时css样式代码中所定义的css类名，实现更复杂丰富的样式效果。',
                            '但从',
                            fac.AntdText('fac', strong=True),
                            fac.AntdText('0.2.x', code=True),
                            '版本开始，',
                            fac.AntdText('className', code=True),
                            '参数新增字典型输入支持，最基础的用法可以像参数',
                            fac.AntdText('style', code=True),
                            '一样直接设置css键值对属性，譬如我们如果想要为按钮添加渐变背景色：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    # 动态css类基础使用示例
                    fac.AntdButton(
                        '按钮示例',
                        size='large',
                        className={
                            'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
                            'color': 'white',
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
# 动态css类基础使用示例
fac.AntdButton(
    '按钮示例',
    size='large',
    className={
        'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
        'color': 'white'
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '如果想要在上面按钮示例的基础上，对按钮处于鼠标悬停、聚焦、点击等状态下的样式同样进行一些自定义覆盖，沿用传统的做法就比较繁琐，为方便演示，以配合组件',
                            fac.AntdText('fuc.FefferyStyle', code=True),
                            '为例，我们需要写好原生的css样式代码：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fuc.FefferyStyle(
                        rawStyle="""
.demo-button {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    transition: transform 0.2s ease;
}

/* 覆盖悬停状态样式 */
.demo-button:hover {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
}

/* 覆盖聚焦状态样式 */
.demo-button:focus {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
}

/* 覆盖点击状态样式 */
.demo-button:active {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
    transform: translateY(3px);
}
"""
                    ),
                    fac.AntdButton(
                        '按钮示例', size='large', className='demo-button'
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fuc.FefferyStyle(
    rawStyle='''
.demo-button {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    transition: transform 0.2s ease;
}

/* 覆盖悬停状态样式 */
.demo-button:hover {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
}

/* 覆盖聚焦状态样式 */
.demo-button:focus {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
}

/* 覆盖点击状态样式 */
.demo-button:active {
    background: linear-gradient(135deg,#6b73ff,#000dff);
    color: white;
    border-color: white;
    transform: translateY(3px);
}
'''
),
fac.AntdButton(
    '按钮示例',
    size='large',
    className='demo-button'
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '下面我们换成“动态css类”的方式😉，其中',
                            fac.AntdText('&', code=True),
                            '表示当前组件自身：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdButton(
                        '按钮示例',
                        size='large',
                        className={
                            'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
                            'color': 'white',
                            'transition': 'transform 0.2s ease',
                            # 悬停状态
                            '&:hover': {
                                'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
                                'color': 'white',
                                'borderColor': 'white',
                            },
                            # 聚焦状态
                            '&:focus': {
                                'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
                                'color': 'white',
                                'borderColor': 'white',
                            },
                            # 点击状态
                            '&:active': {
                                'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
                                'color': 'white',
                                'borderColor': 'white',
                                'transform': 'translateY(3px)',
                            },
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdButton(
    '按钮示例',
    size='large',
    className={
        'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
        'color': 'white',
        'transition': 'transform 0.2s ease',
        # 悬停状态
        '&:hover': {
            'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
            'color': 'white',
            'borderColor': 'white'
        },
        # 聚焦状态
        '&:focus': {
            'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
            'color': 'white',
            'borderColor': 'white'
        },
        # 点击状态
        '&:active': {
            'background': 'linear-gradient(135deg,#6b73ff,#000dff)',
            'color': 'white',
            'borderColor': 'white',
            'transform': 'translateY(3px)'
        },
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '通过这种方式，我们也可以非常方便灵活地修改复杂组件内部某些构件元素的样式，以',
                            fac.AntdText('AntdTable', strong=True),
                            '的复杂定制化样式为例（表格组件本身由于底层原因暂不支持动态css类，但我们可以为其包裹其他支持动态css类的容器组件实现需要的效果）：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    # fuc.FefferyDiv支持动态css类
                    fuc.FefferyDiv(
                        fac.AntdTable(
                            columns=[
                                {'dataIndex': f'字段{i}', 'title': f'字段{i}'}
                                for i in range(1, 6)
                            ],
                            data=[{f'字段{i}': 999 for i in range(1, 6)}] * 8,
                            pagination={'pageSize': 5},
                            bordered=True,
                            style={'width': '80%', 'margin': '0 auto'},
                        ),
                        className={
                            '.ant-pagination-total-text': {'color': '#c92a2a'},
                            '.ant-table-thead .ant-table-cell': {
                                'fontWeight': 'bold'
                            },
                            # 修改偶数行背景色
                            'tr:nth-child(even)': {'background': '#c3fae8'},
                            # 覆盖表格行鼠标悬停状态背景色
                            '.ant-table-tbody>tr.ant-table-row:hover>td, .ant-table-tbody>tr>td.ant-table-cell-row-hover': {
                                'background': '#ffec99'
                            },
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
# fuc.FefferyDiv支持动态css类
fuc.FefferyDiv(
    fac.AntdTable(
        columns=[
            {
                'dataIndex': f'字段{i}',
                'title': f'字段{i}'
            }
            for i in range(1, 6)
        ],
        data=[
            {
                f'字段{i}': 999
                for i in range(1, 6)
            }
        ] * 8,
        pagination={
            'pageSize': 5
        },
        bordered=True,
        style={
            'width': '80%',
            'margin': '0 auto'
        }
    ),
    className={
        '.ant-pagination-total-text': {
            'color': '#c92a2a'
        },
        '.ant-table-thead .ant-table-cell': {
            'fontWeight': 'bold'
        },
        # 修改偶数行背景色
        'tr:nth-child(even)': {
            'background': '#c3fae8'
        },
        # 覆盖表格行鼠标悬停状态背景色
        '.ant-table-tbody>tr.ant-table-row:hover>td, .ant-table-tbody>tr>td.ant-table-cell-row-hover': {
            'background': '#ffec99'
        }
    }
)
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'paddingRight': 40},
    )

```

## `views/advanced_usage/batch_props_values.py`
```python
import json
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染“属性批量监听”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[{'title': '进阶使用'}, {'title': '批量属性监听'}]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('fac', strong=True),
                            '中针对部分组件，提供了',
                            fac.AntdText('批量属性监听', strong=True),
                            '支持，通过参数',
                            fac.AntdText('batchPropsNames', code=True),
                            '声明的若干属性，可以在回调函数编排时，仅通过属性',
                            fac.AntdText('batchPropsValues', strong=True),
                            '进行监听和使用，以下方同时开启了节点选择、节点勾选、可拖拽、节点收藏等功能的树组件为例：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdSpace(
                        [
                            fac.AntdTree(
                                id='batch-props-values-demo',
                                treeData=[
                                    {
                                        'title': '四川省',
                                        'key': '四川省',
                                        'children': [
                                            {
                                                'title': '成都市',
                                                'key': '成都市',
                                            },
                                            {
                                                'title': '广安市',
                                                'key': '广安市',
                                            },
                                        ],
                                    },
                                    {
                                        'title': '重庆市',
                                        'key': '重庆市',
                                        'children': [
                                            {
                                                'title': '渝中区',
                                                'key': '渝中区',
                                                'children': [
                                                    {
                                                        'title': '解放碑街道',
                                                        'key': '解放碑街道',
                                                    }
                                                ],
                                            },
                                            {
                                                'title': '渝北区',
                                                'key': '渝北区',
                                            },
                                        ],
                                    },
                                ],
                                selectable=True,
                                checkable=True,
                                enableNodeFavorites=True,
                                draggable=True,
                                batchPropsNames=[
                                    'expandedKeys',
                                    'selectedKeys',
                                    'checkedKeys',
                                    'halfCheckedKeys',
                                    'draggedNodeKey',
                                    'clickedContextMenu',
                                    'favoritedKeys',
                                ],
                            ),
                            html.Pre(id='batch-props-values-demo-output'),
                        ],
                        direction='vertical',
                        style={'width': '100%'},
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdSpace(
    [
        fac.AntdTree(
            id='batch-props-values-demo',
            treeData=[
                {
                    'title': '四川省',
                    'key': '四川省',
                    'children': [
                        {
                            'title': '成都市',
                            'key': '成都市'
                        },
                        {
                            'title': '广安市',
                            'key': '广安市'
                        }
                    ]
                },
                {
                    'title': '重庆市',
                    'key': '重庆市',
                    'children': [
                        {
                            'title': '渝中区',
                            'key': '渝中区',
                            'children': [
                                {
                                    'title': '解放碑街道',
                                    'key': '解放碑街道'
                                }
                            ]
                        },
                        {
                            'title': '渝北区',
                            'key': '渝北区'
                        }
                    ]
                }
            ],
            selectable=True,
            checkable=True,
            enableNodeFavorites=True,
            draggable=True,
            batchPropsNames=[
                'expandedKeys',
                'selectedKeys',
                'checkedKeys',
                'halfCheckedKeys',
                'draggedNodeKey',
                'clickedContextMenu',
                'favoritedKeys'
            ]
        ),
        html.Pre(id='batch-props-values-demo-output')
    ],
    direction='vertical',
    style={
        'width': '100%'
    }
)

...

import json

...

@app.callback(
    Output('batch-props-values-demo-output', 'children'),
    Input('batch-props-values-demo', 'batchPropsValues')
)
def batch_props_values_demo(batchPropsValues):

    return json.dumps(
        dict(
            batchPropsValues=batchPropsValues
        ),
        indent=4,
        ensure_ascii=False
    )
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'paddingRight': 40},
    )


@app.callback(
    Output('batch-props-values-demo-output', 'children'),
    Input('batch-props-values-demo', 'batchPropsValues'),
)
def batch_props_values_demo(batchPropsValues):
    return json.dumps(
        dict(batchPropsValues=batchPropsValues), indent=4, ensure_ascii=False
    )

```

## `views/advanced_usage/import_alias.py`
```python
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component


def render() -> Component:
    """渲染“组件按别名导入”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[
                            {'title': '进阶使用'},
                            {'title': '组件按别名导入'},
                        ]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            '除了常规的',
                            fac.AntdText(
                                'import feffery_antd_components as fac',
                                code=True,
                            ),
                            '导入方式外，还可以使用',
                            fac.AntdText(
                                'import feffery_antd_components.alias as fac',
                                code=True,
                            ),
                            '进行组件的按别名导入，从而省略各组件名的',
                            fac.AntdText('Antd', code=True),
                            '前缀信息，譬如下面的示例代码：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdSpace(
                        [
                            fac.AntdButton(f'按钮{i}', type='primary')
                            for i in range(1, 6)
                        ]
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
import feffery_antd_components.alias as fac

...

fac.Space(
    [
        fac.Button(
            f'按钮{i}',
            type='primary'
        )
        for i in range(1, 6)
    ]
)
""",
                    ),
                    html.Div(style={'height': 'calc(100vh - 800px)'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'paddingRight': 40},
    )

```

## `views/advanced_usage/internationalization.py`
```python
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component


def render() -> Component:
    """渲染“国际化”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[{'title': '进阶使用'}, {'title': '国际化'}]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('fac', strong=True),
                            '针对部分组件，具有切换组件自带文案信息语种的功能，基于相关组件的参数',
                            fac.AntdText('locale', code=True),
                            '（默认为',
                            fac.AntdText('"zh-cn"', code=True),
                            '，即简体中文），也可以设置为',
                            fac.AntdText('"en-us"', code=True),
                            '切换到英文文案模式，典型例子如下：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdForm(
                        [
                            fac.AntdFormItem(
                                fac.AntdSpace(
                                    [
                                        fac.AntdDatePicker(),
                                        fac.AntdDateRangePicker(),
                                    ]
                                ),
                                label='locale="zh-cn"（默认）',
                            ),
                            fac.AntdFormItem(
                                fac.AntdSpace(
                                    [
                                        fac.AntdDatePicker(locale='en-us'),
                                        fac.AntdDateRangePicker(locale='en-us'),
                                    ]
                                ),
                                label='locale="en-us"',
                            ),
                        ],
                        layout='vertical',
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdForm(
    [
        fac.AntdFormItem(
            fac.AntdSpace(
                [
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker()
                ]
            ),
            label='locale="zh-cn"（默认）'
        ),

        fac.AntdFormItem(
            fac.AntdSpace(
                [
                    fac.AntdDatePicker(
                        locale='en-us'
                    ),
                    fac.AntdDateRangePicker(
                        locale='en-us'
                    )
                ]
            ),
            label='locale="en-us"'
        )
    ],
    layout='vertical'
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '上面介绍的例子是针对每个组件单独控制语种，而如果你的应用中存在着大量的需要设置为其他语种的组件，则可以将相关组件全部嵌套在全局配置组件',
                            fac.AntdText('AntdConfigProvider', strong=True),
                            '中，并为其设置参数',
                            fac.AntdText('locale="en-us"', code=True),
                            '，从而批量快捷覆盖设置内部元素的国际化语种',
                            '（更多内容请参考',
                            html.A(
                                'AntdConfigProvider',
                                href='/AntdConfigProvider',
                                target='_blank',
                            ),
                            '文档）：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdConfigProvider(
                        fac.AntdSpace(
                            [fac.AntdDatePicker(), fac.AntdDateRangePicker()]
                        ),
                        locale='en-us',
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdConfigProvider(
    fac.AntdSpace(
        [
            fac.AntdDatePicker(),
            fac.AntdDateRangePicker()
        ]
    ),
    locale='en-us'
)
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'marginRight': 40},
    )

```

## `views/advanced_usage/popup_container.py`
```python
from dash import html
import feffery_antd_components as fac
import feffery_utils_components as fuc
import feffery_markdown_components as fmc
from dash.dependencies import Component


def render() -> Component:
    """渲染“弹出层容器设置”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[
                            {'title': '进阶使用'},
                            {'title': '弹出层容器设置'},
                        ]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('fac', code=True),
                            '对所有具有悬浮弹出层元素的组件的显示稳定性进行了优化，对于所有设计有参数',
                            fac.AntdText('popupContainer', code=True),
                            '的组件，默认',
                            fac.AntdText('popupContainer="body"', code=True),
                            '，在此默认设定下相关组件悬浮弹出层的位置计算参照容器为页面根节点，此时如果我们在带有滚动条的局部容器内放置具有悬浮弹出层的组件，',
                            '当悬浮弹出层处于显示状态时，在对应局部容器内进行滚动时，这些悬浮弹出层会出现不跟随滚动的问题，就像下面的例子一样：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            html.Div(style={'height': 100}),
                            fac.AntdPopover(
                                fac.AntdButton('点我展开，接着滚动试试'),
                                title='悬浮弹出层局部滚动不跟随示例',
                                content='默认popupContainer="body"',
                                trigger='focus',
                            ),
                            html.Div(style={'height': 600}),
                        ],
                        style={
                            'height': 300,
                            'overflowY': 'auto',
                            'background': '#f1f3f5',
                            'padding': 25,
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        html.Div(
            style={
                'height': 100
            }
        ),
        fac.AntdPopover(
            fac.AntdButton(
                '点我展开，接着滚动试试'
            ),
            title='悬浮弹出层局部滚动不跟随示例',
            content='默认popupContainer="body"',
            trigger='focus'
        ),
        html.Div(
            style={
                'height': 600
            }
        ),
    ],
    style={
        'height': 300,
        'overflowY': 'auto',
        'background': '#f1f3f5',
        'padding': 25
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '面对这种情况，我们可以在悬浮弹出层所在的组件中，设置参数',
                            fac.AntdText('popupContainer="parent"', code=True),
                            '，同时确保对应容器css样式中的position为relative或absolute，从而将对应组件的悬浮弹出层参照容器从页面根节点，切换为这些组件各自的父容器，',
                            '从而确保相关悬浮弹出层可以被正确计算位置变化：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            html.Div(style={'height': 100}),
                            fac.AntdPopover(
                                fac.AntdButton('点我展开，接着滚动试试'),
                                title='悬浮弹出层局部滚动不跟随示例',
                                content='默认popupContainer="parent"',
                                trigger='focus',
                                popupContainer='parent',
                            ),
                            html.Div(style={'height': 600}),
                        ],
                        style={
                            'height': 300,
                            'overflowY': 'auto',
                            'background': '#f1f3f5',
                            'padding': 25,
                            'position': 'relative',
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        html.Div(
            style={
                'height': 100
            }
        ),
        fac.AntdPopover(
            fac.AntdButton(
                '点我展开，接着滚动试试'
            ),
            title='悬浮弹出层局部滚动不跟随示例',
            content='默认popupContainer="parent"',
            trigger='focus',
            popupContainer='parent'
        ),
        html.Div(
            style={
                'height': 600
            }
        ),
    ],
    style={
        'height': 300,
        'overflowY': 'auto',
        'background': '#f1f3f5',
        'padding': 25,
        'position': 'relative'
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '除了上面介绍的局部滚动场景以外，其他与悬浮弹出层锚点相关的场景下，妥善使用参数',
                            fac.AntdText('popupContainer', code=True),
                            '可以有效解决一些相关的显示问题，譬如在下面的“相对-绝对”经典布局中，由于其中的绝对定位容器设置了z-index，',
                            '导致其内部放置的',
                            fac.AntdText('AntdDropdown', strong=True),
                            '组件附带的悬浮展开层显示异常：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            fuc.FefferyDiv(
                                fac.AntdDropdown(
                                    title='下拉菜单测试',
                                    menuItems=[
                                        {'title': f'下拉子项{i}'}
                                        for i in range(1, 6)
                                    ],
                                ),
                                style={
                                    'position': 'absolute',
                                    'top': 25,
                                    'left': 25,
                                    'width': 200,
                                    'padding': '25px',
                                    'background': 'white',
                                    'borderRadius': 6,
                                    'zIndex': 99999,
                                },
                                shadow='always-shadow',
                            )
                        ],
                        style={
                            'height': 300,
                            'background': '#f8f9fa',
                            'position': 'relative',
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        fuc.FefferyDiv(
            fac.AntdDropdown(
                title='下拉菜单测试',
                menuItems=[
                    {
                        'title': f'下拉子项{i}'
                    }
                    for i in range(1, 6)
                ]
            ),
            style={
                'position': 'absolute',
                'top': 25,
                'left': 25,
                'width': 200,
                'padding': '25px',
                'background': 'white',
                'borderRadius': 6,
                'zIndex': 99999
            },
            shadow='always-shadow'
        )
    ],
    style={
        'height': 300,
        'background': '#f8f9fa',
        'position': 'relative'
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '而对上面例子中的',
                            fac.AntdText('AntdDropdown', strong=True),
                            '设置',
                            fac.AntdText('popupContainer="parent"', code=True),
                            '后，即可在这个场景下保证下拉展开菜单显示正常：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            fuc.FefferyDiv(
                                fac.AntdDropdown(
                                    title='下拉菜单测试',
                                    menuItems=[
                                        {'title': f'下拉子项{i}'}
                                        for i in range(1, 6)
                                    ],
                                    popupContainer='parent',
                                ),
                                style={
                                    'position': 'absolute',
                                    'top': 25,
                                    'left': 25,
                                    'width': 200,
                                    'padding': '25px',
                                    'background': 'white',
                                    'borderRadius': 6,
                                    'zIndex': 99999,
                                },
                                shadow='always-shadow',
                            )
                        ],
                        style={
                            'height': 300,
                            'background': '#f8f9fa',
                            'position': 'relative',
                        },
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        fuc.FefferyDiv(
            fac.AntdDropdown(
                title='下拉菜单测试',
                menuItems=[
                    {
                        'title': f'下拉子项{i}'
                    }
                    for i in range(1, 6)
                ],
                popupContainer='parent'
            ),
            style={
                'position': 'absolute',
                'top': 25,
                'left': 25,
                'width': 200,
                'padding': '25px',
                'background': 'white',
                'borderRadius': 6,
                'zIndex': 99999
            },
            shadow='always-shadow'
        )
    ],
    style={
        'height': 300,
        'background': '#f8f9fa',
        'position': 'relative'
    }
)
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'paddingRight': 40},
    )

```

## `views/advanced_usage/prop_persistence.py`
```python
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component


def render() -> Component:
    """渲染“属性持久化”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[{'title': '进阶使用'}, {'title': '属性持久化'}]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('fac', strong=True),
                            '中具有参数',
                            fac.AntdText('persistence', code=True),
                            '、',
                            fac.AntdText('persisted_props', code=True),
                            '、',
                            fac.AntdText('persistence_type', code=True),
                            '的组件，可使用',
                            fac.AntdText('属性持久化', strong=True),
                            '功能，开启后可分别在不同生命周期内对目标组件的属性进行记忆，这可能听起来比较抽象，让我们从下面的例子中了解更多：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdParagraph(
                        [
                            '下面的示例输入框，已设置了',
                            fac.AntdText('persistence=True', code=True),
                            '，即开启了默认的基于浏览器本地缓存的属性持久化功能，因此当我们在输入框内输入任意内容后，刷新页面，已输入的内容都会被记忆，因为',
                            fac.AntdText('value', code=True),
                            '属性是输入框组件属性持久化默认作用的目标属性之一：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdInput(
                        id='persistence-input-demo',
                        placeholder='请输入',
                        persistence=True,
                        style={'width': 256},
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdInput(
    id='persistence-input-demo',
    placeholder='请输入',
    persistence=True,
    style={
        'width': 256
    }
)
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '下面是支持属性持久化特性的全部组件，你可以在各自的文档页参数说明中了解更多：'
                        ]
                    ),
                    fac.AntdSpace(
                        [
                            fac.AntdCheckCard(
                                '持久化测试',
                                id='check-card-persistence-demo',
                                defaultChecked=True,
                                persistence=True,
                            ),
                            fac.AntdCheckCardGroup(
                                [
                                    fac.AntdCheckCard(f'选项{i}', value=i)
                                    for i in range(1, 6)
                                ],
                                id='check-card-group-persistence-demo',
                                size='small',
                                multiple=True,
                                defaultValue=[1, 2],
                                persistence=True,
                            ),
                            fac.AntdTabs(
                                id='tabs-persistence-demo',
                                items=[
                                    {
                                        'key': f'标签页{i}',
                                        'label': f'标签页{i}',
                                        'children': html.Div(
                                            f'这是标签页{i}的内容示例',
                                            style={
                                                'display': 'flex',
                                                'justifyContent': 'center',
                                                'alignItems': 'center',
                                                'fontSize': 18,
                                                'background': f'rgba(28, 126, 214, calc(1 - 0.2 * {i}))',
                                                'height': 200,
                                            },
                                        ),
                                    }
                                    for i in range(1, 6)
                                ],
                                defaultActiveKey='标签页1',
                                persistence=True,
                            ),
                            fac.AntdCalendar(
                                id='calendar-persistence-demo',
                                defaultValue='2023-01-01',
                                persistence=True,
                                style={'width': '300px'},
                            ),
                            fac.AntdCascader(
                                id='cascader-persistence-demo',
                                placeholder='请选择',
                                options=[
                                    {
                                        'value': '节点1',
                                        'label': '节点1',
                                        'children': [
                                            {
                                                'value': '节点1-1',
                                                'label': '节点1-1',
                                            },
                                            {
                                                'value': '节点1-2',
                                                'label': '节点1-2',
                                                'children': [
                                                    {
                                                        'value': '节点1-2-1',
                                                        'label': '节点1-2-1',
                                                    },
                                                    {
                                                        'value': '节点1-2-2',
                                                        'label': '节点1-2-2',
                                                    },
                                                ],
                                            },
                                        ],
                                    },
                                    {
                                        'value': '节点2',
                                        'label': '节点2',
                                        'children': [
                                            {
                                                'value': '节点2-1',
                                                'label': '节点2-1',
                                            },
                                            {
                                                'value': '节点2-2',
                                                'label': '节点2-2',
                                            },
                                        ],
                                    },
                                ],
                                persistence=True,
                                style={'width': '200px'},
                            ),
                            fac.AntdCheckbox(
                                id='checkbox-persistence-demo',
                                label='开启',
                                persistence=True,
                            ),
                            fac.AntdCheckboxGroup(
                                id='checkbox-group-persistence-demo',
                                options=[
                                    {'label': f'选项{i}', 'value': f'选项{i}'}
                                    for i in range(5)
                                ],
                                persistence=True,
                            ),
                            fac.AntdCollapse(
                                fac.AntdParagraph('内容示例' * 20),
                                id='collapse-persistence-demo',
                                isOpen=True,
                                title='回调示例',
                                persistence=True,
                                style={'width': 300},
                            ),
                            fac.AntdDatePicker(
                                id='date-picker-persistence-demo',
                                persistence=True,
                                style={'width': 175},
                            ),
                            fac.AntdDateRangePicker(
                                id='date-range-picker-persistence-demo',
                                persistence=True,
                                style={'width': 300},
                            ),
                            fac.AntdInput(
                                id='input-persistence-demo',
                                persistence=True,
                                style={'width': 150},
                            ),
                            fac.AntdInput(
                                id='input-password-persistence-demo',
                                mode='password',
                                passwordUseMd5=True,
                                persistence=True,
                                style={'width': 150},
                            ),
                            fac.AntdInputNumber(
                                id='input-number-persistence-demo',
                                persistence=True,
                                style={'width': 150},
                            ),
                            html.Div(
                                fac.AntdMenu(
                                    id='menu-persistence-demo',
                                    persistence=True,
                                    defaultSelectedKey='图标antd-home',
                                    menuItems=[
                                        {
                                            'component': 'Item',
                                            'props': {
                                                'key': f'图标{icon}',
                                                'title': f'图标{icon}',
                                                'icon': icon,
                                            },
                                        }
                                        for icon in [
                                            'antd-home',
                                            'antd-cloud-upload',
                                            'antd-bar-chart',
                                        ]
                                    ],
                                    mode='inline',
                                ),
                                style={'width': '250px'},
                            ),
                            fac.AntdPagination(
                                id='pagination-persistence-demo',
                                defaultPageSize=10,
                                total=100,
                                pageSizeOptions=[5, 10, 20],
                                showSizeChanger=True,
                                persistence=True,
                            ),
                            fac.AntdRadioGroup(
                                id='radio-group-persistence-demo',
                                options=[
                                    {'label': f'选项{c}', 'value': c}
                                    for c in list('abcdef')
                                ],
                                defaultValue='a',
                                persistence=True,
                            ),
                            fac.AntdRate(
                                id='rate-persistence-demo',
                                count=10,
                                allowHalf=True,
                                defaultValue=1,
                                persistence=True,
                            ),
                            fac.AntdSegmented(
                                id='segmented-persistence-demo',
                                options=[
                                    {'label': f'选项{i}', 'value': i}
                                    for i in range(1, 6)
                                ],
                                defaultValue=2,
                                persistence=True,
                            ),
                            fac.AntdSelect(
                                id='select-persistence-demo',
                                options=[
                                    {'label': f'选项{i}', 'value': f'选项{i}'}
                                    for i in range(1, 6)
                                ],
                                persistence=True,
                                style={'width': 200},
                            ),
                            fac.AntdSlider(
                                id='slider-persistence-demo',
                                min=0,
                                max=100,
                                defaultValue=33,
                                persistence=True,
                                style={'width': 300},
                            ),
                            fac.AntdSlider(
                                id='slider-range-persistence-demo',
                                range=True,
                                min=0,
                                max=100,
                                defaultValue=[10, 90],
                                persistence=True,
                                style={'width': 300},
                            ),
                            fac.AntdSwitch(
                                id='switch-persistence-demo', persistence=True
                            ),
                            fac.AntdTimePicker(
                                id='time-picker-persistence-demo',
                                defaultValue='06:00:00',
                                persistence=True,
                            ),
                            fac.AntdTimeRangePicker(
                                id='time-range-picker-persistence-demo',
                                defaultValue=['12:00:00', '13:00:00'],
                                persistence=True,
                            ),
                            fac.AntdTransfer(
                                id='transfer-persistence-demo',
                                dataSource=[
                                    {'key': i, 'title': f'选项{i}'}
                                    for i in range(1, 10)
                                ],
                                targetKeys=[2, 3, 4],
                                persistence=True,
                            ),
                            fac.AntdTree(
                                id='tree-persistence-demo',
                                treeData=[
                                    {
                                        'title': '四川省',
                                        'key': '四川省',
                                        'children': [
                                            {
                                                'title': '成都市',
                                                'key': '成都市',
                                            },
                                            {
                                                'title': '广安市',
                                                'key': '广安市',
                                            },
                                        ],
                                    },
                                    {
                                        'title': '重庆市',
                                        'key': '重庆市',
                                        'children': [
                                            {
                                                'title': '渝中区',
                                                'key': '渝中区',
                                                'children': [
                                                    {
                                                        'title': '解放碑街道',
                                                        'key': '解放碑街道',
                                                    }
                                                ],
                                            },
                                            {
                                                'title': '渝北区',
                                                'key': '渝北区',
                                            },
                                        ],
                                    },
                                ],
                                multiple=True,
                                checkable=True,
                                persistence=True,
                            ),
                            fac.AntdTreeSelect(
                                id='tree-select-persistence-demo',
                                treeData=[
                                    {
                                        'key': '节点1',
                                        'value': '1',
                                        'title': '节点1',
                                        'children': [
                                            {
                                                'key': f'节点1-{i}',
                                                'value': f'1-{i}',
                                                'title': f'节点1-{i}',
                                            }
                                            for i in range(1, 5)
                                        ],
                                    },
                                    {
                                        'key': '节点2',
                                        'value': '2',
                                        'title': '节点2',
                                    },
                                ],
                                placeholder='请选择',
                                persistence=True,
                                style={'width': 256},
                            ),
                            fac.AntdTreeSelect(
                                id='tree-select-multiple-persistence-demo',
                                treeData=[
                                    {
                                        'key': '节点1',
                                        'value': '1',
                                        'title': '节点1',
                                        'children': [
                                            {
                                                'key': f'节点1-{i}',
                                                'value': f'1-{i}',
                                                'title': f'节点1-{i}',
                                            }
                                            for i in range(1, 5)
                                        ],
                                    },
                                    {
                                        'key': '节点2',
                                        'value': '2',
                                        'title': '节点2',
                                    },
                                ],
                                placeholder='请选择',
                                multiple=True,
                                treeCheckable=True,
                                persistence=True,
                                style={'width': 256},
                            ),
                        ],
                        direction='vertical',
                        style={'width': '100%'},
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
fac.AntdSpace(
    [
        fac.AntdCheckCard(
            '持久化测试',
            id='check-card-persistence-demo',
            defaultChecked=True,
            persistence=True
        ),
        fac.AntdCheckCardGroup(
            [
                fac.AntdCheckCard(
                    f'选项{i}',
                    value=i
                )
                for i in range(1, 6)
            ],
            id='check-card-group-persistence-demo',
            size='small',
            multiple=True,
            defaultValue=[1, 2],
            persistence=True
        ),

        fac.AntdTabs(
            id='tabs-persistence-demo',
            items=[
                {
                    'key': f'标签页{i}',
                    'label': f'标签页{i}',
                    'children': html.Div(
                        f'这是标签页{i}的内容示例',
                        style={
                            'display': 'flex',
                            'justifyContent': 'center',
                            'alignItems': 'center',
                            'fontSize': 18,
                            'background': f'rgba(28, 126, 214, calc(1 - 0.2 * {i}))',
                            'height': 200
                        }
                    )
                }
                for i in range(1, 6)
            ],
            defaultActiveKey='标签页1',
            persistence=True
        ),
        fac.AntdCalendar(
            id='calendar-persistence-demo',
            defaultValue='2023-01-01',
            persistence=True,
            style={
                'width': '300px'
            }
        ),
        fac.AntdCascader(
            id='cascader-persistence-demo',
            placeholder='请选择',
            options=[
                {
                    'value': '节点1',
                    'label': '节点1',
                    'children': [
                        {
                            'value': '节点1-1',
                            'label': '节点1-1'
                        },
                        {
                            'value': '节点1-2',
                            'label': '节点1-2',
                            'children': [
                                {
                                    'value': '节点1-2-1',
                                    'label': '节点1-2-1'
                                },
                                {
                                    'value': '节点1-2-2',
                                    'label': '节点1-2-2'
                                }
                            ]
                        }
                    ]
                },
                {
                    'value': '节点2',
                    'label': '节点2',
                    'children': [
                        {
                            'value': '节点2-1',
                            'label': '节点2-1'
                        },
                        {
                            'value': '节点2-2',
                            'label': '节点2-2'
                        }
                    ]
                }
            ],
            persistence=True,
            style={
                'width': '200px'
            }
        ),
        fac.AntdCheckbox(
            id='checkbox-persistence-demo',
            label='开启',
            persistence=True
        ),
        fac.AntdCheckboxGroup(
            id='checkbox-group-persistence-demo',
            options=[
                {
                    'label': f'选项{i}',
                    'value': f'选项{i}'
                }
                for i in range(5)
            ],
            persistence=True
        ),
        fac.AntdCollapse(
            fac.AntdParagraph(
                '内容示例'*20
            ),
            id='collapse-persistence-demo',
            isOpen=True,
            title='回调示例',
            persistence=True,
            style={
                'width': 300
            }
        ),
        fac.AntdDatePicker(
            id='date-picker-persistence-demo',
            persistence=True,
            style={
                'width': 175
            },
        ),
        fac.AntdDateRangePicker(
            id='date-range-picker-persistence-demo',
            persistence=True,
            style={
                'width': 300
            },
        ),
        fac.AntdInput(
            id='input-persistence-demo',
            persistence=True,
            style={
                'width': 150
            }
        ),
        fac.AntdInput(
            id='input-password-persistence-demo',
            mode='password',
            passwordUseMd5=True,
            persistence=True,
            style={
                'width': 150
            }
        ),
        fac.AntdInputNumber(
            id='input-number-persistence-demo',
            persistence=True,
            style={
                'width': 150
            }
        ),

        html.Div(
            fac.AntdMenu(
                id='menu-persistence-demo',
                persistence=True,
                defaultSelectedKey='图标antd-home',
                menuItems=[
                    {
                        'component': 'Item',
                        'props': {
                            'key': f'图标{icon}',
                            'title': f'图标{icon}',
                            'icon': icon
                        }
                    }
                    for icon in [
                        'antd-home',
                        'antd-cloud-upload',
                        'antd-bar-chart'
                    ]
                ],
                mode='inline'
            ),
            style={
                'width': '250px'
            }
        ),
        fac.AntdPagination(
            id='pagination-persistence-demo',
            defaultPageSize=10,
            total=100,
            pageSizeOptions=[5, 10, 20],
            showSizeChanger=True,
            persistence=True
        ),
        fac.AntdRadioGroup(
            id='radio-group-persistence-demo',
            options=[
                {
                    'label': f'选项{c}',
                    'value': c
                }
                for c in list('abcdef')
            ],
            defaultValue='a',
            persistence=True
        ),
        fac.AntdRate(
            id='rate-persistence-demo',
            count=10,
            allowHalf=True,
            defaultValue=1,
            persistence=True
        ),
        fac.AntdSegmented(
            id='segmented-persistence-demo',
            options=[
                {
                    'label': f'选项{i}',
                    'value': i
                }
                for i in range(1, 6)
            ],
            defaultValue=2,
            persistence=True
        ),
        fac.AntdSelect(
            id='select-persistence-demo',
            options=[
                {
                    'label': f'选项{i}',
                    'value': f'选项{i}'
                }
                for i in range(1, 6)
            ],
            persistence=True,
            style={
                'width': 200
            }
        ),
        fac.AntdSlider(
            id='slider-persistence-demo',
            min=0,
            max=100,
            defaultValue=33,
            persistence=True,
            style={
                'width': 300
            }
        ),
        fac.AntdSlider(
            id='slider-range-persistence-demo',
            range=True,
            min=0,
            max=100,
            defaultValue=[10, 90],
            persistence=True,
            style={
                'width': 300
            }
        ),
        fac.AntdSwitch(
            id='switch-persistence-demo',
            persistence=True
        ),
        fac.AntdTimePicker(
            id='time-picker-persistence-demo',
            defaultValue='06:00:00',
            persistence=True
        ),
        fac.AntdTimeRangePicker(
            id='time-range-picker-persistence-demo',
            defaultValue=[
                '12:00:00',
                '13:00:00'
            ],
            persistence=True
        ),
        fac.AntdTransfer(
            id='transfer-persistence-demo',
            dataSource=[
                {
                    'key': i,
                    'title': f'选项{i}'
                }
                for i in range(1, 10)
            ],
            targetKeys=[2, 3, 4],
            persistence=True
        ),
        fac.AntdTree(
            id='tree-persistence-demo',
            treeData=[
                {
                    'title': '四川省',
                    'key': '四川省',
                    'children': [
                        {
                            'title': '成都市',
                            'key': '成都市'
                        },
                        {
                            'title': '广安市',
                            'key': '广安市'
                        }
                    ]
                },
                {
                    'title': '重庆市',
                    'key': '重庆市',
                    'children': [
                        {
                            'title': '渝中区',
                            'key': '渝中区',
                            'children': [
                                {
                                    'title': '解放碑街道',
                                    'key': '解放碑街道'
                                }
                            ]
                        },
                        {
                            'title': '渝北区',
                            'key': '渝北区'
                        }
                    ]
                }
            ],
            multiple=True,
            checkable=True,
            persistence=True
        ),
        fac.AntdTreeSelect(
            id='tree-select-persistence-demo',
            treeData=[
                {
                    'key': '节点1',
                    'value': '1',
                    'title': '节点1',
                    'children': [
                        {
                            'key': f'节点1-{i}',
                            'value': f'1-{i}',
                            'title': f'节点1-{i}'
                        }
                        for i in range(1, 5)
                    ]
                },
                {
                    'key': '节点2',
                    'value': '2',
                    'title': '节点2'
                }
            ],
            placeholder='请选择',
            persistence=True,
            style={
                'width': 256
            }
        ),
        fac.AntdTreeSelect(
            id='tree-select-multiple-persistence-demo',
            treeData=[
                {
                    'key': '节点1',
                    'value': '1',
                    'title': '节点1',
                    'children': [
                        {
                            'key': f'节点1-{i}',
                            'value': f'1-{i}',
                            'title': f'节点1-{i}'
                        }
                        for i in range(1, 5)
                    ]
                },
                {
                    'key': '节点2',
                    'value': '2',
                    'title': '节点2'
                }
            ],
            placeholder='请选择',
            multiple=True,
            treeCheckable=True,
            persistence=True,
            style={
                'width': 256
            }
        )
    ],
    direction='vertical',
    style={
        'width': '100%'
    }
)
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'marginRight': 40},
    )

```

## `views/advanced_usage/use_key_to_refresh.py`
```python
import uuid
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染“强制刷新组件”文档页"""

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(duration=0.3),
                    fac.AntdBreadcrumb(
                        items=[{'title': '进阶使用'}, {'title': '强制刷新组件'}]
                    ),
                    fac.AntdDivider(isDashed=True),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('fac', strong=True),
                            '中的全部组件都具有参数',
                            fac.AntdText('key', code=True),
                            '，对其进行更新可以实现对该组件的强制重载，譬如在下面的例子中，切换上面的类型，会对下方内容区的内容进行更新，',
                            '但当类型发生切换后，先前的滚动条位置会残留：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            fac.AntdSpace(
                                [
                                    fac.AntdRadioGroup(
                                        id='key-demo1-type',
                                        options=[
                                            {
                                                'label': f'类型{i}',
                                                'value': f'类型{i}',
                                            }
                                            for i in range(1, 6)
                                        ],
                                        defaultValue='类型1',
                                    ),
                                    fac.AntdSpace(
                                        id='key-demo1-output',
                                        style={
                                            'width': 200,
                                            'height': 100,
                                            'overflowY': 'auto',
                                            'border': '1px solid #dee2e6',
                                        },
                                    ),
                                ],
                                direction='vertical',
                            )
                        ],
                        style={'padding': 25},
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        fac.AntdSpace(
            [
                fac.AntdRadioGroup(
                    id='key-demo1-type',
                    options=[
                        {
                            'label': f'类型{i}',
                            'value': f'类型{i}',
                        }
                        for i in range(1, 6)
                    ],
                    defaultValue='类型1'
                ),

                fac.AntdSpace(
                    id='key-demo1-output',
                    style={
                        'width': 200,
                        'height': 100,
                        'overflowY': 'auto',
                        'border': '1px solid #dee2e6'
                    }
                )
            ],
            direction='vertical'
        )
    ],
    style={
        'padding': 25
    }
)

...

@app.callback(
    Output('key-demo1-output', 'children'),
    Input('key-demo1-type', 'value')
)
def key_demo1(value):

    return value * 100
""",
                    ),
                    fac.AntdParagraph(
                        [
                            '这时我们就可以使用',
                            fac.AntdText('key', code=True),
                            '来辅助强制重置：',
                        ],
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        [
                            fac.AntdSpace(
                                [
                                    fac.AntdRadioGroup(
                                        id='key-demo2-type',
                                        options=[
                                            {
                                                'label': f'类型{i}',
                                                'value': f'类型{i}',
                                            }
                                            for i in range(1, 6)
                                        ],
                                        defaultValue='类型1',
                                    ),
                                    fac.AntdSpace(
                                        id='key-demo2-output',
                                        style={
                                            'width': 200,
                                            'height': 100,
                                            'overflowY': 'auto',
                                            'border': '1px solid #dee2e6',
                                        },
                                    ),
                                ],
                                direction='vertical',
                            )
                        ],
                        style={'padding': 25},
                    ),
                    fmc.FefferySyntaxHighlighter(
                        showCopyButton=True,
                        showLineNumbers=True,
                        language='python',
                        codeTheme='coy-without-shadows',
                        codeString="""
html.Div(
    [
        fac.AntdSpace(
            [
                fac.AntdRadioGroup(
                    id='key-demo2-type',
                    options=[
                        {
                            'label': f'类型{i}',
                            'value': f'类型{i}',
                        }
                        for i in range(1, 6)
                    ],
                    defaultValue='类型1'
                ),

                fac.AntdSpace(
                    id='key-demo2-output',
                    style={
                        'width': 200,
                        'height': 100,
                        'overflowY': 'auto',
                        'border': '1px solid #dee2e6'
                    }
                )
            ],
            direction='vertical'
        )
    ],
    style={
        'padding': 25
    }
)

...

import uuid

...

@app.callback(
    [Output('key-demo2-output', 'children'),
     Output('key-demo2-output', 'key')],
    Input('key-demo2-type', 'value')
)
def key_demo2(value):

    return [value * 100, str(uuid.uuid4())]
""",
                    ),
                    html.Div(style={'height': '100px'}),
                ],
                style={'flex': 'auto', 'padding': '25px'},
            )
        ],
        style={'display': 'flex', 'marginRight': 40},
    )


@app.callback(
    Output('key-demo1-output', 'children'), Input('key-demo1-type', 'value')
)
def key_demo1(value):
    return value * 100


@app.callback(
    [Output('key-demo2-output', 'children'), Output('key-demo2-output', 'key')],
    Input('key-demo2-type', 'value'),
)
def key_demo2(value):
    return [value * 100, str(uuid.uuid4())]

```
