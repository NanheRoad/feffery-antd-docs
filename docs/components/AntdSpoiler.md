# AntdSpoiler

## 简介源码：`views/AntdSpoiler/intro.py`
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
                {'title': 'AntdSpoiler 展开收起'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSpoiler 展开收起', level=2),
        fac.AntdParagraph('用于实现对指定内容的展开收起效果。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100), maxHeight=70
)
```

### label_position

- 说明：演示 label_position 的用法。

#### 代码
```python
fac.AntdFlex(
    [
        fac.AntdSegmented(
            id='spolier-label-position-options',
            options=[
                {'label': 'left', 'value': 'left'},
                {'label': 'right', 'value': 'right'},
            ],
            defaultValue='left',
        ),
        fac.AntdSpoiler(
            fac.AntdParagraph('内容示例' * 100),
            id='spolier-label-position-demo',
            maxHeight=70,
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)

...

@app.callback(
    Output('spolier-label-position-demo', 'labelPosition'),
    Input('spolier-label-position-options', 'value'),
)
def update_spoiler_label_position(value):
    return value
```

### transition_duration

- 说明：演示 transition_duration 的用法。

#### 代码
```python
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100),
    maxHeight=70,
    transitionDuration=0.5,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- contentClassName (string | dict; optional):
    内容区css类名，支持[动态css](/advanced-classname).

- contentStyle (dict; optional):
    内容区css样式.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- hideLabel (a list of or a singular dash component, string or number; optional):
    组件型，展开状态下，收起按钮的文案内容.

- showLabel (a list of or a singular dash component, string or number; optional):
    组件型，收起状态下，展开按钮的文案内容.

- labelPosition (a value equal to: 'left', 'right'; default 'left'):
    展开/收起按钮的位置，可选项有`'left'`、`'right'`  默认值：`'left'`.

- open (boolean; default False):
    监听或设置是否处于展开状态  默认值：`False`.

- maxHeight (number; default 50):
    收起状态下，内容区域最大像素高度  默认值：`50`.

- transitionDuration (number; default 0.1):
    展开/收起过渡动画耗时，单位：秒  默认值：`0.1`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
