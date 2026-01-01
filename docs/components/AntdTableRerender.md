# AntdTableRerender

## 简介源码：`views/AntdTableRerender/intro.py`
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
                {'title': translator.t('再渲染模式')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdTable 表格'), level=2),
        fac.AntdParagraph(translator.t('表格组件中使用不同的再渲染模式。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### button按钮模式及回调监听

- 说明：将单元格内容快捷渲染为按钮形式，并通过回调监听相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-rerender-button-demo',
        columns=[
            {
                'title': 'button示例1',
                'dataIndex': 'button示例1',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'button示例2',
                'dataIndex': 'button示例2',
                'renderOptions': {'renderType': 'button'},
            },
            {
                'title': 'button示例3',
                'dataIndex': 'button示例3',
                'renderOptions': {
                    'renderType': 'button',
                    'renderButtonPopConfirmProps': {
                        'title': '确认执行？',
                        'okText': '确认',
                        'cancelText': '取消',
                    },
                },
            },
        ],
        data=[
            {
                'button示例1': {
                    'content': f'按钮1-{i}',
                    'type': 'link',
                    'custom': 'balabalabalabala',
                },
                'button示例2': [
                    {
                        'content': f'按钮2-{i}-{j}',
                        'type': 'primary',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
                'button示例3': [
                    {
                        'content': f'按钮3-{i}-{j}',
                        'type': 'dashed',
                        'danger': True,
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 3)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
    ),
    html.Pre(id='table-rerender-button-demo-output'),
]

...

@app.callback(
    Output('table-rerender-button-demo-output', 'children'),
    Input('table-rerender-button-demo', 'nClicksButton'),
    [
        State('table-rerender-button-demo', 'clickedContent'),
        State('table-rerender-button-demo', 'clickedCustom'),
        State('table-rerender-button-demo', 'recentlyButtonClickedDataIndex'),
        State('table-rerender-button-demo', 'recentlyButtonClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_button_demo(
    nClicksButton,
    clickedContent,
    clickedCustom,
    recentlyButtonClickedDataIndex,
    recentlyButtonClickedRow,
):
    return json.dumps(
        dict(
            nClicksButton=nClicksButton,
            clickedContent=clickedContent,
            clickedCustom=clickedCustom,
            recentlyButtonClickedDataIndex=recentlyButtonClickedDataIndex,
            recentlyButtonClickedRow=recentlyButtonClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### 控制按钮形态

- 说明：配合`color`与`variant`参数渲染具有不同颜色和形态的按钮。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'dataIndex': 'variant参数值',
            'title': 'variant参数值',
        },
        {
            'dataIndex': '渲染效果',
            'title': '渲染效果',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            'variant参数值': variant,
            '渲染效果': [
                {'content': color, 'color': color, 'variant': variant}
                for color in [
                    'default',
                    'primary',
                    'danger',
                    'blue',
                    'purple',
                    'cyan',
                    'green',
                    'magenta',
                    'pink',
                    'red',
                    'orange',
                    'yellow',
                    'volcano',
                    'geekblue',
                    'lime',
                    'gold',
                ]
            ],
        }
        for variant in [
            'outlined',
            'dashed',
            'solid',
            'filled',
            'text',
            'link',
        ]
    ],
    bordered=True,
    tableLayout='fixed',
)
```

### 独立控制按钮是否添加气泡确认框

- 说明：同一单元格中的每个按钮都可以单独控制是否添加气泡确认框。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'dataIndex': '按钮示例',
            'title': '按钮示例',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            '按钮示例': [
                {
                    'content': '带气泡确认',
                    'popConfirmProps': {
                        'title': '气泡确认标题',
                        'okText': '确认',
                        'cancelText': '取消',
                    },
                },
                {
                    'content': '不带气泡确认',
                },
            ]
        }
    ],
    bordered=True,
)
```

### 独立控制按钮是否添加文字提示框

- 说明：同一单元格中的每个按钮都可以单独控制是否添加文字提示框。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'dataIndex': '按钮示例',
            'title': '按钮示例',
            'renderOptions': {'renderType': 'button'},
        },
    ],
    data=[
        {
            '按钮示例': [
                {
                    'content': '带tooltip',
                    'tooltip': {'title': 'tooltip示例'},
                },
                {
                    'content': '不带tooltip',
                },
            ]
        }
    ],
    bordered=True,
)
```

### checkbox勾选框模式及回调监听

- 说明：将单元格内容快捷渲染为勾选框形式，并通过回调监听相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-rerender-checkbox-demo',
        columns=[
            {
                'title': 'checkbox示例',
                'dataIndex': 'checkbox示例',
                'renderOptions': {'renderType': 'checkbox'},
            }
        ],
        data=[
            {
                'checkbox示例': {
                    'checked': i % 2 == 0,
                    'label': f'选项{i}',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-checkbox-demo-output'),
]

...

@app.callback(
    Output('table-rerender-checkbox-demo-output', 'children'),
    [
        Input('table-rerender-checkbox-demo', 'recentlyCheckedLabel'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedDataIndex'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedStatus'),
        Input('table-rerender-checkbox-demo', 'recentlyCheckedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_checkbox_demo(
    recentlyCheckedLabel,
    recentlyCheckedDataIndex,
    recentlyCheckedStatus,
    recentlyCheckedRow,
):
    return json.dumps(
        dict(
            recentlyCheckedLabel=recentlyCheckedLabel,
            recentlyCheckedDataIndex=recentlyCheckedDataIndex,
            recentlyCheckedStatus=recentlyCheckedStatus,
            recentlyCheckedRow=recentlyCheckedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### copyable可复制模式

- 说明：将单元格内容快捷渲染为可复制形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'copyable示例',
            'dataIndex': 'copyable示例',
            'renderOptions': {'renderType': 'copyable'},
        }
    ],
    data=[{'copyable示例': '可复制内容'}],
    bordered=True,
    style={'width': 200},
)
```

### corner-mark角标模式

- 说明：将单元格内容快捷渲染为角标形式。

#### 代码
```python
fac.AntdTable(
    size='small',
    columns=[
        {
            'title': '角标模式',
            'dataIndex': '角标模式',
            'renderOptions': {'renderType': 'corner-mark'},
        }
    ],
    data=[
        {
            'key': i,
            '角标模式': {
                'content': '角标模式',
                'color': ['red', 'blue', 'green'][i],
                'offsetX': -7.5,
                'offsetY': -8.5,
                'placement': 'top-left',
                'hide': [False, True, False][i],
            },
        }
        for i in range(3)
    ],
    bordered=True,
    style={'width': '200px'},
)
```

### 自定义单元格元素

- 说明：目前已有的快捷再渲染模式满足不了你的需求？没关系，任何组件元素都可以作为单元格值被传入😉！（此特性建议仅用作静态展示使用）

#### 代码
```python
fac.AntdTable(
    columns=[{'title': '自定义元素示例', 'dataIndex': '自定义元素示例'}],
    data=[
        {
            '自定义元素示例': html.Div(
                fac.AntdText(
                    '示例内容' * 100, style={'textIndent': '2rem'}
                ),
                style={
                    'maxHeight': 50,
                    'overflowY': 'auto',
                    'textAlign': 'left',
                },
            )
        },
        {
            '自定义元素示例': fmc.FefferyMarkdown(
                markdownStr="""
```python
import numpy as np
from dash import html
import feffery_antd_components as fac
import feffery_markdown_components as fmc
```
"""
            )
        },
        {'自定义元素示例': fuc.FefferyQRCode(value='FefferyQRCode示例')},
    ],
    bordered=True,
    style={'width': '100%'},
)
```

### custom-format自定义格式模式

- 说明：在这个例子中，数值测试1与数值测试2字段本质上都是数值型，但在`custom-format`模式下，可通过参数`customFormatFuncs`自定义的js函数来改变单元格中所渲染出的内容格式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': '数值测试1',
            'dataIndex': '数值测试1',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
        {
            'title': '数值测试2',
            'dataIndex': '数值测试2',
            'width': '50%',
            'renderOptions': {'renderType': 'custom-format'},
        },
    ],
    data=[
        {'数值测试1': np.random.rand(), '数值测试2': np.random.rand()}
        for i in range(10)
    ],
    sortOptions={'sortDataIndexes': ['数值测试1', '数值测试2']},
    bordered=True,
    customFormatFuncs={
        '数值测试1': '(x) => `${(x*100).toFixed(2)}%`',
        '数值测试2': '(x) => x <= 0.5 ? `低水平：${x.toFixed(2)}` : `高水平：${x.toFixed(2)}`',
    },
    style={'width': '500px'},
)
```

### dropdown-links下拉链接菜单模式

- 说明：将单元格内容快捷渲染为下拉链接菜单形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'dropdown-links示例1',
            'dataIndex': 'dropdown-links示例1',
            'renderOptions': {'renderType': 'dropdown-links'},
            'width': '30%',
        },
        {
            'title': 'dropdown-links示例2',
            'dataIndex': 'dropdown-links示例2',
            'renderOptions': {
                'renderType': 'dropdown-links',
                'dropdownProps': {'title': '更多'},
            },
            'width': '70%',
        },
    ],
    data=[
        {
            'dropdown-links示例1': [
                {
                    'title': f'image示例{i}.png',
                    'href': f'assets/imgs/image示例{i}.png',
                }
                for i in range(1, 8)
            ],
            'dropdown-links示例2': [
                {
                    'title': f'image示例{i}.png',
                    'href': f'assets/imgs/image示例{i}.png',
                }
                for i in range(1, 8)
            ],
        }
    ]
    * 3,
    bordered=True,
    style={'width': 400},
)
```

### dropdown下拉菜单模式及回调监听

- 说明：将单元格内容快捷渲染为下拉菜单形式，并通过回调监听相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-rerender-dropdown-demo',
        columns=[
            {
                'title': 'dropdown示例1',
                'dataIndex': 'dropdown示例1',
                'renderOptions': {'renderType': 'dropdown'},
            },
            {
                'title': 'dropdown示例2',
                'dataIndex': 'dropdown示例2',
                'renderOptions': {
                    'renderType': 'dropdown',
                    'dropdownProps': {'title': '更多'},
                },
            },
        ],
        data=[
            {
                'dropdown示例1': [
                    {
                        'title': f'示例1-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
                'dropdown示例2': [
                    {
                        'title': f'示例2-{i}-{j}',
                        'custom': 'balabalabalabala',
                    }
                    for j in range(1, 6)
                ],
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-dropdown-demo-output'),
]

...

@app.callback(
    Output('table-rerender-dropdown-demo-output', 'children'),
    Input('table-rerender-dropdown-demo', 'nClicksDropdownItem'),
    [
        State(
            'table-rerender-dropdown-demo', 'recentlyClickedDropdownItemTitle'
        ),
        State(
            'table-rerender-dropdown-demo',
            'recentlyDropdownItemClickedDataIndex',
        ),
        State('table-rerender-dropdown-demo', 'recentlyDropdownItemClickedRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_dropdown_demo(
    nClicksDropdownItem,
    recentlyClickedDropdownItemTitle,
    recentlyDropdownItemClickedDataIndex,
    recentlyDropdownItemClickedRow,
):
    return json.dumps(
        dict(
            nClicksDropdownItem=nClicksDropdownItem,
            recentlyClickedDropdownItemTitle=recentlyClickedDropdownItemTitle,
            recentlyDropdownItemClickedDataIndex=recentlyDropdownItemClickedDataIndex,
            recentlyDropdownItemClickedRow=recentlyDropdownItemClickedRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### ellipsis-copyable长内容省略+可复制模式

- 说明：将单元格内容快捷渲染为长内容省略+可复制形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'ellipsis-copyable示例',
            'dataIndex': 'ellipsis-copyable示例',
            'renderOptions': {'renderType': 'ellipsis-copyable'},
        }
    ],
    data=[{'ellipsis-copyable示例': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
```

### ellipsis长内容省略模式

- 说明：将单元格内容快捷渲染为长内容省略形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'ellipsis示例',
            'dataIndex': 'ellipsis示例',
            'renderOptions': {'renderType': 'ellipsis'},
        }
    ],
    data=[{'ellipsis示例': 'bala' * 10}],
    bordered=True,
    style={'width': 200},
)
```

### image-avatar图片型头像模式

- 说明：将单元格内容快捷渲染为图片型头像形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'image-avatar示例1',
            'dataIndex': 'image-avatar示例1',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
        {
            'title': 'image-avatar示例2',
            'dataIndex': 'image-avatar示例2',
            'renderOptions': {'renderType': 'image-avatar'},
            'width': '50%',
        },
    ],
    data=[
        {
            'image-avatar示例1': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg'
            },
            'image-avatar示例2': {
                'src': 'assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                'shape': 'square',
            },
        }
    ]
    * 3,
    bordered=True,
    style={'width': 300},
)
```

### image图片模式

- 说明：将单元格内容快捷渲染为图片形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': '交互式图片',
            'dataIndex': '交互式图片',
            'renderOptions': {'renderType': 'image'},
        },
        {
            'title': '静态图片',
            'dataIndex': '静态图片',
            'renderOptions': {'renderType': 'image'},
        },
    ],
    data=[
        {
            '交互式图片': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
            },
            '静态图片': {
                'src': '/assets/imgs/fac-logo.svg',
                'height': '75px',
                'preview': False,
            },
        }
        for i in range(5)
    ],
    bordered=True,
    style={'width': '300px'},
)
```

### link链接模式

- 说明：将单元格内容快捷渲染为链接形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'link示例1',
            'dataIndex': 'link示例1',
            'renderOptions': {'renderType': 'link'},
            'width': '50%',
        },
        {
            'title': 'link示例2',
            'dataIndex': 'link示例2',
            'renderOptions': {
                'renderType': 'link',
                'renderLinkText': '示例链接',
            },
            'width': '50%',
        },
    ],
    data=[
        {
            'link示例1': {'content': f'{content}仓库', 'href': href},
            'link示例2': {'href': '/AntdTable-rerender'},
        }
        for href, content in zip(
            [
                'https://github.com/CNFeffery/feffery-antd-components',
                'https://github.com/CNFeffery/feffery-utils-components',
                'https://github.com/CNFeffery/feffery-antd-charts',
                'https://github.com/CNFeffery/feffery-markdown-components',
                'https://github.com/CNFeffery/feffery-leaflet-components',
            ],
            ['fac', 'fuc', 'fact', 'fmc', 'flc'],
        )
    ],
    bordered=True,
    style={'width': 400},
)
```

### mini-area迷你面积图模式

- 说明：将单元格内容快捷渲染为迷你面积图形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-area示例1',
            'dataIndex': 'mini-area示例1',
            'renderOptions': {'renderType': 'mini-area'},
        },
        {
            'title': 'mini-area示例2',
            'dataIndex': 'mini-area示例2',
            'renderOptions': {
                'renderType': 'mini-area',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-area',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-area示例1': [np.random.rand() for i in range(25)],
            'mini-area示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
```

### mini-bar迷你柱状图模式

- 说明：将单元格内容快捷渲染为迷你柱状图形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-bar示例1',
            'dataIndex': 'mini-bar示例1',
            'renderOptions': {'renderType': 'mini-bar'},
        },
        {
            'title': 'mini-bar示例2',
            'dataIndex': 'mini-bar示例2',
            'renderOptions': {
                'renderType': 'mini-bar',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-bar',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-bar示例1': [np.random.rand() for i in range(25)],
            'mini-bar示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
```

### mini-line迷你折线图模式

- 说明：将单元格内容快捷渲染为迷你折线图形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-line示例1',
            'dataIndex': 'mini-line示例1',
            'renderOptions': {'renderType': 'mini-line'},
        },
        {
            'title': 'mini-line示例2',
            'dataIndex': 'mini-line示例2',
            'renderOptions': {
                'renderType': 'mini-line',
                'tooltipCustomContent': """(x, data) => `数值：${data[0]?.data?.y.toFixed(3)}`""",
            },
        },
        {
            'title': '自定义颜色示例',
            'dataIndex': '自定义颜色示例',
            'renderOptions': {
                'renderType': 'mini-line',
                'miniChartColor': '#ff7875',
            },
        },
    ],
    data=[
        {
            'mini-line示例1': [np.random.rand() for i in range(25)],
            'mini-line示例2': [np.random.rand() for i in range(25)],
            '自定义颜色示例': [np.random.rand() for i in range(25)],
        }
    ]
    * 3,
    bordered=True,
    tableLayout='fixed',
    style={'width': 400},
)
```

### 控制进度条颜色

- 说明：基于配置项`progressColor`控制进度条颜色，支持渐变色。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': '#f08c00',
            },
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressColor': {
                    'from': '#4c83ff',
                    'to': '#2afadf',
                },
            },
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
```

### 迷你进度图模式基础使用

- 说明：将单元格内容快捷渲染为迷你进度图形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {'renderType': 'mini-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressOneHundredPercentColor': '#f08c00',
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    style={'width': 300},
)
```

### 调整进度数值位置

- 说明：基于配置项`progressPercentPosition`调整进度数值位置。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                'align:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-align',
                    options=['start', 'center', 'end'],
                    value='end',
                ),
            ]
        ),
        fac.AntdSpace(
            [
                'type:',
                fac.AntdRadioGroup(
                    id='table-mini-progress-percent-position-demo-type',
                    options=['inner', 'outer'],
                    value='inner',
                ),
            ]
        ),
        fac.AntdTable(
            id='table-mini-progress-percent-position-demo',
            columns=[
                {
                    'dataIndex': 'mini-progress示例',
                    'title': 'mini-progress示例',
                    'renderOptions': {
                        'renderType': 'mini-progress',
                        'progressShowPercent': True,
                        'progressPercentPosition': {
                            'align': 'end',
                            'type': 'inner',
                        },
                    },
                },
            ],
            data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
            bordered=True,
        ),
    ],
    direction='vertical',
    size='small',
    style={'width': '100%'},
)

...

app.clientside_callback(
    """
(align, type) => {
    return [
        {
            'dataIndex': 'mini-progress示例',
            'title': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': true,
                'progressPercentPosition': {
                    'align': align,
                    'type': type,
                },
            },
        },
    ];
}
""",
    Output('table-mini-progress-percent-position-demo', 'columns'),
    [
        Input('table-mini-progress-percent-position-demo-align', 'value'),
        Input('table-mini-progress-percent-position-demo-type', 'value'),
    ],
    prevent_initial_call=True,
)
```

### 控制进度数值小数位数

- 说明：基于配置项`progressPercentPrecision`控制进度数值小数位数。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressPercentPrecision': 1,
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.5678, 0.6789, 1]],
    bordered=True,
)
```

### 圆角矩形风格

- 说明：基于配置项`progressStrokeLinecap`控制进度条风格。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressStrokeLinecap': 'round',
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
    bordered=True,
)
```

### 显示进度数值

- 说明：基于配置项`progressShowPercent`控制是否显示进度数值。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例',
            'dataIndex': 'mini-progress示例',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
            },
        }
    ],
    data=[{'mini-progress示例': x} for x in [0, 0.66, 1]],
    bordered=True,
)
```

### 控制进度条尺寸

- 说明：基于配置项`progressSize`控制进度条像素尺寸。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-progress示例1',
            'dataIndex': 'mini-progress示例1',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressSize': 24,
            },
        },
        {
            'title': 'mini-progress示例2',
            'dataIndex': 'mini-progress示例2',
            'renderOptions': {
                'renderType': 'mini-progress',
                'progressShowPercent': True,
                'progressStrokeLinecap': 'round',
                'progressSize': 24,
            },
        },
    ],
    data=[
        {'mini-progress示例1': x, 'mini-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    tableLayout='fixed',
)
```

### mini-ring-progress迷你环形进度图模式

- 说明：将单元格内容快捷渲染为迷你环形进度图形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'mini-ring-progress示例1',
            'dataIndex': 'mini-ring-progress示例1',
            'renderOptions': {'renderType': 'mini-ring-progress'},
            'width': '50%',
        },
        {
            'title': 'mini-ring-progress示例2',
            'dataIndex': 'mini-ring-progress示例2',
            'renderOptions': {
                'renderType': 'mini-ring-progress',
                'progressOneHundredPercentColor': '#f08c00',
                'ringProgressFontSize': 8,
            },
            'width': '50%',
        },
    ],
    data=[
        {'mini-ring-progress示例1': x, 'mini-ring-progress示例2': x}
        for x in [0, 0.66, 1]
    ],
    bordered=True,
    miniChartHeight=75,
    style={'width': 300},
)
```

### row-merge跨行单元格合并模式

- 说明：将单元格内容快捷渲染为跨行单元格合并形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'row-merge示例1',
            'dataIndex': 'row-merge示例1',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
        {
            'title': 'row-merge示例2',
            'dataIndex': 'row-merge示例2',
            'renderOptions': {'renderType': 'row-merge'},
            'width': '50%',
        },
    ],
    data=[
        {
            'row-merge示例1': {'content': '示例1-1', 'rowSpan': 1},
            'row-merge示例2': {'content': '示例2-1', 'rowSpan': 2},
        },
        {
            'row-merge示例1': {'content': '示例1-2', 'rowSpan': 2},
            'row-merge示例2': {'rowSpan': 0},
        },
        {
            'row-merge示例1': {'rowSpan': 0},
            'row-merge示例2': {'content': '示例2-2', 'rowSpan': 1},
        },
    ],
    bordered=True,
    style={'width': 300},
)
```

### select下拉选择模式及回调监听

- 说明：将单元格内容快捷渲染为下拉选择形式，并通过回调监听相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-rerender-select-demo',
        columns=[
            {
                'title': 'select示例1',
                'dataIndex': 'select示例1',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select示例2',
                'dataIndex': 'select示例2',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
            {
                'title': 'select示例3',
                'dataIndex': 'select示例3',
                'renderOptions': {'renderType': 'select'},
                'width': 'calc(100% / 3)',
            },
        ],
        data=[
            {
                'select示例1': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'allowClear': True,
                    'placeholder': '请选择',
                },
                'select示例2': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'mode': 'multiple',
                    'allowClear': True,
                    'placeholder': '请选择',
                },
                'select示例3': {
                    'options': [
                        {'label': f'选项{j}', 'value': f'选项{j}'}
                        for j in range(5)
                    ],
                    'mode': 'tags',
                    'allowClear': True,
                    'placeholder': '请选择',
                },
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 600},
    ),
    html.Pre(id='table-rerender-select-demo-output'),
]

...

@app.callback(
    Output('table-rerender-select-demo-output', 'children'),
    [
        Input('table-rerender-select-demo', 'recentlySelectRow'),
        Input('table-rerender-select-demo', 'recentlySelectDataIndex'),
        Input('table-rerender-select-demo', 'recentlySelectValue'),
    ],
    prevent_initial_call=True,
)
def table_rerender_select_demo(
    recentlySelectRow, recentlySelectDataIndex, recentlySelectValue
):
    return json.dumps(
        dict(
            recentlySelectRow=recentlySelectRow,
            recentlySelectDataIndex=recentlySelectDataIndex,
            recentlySelectValue=recentlySelectValue,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### status-badge状态徽标模式

- 说明：将单元格内容快捷渲染为状态徽标形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': '状态徽标示例',
            'dataIndex': '状态徽标示例',
            'renderOptions': {'renderType': 'status-badge'},
        }
    ],
    data=[
        {
            'key': i,
            '状态徽标示例': {'status': status, 'text': status + '状态示例'},
        }
        for i, status in enumerate(
            ['success', 'processing', 'default', 'error', 'warning']
        )
    ],
    style={'width': '250px'},
)
```

### switch开关模式及回调监听

- 说明：将单元格内容快捷渲染为开关形式，并通过回调监听相关事件。

#### 代码
```python
[
    fac.AntdTable(
        id='table-rerender-switch-demo',
        columns=[
            {
                'title': 'switch示例',
                'dataIndex': 'switch示例',
                'renderOptions': {'renderType': 'switch'},
            }
        ],
        data=[
            {
                'switch示例': {
                    'checked': i % 2 == 0,
                    'checkedChildren': '开',
                    'unCheckedChildren': '关',
                    'custom': 'balabalabalabala',
                }
            }
            for i in range(1, 4)
        ],
        bordered=True,
        style={'width': 200},
    ),
    html.Pre(id='table-rerender-switch-demo-output'),
]

...

@app.callback(
    Output('table-rerender-switch-demo-output', 'children'),
    [
        Input('table-rerender-switch-demo', 'recentlySwitchDataIndex'),
        Input('table-rerender-switch-demo', 'recentlySwitchStatus'),
        Input('table-rerender-switch-demo', 'recentlySwitchRow'),
    ],
    prevent_initial_call=True,
)
def table_rerender_switch_demo(
    recentlySwitchDataIndex, recentlySwitchStatus, recentlySwitchRow
):
    return json.dumps(
        dict(
            recentlySwitchDataIndex=recentlySwitchDataIndex,
            recentlySwitchStatus=recentlySwitchStatus,
            recentlySwitchRow=recentlySwitchRow,
        ),
        indent=4,
        ensure_ascii=False,
    )
```

### tags标签模式

- 说明：将单元格内容快捷渲染为标签形式。

#### 代码
```python
fac.AntdTable(
    columns=[
        {
            'title': 'tags示例1',
            'dataIndex': 'tags示例1',
            'renderOptions': {'renderType': 'tags'},
        },
        {
            'title': 'tags示例2',
            'dataIndex': 'tags示例2',
            'renderOptions': {'renderType': 'tags'},
        },
    ],
    data=[
        {
            'tags示例1': {'tag': f'标签{i}', 'color': 'cyan'},
            'tags示例2': [
                {'tag': f'标签{i}-{j}', 'color': color}
                for j, color in zip(
                    range(1, 4), ['volcano', 'blue', 'geekblue']
                )
            ],
        }
        for i in range(1, 4)
    ],
    bordered=True,
    style={'width': 400},
)
```
