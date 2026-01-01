# AntdCheckableTag

## 简介源码：`views/AntdCheckableTag/intro.py`
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
                {'title': 'AntdCheckableTag 可选择标签'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCheckableTag 可选择标签', level=2),
        fac.AntdParagraph('可以点击切换选中状态的标签。'),
    ]

```

## 示例源码（demos）

### `views/AntdCheckableTag/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, ALL
from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdDivider('单标签回调', innerTextOrientation='left'),
            fac.AntdCheckableTag(
                content='单标签', id='checkable-tag-single-demo'
            ),
            fac.AntdCard(
                id='checkable-tag-single-demo-output',
                styles={'header': {'display': 'none'}},
            ),
            fac.AntdDivider('多标签回调', innerTextOrientation='left'),
            fac.AntdSpace(
                [
                    fac.AntdCheckableTag(
                        id={'type': 'checkable-tag-demo', 'index': i},
                        content=f'标签{i}',
                    )
                    for i in range(1, 6)
                ]
            ),
            fac.AntdCard(
                id='checkable-tag-output-demo',
                styles={'header': {'display': 'none'}},
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
    )

    return demo_contents


# 单标签回调
@app.callback(
    Output('checkable-tag-single-demo-output', 'children'),
    Input('checkable-tag-single-demo', 'checked'),
)
def checkable_tag_single_demo(checked):
    return f'checked: {checked}'


# 多标签回调
@app.callback(
    Output('checkable-tag-output-demo', 'children'),
    Input({'type': 'checkable-tag-demo', 'index': ALL}, 'checked'),
)
def checkable_tag_demo(checked_list):
    return f'checked_list: {checked_list}'


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdDivider('单标签回调', innerTextOrientation='left'),
        fac.AntdCheckableTag(
            content='单标签', id='checkable-tag-single-demo'
        ),
        fac.AntdCard(
            id='checkable-tag-single-demo-output',
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider('多标签回调', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdCheckableTag(
                    id={'type': 'checkable-tag-demo', 'index': i},
                    content=f'标签{i}',
                )
                for i in range(1, 6)
            ]
        ),
        fac.AntdCard(
            id='checkable-tag-output-demo',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)


# 单标签回调
@app.callback(
    Output('checkable-tag-single-demo-output', 'children'),
    Input('checkable-tag-single-demo', 'checked'),
)
def checkable_tag_single_demo(checked):
    return f'checked: {checked}'


# 多标签回调
@app.callback(
    Output('checkable-tag-output-demo', 'children'),
    Input({'type': 'checkable-tag-demo', 'index': ALL}, 'checked'),
)
def checkable_tag_demo(checked_list):
    return f'checked_list: {checked_list}'
"""
    }
]

```

### `views/AntdCheckableTag/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCheckableTag(
                content=f'标签{i}',
            )
            for i in range(1, 6)
        ],
        wrap=True,
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdCheckableTag(
            content=f'标签{i}',
        )
        for i in range(1, 6)
    ],
    wrap=True,
    style={
        'width': '100%',
    },
)
"""
    }
]

```

### `views/AntdCheckableTag/demos/checked_unchecked_content.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdCheckableTag(
                checkedContent='已选中',
                unCheckedContent='未选中',
            ),
            fac.AntdCheckableTag(
                checkedContent=fac.AntdSpace(
                    [
                        fac.AntdIcon(icon='antd-like'),
                        '取消',
                    ],
                    align='center',
                ),
                unCheckedContent=fac.AntdSpace(
                    [
                        fac.AntdIcon(icon='antd-like'),
                        '点赞',
                    ],
                    align='center',
                ),
            ),
        ],
        wrap=True,
        style={
            'width': '100%',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdCheckableTag(
            checkedContent='已选中',
            unCheckedContent='未选中',
        ),
        fac.AntdCheckableTag(
            checkedContent=fac.AntdSpace(
                [
                    fac.AntdIcon(icon='antd-like'),
                    '取消',
                ],
                align='center',
            ),
            unCheckedContent=fac.AntdSpace(
                [
                    fac.AntdIcon(icon='antd-like'),
                    '点赞',
                ],
                align='center',
            ),
        ),
    ],
    wrap=True,
    style={
        'width': '100%',
    },
)
"""
    }
]

```
