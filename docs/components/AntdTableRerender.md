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

## API 参数说明

- id (string; optional):
  Unique id of the component.

- key (string; optional):
  Update the `key` value of the current component to force re-rendering.

- className (string; optional):
  CSS class name of the component.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
  Language for component text. Options: `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German), `'ru-ru'` (Russian).
  Default: `'zh-cn'`.

- containerId (string; optional):
  When the table is rendered in a scrollable container, specify the container id to avoid abnormal behavior of expanded rows when scrolling.

- columns (list of dicts; optional):
  Configure column definitions.

  `columns` is a list of dicts with keys:

  - title (a list of or a singular dash component, string or number; required):
    Required. Current column title.

  - dataIndex (string; required):
    Required. Unique identifier of the column.

  - group (string | list of strings; optional):
    Group information of the column, used for rendering multi-level headers.

  - renderOptions (dict; optional):
    Configure [re-render mode](/AntdTable-rerender) parameters.

    `renderOptions` is a dict with keys:

    - renderType (a value equal to: 'link', 'ellipsis', 'copyable', 'ellipsis-copyable', 'tags', 'status-badge', 'image', 'custom-format', 'corner-mark', 'row-merge', 'dropdown', 'dropdown-links', 'image-avatar', 'mini-line', 'mini-bar', 'mini-progress', 'mini-ring-progress', 'mini-area', 'button', 'checkbox', 'switch', 'select'; optional):
      Re-render type. Options: `'link'`, `'ellipsis'`, `'copyable'`, `'ellipsis-copyable'`, `'tags'`, `'status-badge'`, `'image'`,
      `'custom-format'`, `'corner-mark'`, `'row-merge'`, `'dropdown'`, `'dropdown-links'`, `'image-avatar'`,
      `'mini-line'`, `'mini-bar'`, `'mini-progress'`, `'mini-ring-progress'`, `'mini-area'`,
      `'button'`, `'checkbox'`, `'switch'`, `'select'`.

    - renderLinkText (string; optional):
      When `renderType='link'`, set link text content.

    - renderButtonSplit (boolean; optional):
      When `renderType='button'`, whether to add dividers between multiple buttons.

    - renderButtonPopConfirmProps (dict; optional):
      When `renderType='button'`, configure confirmation popup parameters.

      `renderButtonPopConfirmProps` is a dict with keys:

      - title (string; optional):
        Confirmation popup title.

      - okText (string; optional):
        Confirmation button text.

      - cancelText (string; optional):
        Cancel button text.

    - miniChartColor (string; optional):
      For `renderType='mini-line'`, `'mini-area'`, `'mini-bar'`, set chart color.

    - tooltipCustomContent (string; optional):
      For `renderType='mini-line'`, `'mini-area'`, `'mini-bar'`, JavaScript function string for tooltip content.

    - progressOneHundredPercentColor (string; optional):
      For `renderType='mini-progress'`, `'mini-ring-progress'`, fill color when progress reaches 100%.

    - progressShowPercent (boolean; optional):
      For `renderType='mini-progress'`, whether to show percent text.
      Default: `False`.

    - progressPercentPrecision (number; optional):
      For `renderType='mini-progress'`, number of decimal places for percent text. Default keeps original precision.

    - progressPercentPosition (dict; optional):
      For `renderType='mini-progress'`, position of percent text.

      `progressPercentPosition` is a dict with keys:

      - align (a value equal to: 'start', 'center', 'end'; optional):
        Alignment. Options: `'start'`, `'center'`, `'end'`.

      - type (a value equal to: 'inner', 'outer'; optional):
        Position. Options: `'inner'`, `'outer'`.

    - progressStrokeLinecap (a value equal to: 'square', 'round'; optional):
      For `renderType='mini-progress'`, progress bar cap style. Options: `'square'`, `'round'`.
      Default: `'square'`.

    - progressSize (number; optional):
      For `renderType='mini-progress'`, set pixel size.

    - progressColor (dict; optional):
      For `renderType='mini-progress'`, progress bar color. Supports gradient with keys `'from'`, `'to'`.

      `progressColor` is a string

      Or dict with keys:

  - from (string; optional):
    Gradient start color.

  - to (string; optional):
    Gradient end color.

    - ringProgressFontSize (number; optional):
      For `renderType='mini-ring-progress'`, font size of percent text.

    - dropdownProps (dict; optional):
      For `renderType='dropdown'`, `'dropdown-links'`, configure dropdown menu parameters.

      `dropdownProps` is a dict with keys:

      - title (string; optional):
        Dropdown anchor title.

      - arrow (boolean; optional):
        Whether to show arrow. Default: `False`.

      - disabled (boolean; optional):
        Whether to disable dropdown globally. Lower priority than per-item settings.

      - overlayClassName (string; optional):
        CSS class name of dropdown container.

      - overlayStyle (dict; optional):
        CSS style of dropdown container.

      - placement (a value equal to: 'bottomLeft', 'bottomCenter', 'bottomRight', 'topLeft', 'topCenter', 'topRight'; optional):
        Dropdown placement. Options: `'bottomLeft'`, `'bottomCenter'`, `'bottomRight'`, `'topLeft'`, `'topCenter'`, `'topRight'`.

  - fixed (a value equal to: 'left', 'right' | boolean; optional):
    Column fixed direction. Options: `'left'`, `'right'`. `True` = `'left'`.

  - editable (boolean; optional):
    Whether the column is editable. Default: `False`.

  - editOptions (dict; optional):
    Configure editable input box parameters.

    `editOptions` is a dict with keys:

    - mode (a value equal to: 'default', 'text-area'; optional):
      Input mode. Options: `'default'`, `'text-area'`. Default: `'default'`.

    - autoSize (dict; optional):
      When `mode='textarea'`, configure auto resize. Same as `AntdInput`.
      Default: `False`.

      `autoSize` is a boolean

      Or dict with keys:

  - minRows (number; optional)

  - maxRows (number; optional)

    - maxLength (number; optional):
      Max characters in editable input. Default: unlimited.

    - placeholder (string; optional):
      Placeholder text when empty.

    - disabledKeys (list of strings; optional):
      List of row `key` values to disable input.

  - align (a value equal to: 'left', 'center', 'right'; optional):
    Column alignment. Options: `'left'`, `'center'`, `'right'`. Default: `'center'`.

  - headerAlign (a value equal to: 'left', 'center', 'right'; optional):
    Header alignment. Follows column alignment by default. Options: `'left'`, `'center'`, `'right'`.
    Default: `'center'`.

  - width (number | string; optional):
    Column width.

  - minWidth (number | string; optional):
    Minimum width. Only effective when `tableLayout="auto"`.

  - hidden (boolean; optional):
    Whether to hide the column. Default: `False`.

  - className (string; optional):
    Column CSS class name.

  - defaultSortOrder (a value equal to: 'ascend', 'descend'; optional):
    Default sort order when initializing. Options: `'ascend'`, `'descend'`.

  - filterResetToDefaultFilteredValue (boolean; optional):
    If default filter values are set via `defaultFilteredValues`, whether reset restores them.
    Default: `False`.

- showHeader (boolean; default True):
  Whether to display table header. Default: `True`.

- rowHoverable (boolean; default True):
  Whether rows have hover effect. Default: `True`.

- tableLayout (a value equal to: 'auto', 'fixed'; optional):
  When column widths are not set, control width allocation. Options: `'auto'`, `'fixed'`.

- data (list of dicts; optional):
  Define table data source, corresponding to `columns`.

  `data` is a list of dicts with strings as keys and values of type
  list of boolean | number | string | dict | lists | a list of or a
  singular dash component, string or number | string | number |
  boolean | dict with keys:

  - content (string; optional):
    For `'link'` mode, link text content. Overrides `renderLinkText` in column config.

  - href (string; optional):
    For `'link'` mode, link address.

  - target (string; optional):
    For `'link'` mode, link target. Default: `'_blank'`.

  - disabled (boolean; optional):
    For `'link'` mode, whether the link is disabled. Default: `False`.

    Or list of numbers | dict with keys:

  - color (string; optional):
    For `'tags'` mode, tag color.

  - tag (string | number; optional):
    For `'tags'` mode, tag content. | list of dicts with keys:

  - color (string; optional):
    For `'tags'` mode, tag color.

  - tag (string | number; optional):
    For `'tags'` mode, tag content. | dict with keys:

  - disabled (boolean; optional):
    For `'button'` mode, same as parameter in `AntdButton`.

  - type (a value equal to: 'primary', 'ghost', 'dashed', 'link', 'text', 'default'; optional):
    For `'button'` mode, same as parameter in `AntdButton`.

    - color (a value equal to: 'default', 'primary', 'danger', 'blue', 'purple', 'cyan', 'green', 'magenta', 'pink', 'red', 'orange', 'yellow', 'volcano', 'geekblue', 'lime', 'gold'; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - variant (a value equal to: 'outlined', 'dashed', 'solid', 'filled', 'text', 'link'; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - danger (boolean; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - style (dict; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - content (string; optional):
      For `'button'` mode, button text content.

    - href (string; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - target (string; optional):
      For `'button'` mode, same as parameter in `AntdButton`.

    - popConfirmProps (dict; optional):
      For `'button'` mode, configure confirmation popup parameters for the button (higher priority).

      `popConfirmProps` is a dict with keys:

      - title (string; optional):
        Confirmation popup title.

      - okText (string; optional):
        Confirmation button text.

      - cancelText (string; optional):
        Cancel button text.

    - icon (string; optional):
      For `'button'` mode, button prefix icon type. If `iconRenderer='AntdIcon'`, same as `AntdIcon`; if `iconRenderer='fontawesome'`, CSS class name.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'button'` mode, rendering method for button prefix icon.

    - tooltip (dict; optional):
      For `'button'` mode, add tooltip.

      `tooltip` is a dict with keys:

      - title (string; optional):
        Tooltip text.

      - placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight'; optional):
        Tooltip placement. Default: `'top'`.

    - custom (boolean | number | string | dict | list; optional):
      For `'button'` mode, extra information.

    - status (a value equal to: 'success', 'processing', 'default', 'error', 'warning'; optional):
      For `'status-badge'` mode, badge status.

    - text (string | number; optional):
      For `'status-badge'` mode, badge text.

    - src (string; optional):
      For `'image'` mode, image URL.

    - height (string | number; optional):
      For `'image'` mode, image height.

    - preview (boolean; optional):
      For `'image'` mode, whether image is previewable. Default: `True`.

    - placement (a value equal to: 'top-left', 'top-right', 'bottom-left', 'bottom-right'; optional):
      For `'corner-mark'` mode, badge position.

    - color (string; optional):
      For `'corner-mark'` mode, badge color. Default: `'#1890ff'`.

    - content (number | string; optional):
      For `'corner-mark'` mode, cell value.

    - offsetX (number; optional):
      For `'corner-mark'` mode, horizontal offset.

    - offsetY (number; optional):
      For `'corner-mark'` mode, vertical offset.

    - hide (boolean; optional):
      For `'corner-mark'` mode, whether to hide. Default: `False`.

    - checked (boolean; optional):
      For `'checkbox'` mode, checked status.

    - disabled (boolean; optional):
      For `'checkbox'` mode, disabled state.

    - label (string; optional):
      For `'checkbox'` mode, label text.

    - custom (boolean | number | string | dict | list; optional):
      For `'checkbox'` mode, extra information.

    - checked (boolean; optional):
      For `'switch'` mode, switch state.

    - disabled (boolean; optional):
      For `'switch'` mode, disabled state.

    - checkedChildren (string; optional):
      For `'switch'` mode, text when on.

    - unCheckedChildren (string; optional):
      For `'switch'` mode, text when off.

    - custom (boolean | number | string | dict | list; optional):
      For `'switch'` mode, extra information.

    - content (number | string; optional):
      For `'row-merge'` mode, cell value.

    - rowSpan (number; optional):
      For `'row-merge'` mode, number of merged cells.

    - title (string; optional):
      For `'dropdown'` mode, dropdown item text.

    - disabled (boolean; optional):
      For `'dropdown'` mode, whether dropdown item is disabled.

    - icon (string; optional):
      For `'dropdown'` mode, button prefix icon type.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'dropdown'` mode, icon rendering method.

    - custom (boolean | number | string | dict | list; optional):
      For `'dropdown'` mode, extra information.

    - isDivider (boolean; optional):
      For `'dropdown'` mode, whether item is divider. Default: `False`.

    - title (string; optional):
      For `'dropdown-links'` mode, dropdown item text.

    - href (string; optional):
      For `'dropdown-links'` mode, link URL.

    - disabled (boolean; optional):
      For `'dropdown-links'` mode, disabled.

    - icon (string; optional):
      For `'dropdown-links'` mode, icon type.

    - iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; optional):
      For `'dropdown-links'` mode, icon rendering method.

    - isDivider (boolean; optional):
      For `'dropdown-links'` mode, whether divider. Default: `False`.

    - src (string; optional):
      For `'image-avatar'` mode, avatar image URL.

    - size (dict; optional):
      For `'image-avatar'` mode, avatar size. Number = px, string = preset size (`'small'`, `'default'`, `'large'`). Supports responsive. Default: `'default'`.

      `size` is a number | 'large' | 'small' | 'default' | dict with keys: xs, sm, md, lg, xl, xxl.

    - shape (a value equal to: 'circle', 'square'; optional):
      For `'image-avatar'` mode, avatar shape. Default: `'circle'`.

    - className (string; optional):
      For `'select'` mode, CSS class name.

    - style (dict; optional):
      For `'select'` mode, CSS style. Default width: `'100%'`.

    - options (list of dicts; optional):
      For `'select'` mode, dropdown options.

      `options` is a list of dicts with keys:

      - label (string; optional):
        Option text.

      - value (string | number; optional):
        Option value.

    - listHeight (number; optional):
      For `'select'` mode, dropdown menu height. Default: `256`.

    - mode (a value equal to: 'multiple', 'tags'; optional):
      For `'select'` mode, selection mode. Default: single.

    - disabled (boolean; optional):
      For `'select'` mode, disabled state.

    - size (a value equal to: 'small', 'middle', 'large'; optional):
      For `'select'` mode, size. Default: `'middle'`.

    - bordered (boolean; optional):
      For `'select'` mode, whether bordered. Default: `True`.

    - placeholder (string; optional):
      For `'select'` mode, placeholder text.

    - placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; optional):
      For `'select'` mode, dropdown placement. Default: `'bottomLeft'`.

    - value (string | number | list of string | numbers; optional):
      For `'select'` mode, selected value(s).

    - maxTagCount (number | 'responsive'; optional):
      For `'select'` mode, max number of tags shown. Default: `5`.

    - optionFilterProp (a value equal to: 'value', 'label'; optional):
      For `'select'` mode, search target field. Default: `'value'`.

    - allowClear (boolean; optional):
      For `'select'` mode, allow clearing. Default: `True`.

- bordered (boolean; default False):
  Whether to render table borders. Default: `False`.

- maxHeight (number | string; optional):
  Maximum table height in pixels. When actual height exceeds this, a vertical scrollbar is rendered.

- maxWidth (number | string | boolean; optional):
  Maximum table width. When actual width exceeds this, a horizontal scrollbar is rendered.

- scrollToFirstRowOnChange (boolean; default True):
  After pagination, sorting, or filtering triggers table change, whether to scroll to the top. Default: `True`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
  Table cell size. Options: `'small'`, `'middle'`, `'large'`.

- rowSelectionType (a value equal to: 'checkbox', 'radio'; optional):
  Row selection mode. Options: `'checkbox'` (multi-select), `'radio'` (single-select). Default: disabled.

- selectedRowKeys (list of string | numbers; optional):
  Track selected row `key` values.

- selectedRows (list; optional):
  Track selected row records.

- rowSelectionWidth (string | number; default 32):
  Width of row selection column. Default: `32`.

- rowSelectionCheckStrictly (boolean; optional):
  For nested rows, whether selection of parent and child rows are independent. Default: `True`.

- rowSelectionIgnoreRowKeys (list of string | numbers; optional):
  Specify row `key` values that cannot be selected.

- selectedRowsSyncWithData (boolean; default False):
  When data source `data` updates, whether to sync `selectedRows` based on current `selectedRowKeys`.
  Default: `False`.

- sticky (dict; default False):
  Configure sticky header. Default: `False`.

  `sticky` is a boolean | dict with keys:

  - offsetHeader (number; optional):
    Vertical offset for sticky header.

  - offsetScroll (number; optional):
    Vertical offset for bottom scrollbar in sticky header.

- enableHoverListen (boolean; default False):
  Enable row mouse enter/leave event listening. May affect other features. Default: `False`.

- recentlyMouseEnterColumnDataIndex (string; optional):
  When `enableHoverListen=True`, track `dataIndex` of most recently hovered column.

- recentlyMouseEnterRowKey (string | number; optional):
  When `enableHoverListen=True`, track `key` of most recently hovered row.

- recentlyMouseEnterRow (dict; optional):
  When `enableHoverListen=True`, track record of most recently hovered row.

- titlePopoverInfo (dict; optional):
  Configure extra popover info for column titles.

  `titlePopoverInfo` is a dict with strings as keys and values of type dict with keys:

  - title (string; optional):
    Popover title.

  - content (string; optional):
    Popover content.

  - placement (a value equal to: 'top', 'left', 'right', 'bottom', 'topLeft', 'topRight', 'bottomLeft', 'bottomRight', 'leftTop', 'leftBottom', 'rightTop', 'rightBottom'; optional):
    Popover placement. Options: `'top'`, `'left'`, `'right'`, `'bottom'`, `'topLeft'`, `'topRight'`, `'bottomLeft'`, `'bottomRight'`, `'leftTop'`, `'leftBottom'`, `'rightTop'`, `'rightBottom'`.
    Default: `'bottom'`.

  - overlayStyle (dict; optional):
    CSS style for popover overlay.

- columnsFormatConstraint (dict; optional):
  For editable fields, configure regex-based input validation rules.

  `columnsFormatConstraint` is a dict with strings as keys and values of type dict with keys:

  - rule (string; optional):
    Regular expression to validate input format.

  - content (string; optional):
    Message shown when validation fails.

- sortOptions (dict; optional):
  Configure sorting features.

  `sortOptions` is a dict with keys:

  - sortDataIndexes (list of strings; optional):
    Columns (`dataIndex`) involved in sorting. Order of array defines priority (high to low).

  - multiple (boolean | 'auto'; optional):
    Enable multi-column sorting. `'auto'` = auto multi-sort based on click order.
    Default: `False`.

  - forceCompareModes (dict with strings as keys and values of type 'number' | 'custom'; optional):
    Force sorting mode per column. Options: `'number'` (numeric), `'custom'` (custom).

  - customOrders (dict with strings as keys and values of type list; optional):
    When `forceCompareModes='custom'`, define custom sort order for column values.

- showSorterTooltip (boolean; default True):
  For sortable columns, whether to show tooltip on hover. Default: `True`.

- showSorterTooltipTarget (a value equal to: 'full-header', 'sorter-icon'; default 'full-header'):
  Tooltip hover target. Options: `'full-header'`, `'sorter-icon'`.
  Default: `'full-header'`.

- filterOptions (dict; optional):
  Configure filtering features.

  `filterOptions` is a dict with strings as keys and values of type dict with keys:

  - filterMode (a value equal to: 'checkbox', 'keyword', 'tree'; optional):
    Filter mode. Options: `'checkbox'`, `'keyword'`, `'tree'`. `'tree'` mode requires `filterCustomTreeItems`.
    Default: `'checkbox'`.

  - filterCustomItems (list | boolean | number | string | dict | list; optional):
    For `'checkbox'` mode, define custom filter items.

  - filterCustomTreeItems (list of dicts; optional):
    For `'tree'` mode, define custom tree structure.

  - filterMultiple (boolean; optional):
    For `'checkbox'` mode, whether multi-select is enabled. Default: `True`.

  - filterSearch (boolean; optional):
    For `'checkbox'` mode, whether search box is enabled. Default: `False`.

- defaultFilteredValues (dict with strings as keys and values of type list; optional):
  Default filter values for fields.

- pagination (dict; optional):
  Configure pagination. Set `False` to disable.

  `pagination` is a dict with keys:

  - position (a value equal to: 'topLeft', 'topCenter', 'topRight', 'bottomLeft', 'bottomCenter', 'bottomRight'; optional):
    Pagination component placement. Default: `'bottomRight'`.

  - pageSize (number; optional):
    Track or set max rows per page.

  - current (number; optional):
    Track or set current page number.

  - showSizeChanger (boolean; optional):
    Show pageSize switcher. Default: `True` if total rows > 50.

  - pageSizeOptions (list of numbers; optional):
    Options for pageSize switcher.

  - showTitle (boolean; optional):
    Whether to show native browser tooltip on page number hover. Default: `True`.

  - showQuickJumper (boolean; optional):
    Whether to render quick jump control. Default: `False`.

  - showTotalPrefix (string; optional):
    Prefix text for total records description.

  - showTotalSuffix (string; optional):
    Suffix text for total records description.

  - hideOnSinglePage (boolean; optional):
    Hide pagination if rows < one page. Default: `False`.

  - simple (boolean; optional):
    Enable simple mode. Default: `False`.

  - disabled (boolean; optional):
    Disable pagination controls. Default: `False`.

  - size (a value equal to: 'default', 'small'; optional):
    Pagination control size. Default: `'default'`.

  - total (number; optional):
    Manually set total rows, usually with [server-side mode](/AntdTable-server-side-mode).

  - showLessItems (boolean; optional):
    Prefer fewer jump items. Default: `False`.

- currentData (list; optional):
  Track table data after edits.

- recentlyChangedRow (dict; optional):
  Track row most recently edited.

- recentlyChangedColumn (string; optional):
  Track `dataIndex` of most recently edited column.

- sorter (dict; optional):
  Track sort behavior.

  `sorter` is a dict with keys:

  - columns (list of strings; optional):
    Track sorted columns (`dataIndex`).

  - orders (list of a value equal to: 'ascend', 'descend'; optional):
    Track sort order. `'ascend'` = ascending, `'descend'` = descending.

- filter (dict; optional):
  Track filter behavior.

- mode (a value equal to: 'client-side', 'server-side'; default 'client-side'):
  Data load mode. Options: `'client-side'` (client), `'server-side'` (server). Server mode fits large datasets. Default: `'client-side'`.

- summaryRowContents (list of dicts; optional):
  Configure summary row contents.

  `summaryRowContents` is a list of dicts with keys:

  - content (a list of or a singular dash component, string or number; optional):
    Component, summary cell content.

  - colSpan (number; optional):
    Number of columns spanned by cell. Default: `1`.

  - align (a value equal to: 'left', 'center', 'right'; optional):
    Column alignment. Options: `'left'`, `'center'`, `'right'`.

- summaryRowBlankColumns (number; default 0):
  Number of blank columns per summary row. For use with row selection, etc. Default: `0`.

- summaryRowFixed (boolean | a value equal to: 'top', 'bottom'; default False):
  Whether to fix summary row. Options: `'top'`, `'bottom'`. Default: `False`.

- conditionalStyleFuncs (dict with strings as keys and values of type string; optional):
  Configure conditional formatting JavaScript functions per column.

- expandedRowKeyToContent (list of dicts; optional):
  Configure expanded row content. Key = row `key`, value = expanded content.

  `expandedRowKeyToContent` is a list of dicts with keys:

  - key (string | number; required)

  - content (a list of or a singular dash component, string or number; optional)

- expandedRowWidth (string | number; optional):
  Width of expanded row control column.

- expandRowByClick (boolean; default False):
  Allow expanding row by clicking directly. Default: `False`.

- defaultExpandedRowKeys (list of strings; optional):
  Keys of rows expanded by default.

- expandedRowKeys (list of strings; optional):
  Track or set expanded row keys.

- enableCellClickListenColumns (list of strings; optional):
  Enable cell click/double-click/right-click event listening. Default: `False`.

- recentlyCellClickColumn (string; optional):
  When enabled, track `dataIndex` of most recent cell click.

- recentlyCellClickRecord (dict; optional):
  When enabled, track record of most recent cell click.

- nClicksCell (number; default 0):
  When enabled, track cumulative number of cell clicks. Default: `0`.

- cellClickEvent (dict; optional):
  When enabled, track details of most recent cell click.

  `cellClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page top-left.

  - pageY (number; optional):
    Y coordinate relative to page top-left.

  - clientX (number; optional):
    X coordinate relative to browser window.

  - clientY (number; optional):
    Y coordinate relative to browser window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- recentlyCellDoubleClickColumn (string; optional):
  Track `dataIndex` of most recent cell double-click.

- recentlyCellDoubleClickRecord (dict; optional):
  Track record of most recent cell double-click.

- nDoubleClicksCell (number; default 0):
  Track cumulative cell double-clicks. Default: `0`.

- cellDoubleClickEvent (dict; optional):
  Track details of most recent cell double-click.

  `cellDoubleClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page.

  - pageY (number; optional):
    Y coordinate relative to page.

  - clientX (number; optional):
    X coordinate relative to window.

  - clientY (number; optional):
    Y coordinate relative to window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- recentlyContextMenuClickColumn (string; optional):
  Track `dataIndex` of most recent cell right-click.

- recentlyContextMenuClickRecord (dict; optional):
  Track record of most recent cell right-click.

- nContextMenuClicksCell (number; default 0):
  Track cumulative cell right-clicks. Default: `0`.

- cellContextMenuClickEvent (dict; optional):
  Track details of most recent cell right-click.

  `cellContextMenuClickEvent` is a dict with keys:

  - pageX (number; optional):
    X coordinate relative to page.

  - pageY (number; optional):
    Y coordinate relative to page.

  - clientX (number; optional):
    X coordinate relative to window.

  - clientY (number; optional):
    Y coordinate relative to window.

  - screenX (number; optional):
    X coordinate relative to screen.

  - screenY (number; optional):
    Y coordinate relative to screen.

  - timestamp (number; optional):
    Event timestamp.

- emptyContent (a list of or a singular dash component, string or number; optional):
  Component for custom empty-state content.

- cellUpdateOptimize (boolean; default False):
  Strictly optimize cell rendering based on data. Default: `False`.

- miniChartHeight (number; default 30):
  Set height for mini-chart cells. Default: `30`.

- miniChartAnimation (boolean; default False):
  Enable animation for mini-chart cells. Default: `False`.

- recentlyButtonClickedRow (dict; optional):
  For `'button'` mode, track row of most recent button click.

- nClicksButton (number; default 0):
  For `'button'` mode, track cumulative button clicks. Default: `0`.

- clickedContent (string; optional):
  For `'button'` mode, track text of most recent button click.

- clickedCustom (boolean | number | string | dict | list; optional):
  For `'button'` mode, track `custom` field of most recent button click.

- recentlyButtonClickedDataIndex (string; optional):
  For `'button'` mode, track `dataIndex` of most recent button click.

- customFormatFuncs (dict with strings as keys and values of type string; optional):
  For `'custom-format'` mode, key = `dataIndex`, value = JavaScript pre-processing function.

- recentlyCheckedRow (dict; optional):
  For `'checkbox'` mode, track row of most recent check.

- recentlyCheckedLabel (string; optional):
  For `'checkbox'` mode, track label of most recent check.

- recentlyCheckedDataIndex (string; optional):
  For `'checkbox'` mode, track `dataIndex` of most recent check.

- recentlyCheckedStatus (boolean; optional):
  For `'checkbox'` mode, track status of most recent check.

- recentlySwitchRow (dict; optional):
  For `'switch'` mode, track row of most recent toggle.

- recentlySwitchDataIndex (string; optional):
  For `'switch'` mode, track `dataIndex` of most recent toggle.

- recentlySwitchStatus (boolean; optional):
  For `'switch'` mode, track status of most recent toggle.

- nClicksDropdownItem (number; default 0):
  For `'dropdown'` mode, track cumulative dropdown item clicks.

- recentlyClickedDropdownItemTitle (string; optional):
  For `'dropdown'` mode, track `title` of most recent item clicked.

- recentlyDropdownItemClickedDataIndex (string; optional):
  For `'dropdown'` mode, track `dataIndex` of most recent item clicked.

- recentlyDropdownItemClickedRow (dict; optional):
  For `'dropdown'` mode, track row of most recent item clicked.

- recentlySelectRow (dict; optional):
  For `'select'` mode, track row of most recent value update.

- recentlySelectDataIndex (string; optional):
  For `'select'` mode, track `dataIndex` of most recent value update.

- recentlySelectValue (number | string | list of number | strings; optional):
  For `'select'` mode, track value(s) of most recent update.

- hiddenRowKeys (list of strings; optional):
  Row `key` values to hide. Default: `[]`.

- dataDeepCompare (boolean; optional):
  On re-render, whether to deep compare `data` for optimization. Default: `False`.

- virtual (boolean; default False):
  Enable virtual scrolling. Default: `False`.

- title (a list of or a singular dash component, string or number; optional):
  Component for table title.

- footer (a list of or a singular dash component, string or number; optional):
  Component for table footer.

- loading (boolean; default False):
  Whether to show loading state. Default: `False`.

- rowClassName (dict; optional):
  CSS class for rows. Supports defining JavaScript function via `func`.

  `rowClassName` is a string | dict with keys:

  - func (string; optional):
    JavaScript function string.

- data-_ (string; optional):
  Wildcard for `data-_` attributes.

- aria-\* (string; optional):
