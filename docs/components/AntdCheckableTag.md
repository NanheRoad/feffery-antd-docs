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

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
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
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
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
```

### checked_unchecked_content

- 说明：演示 checked_unchecked_content 的用法。

#### 代码
```python
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
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- content (a list of or a singular dash component, string or number; optional):
    组件型，标签内容.

- checkedContent (a list of or a singular dash component, string or number; optional):
    组件型，选择状态下的标签内容.

- unCheckedContent (a list of or a singular dash component, string or number; optional):
    组件型，未选择状态下的标签内容.

- checked (boolean; default False):
    监听或设置当前标签的选择状态  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
