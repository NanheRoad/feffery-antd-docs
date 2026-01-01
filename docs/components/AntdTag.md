# AntdTag

## 简介源码：`views/AntdTag/intro.py`
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
                {'title': 'AntdTag 标签'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTag 标签', level=2),
        fac.AntdParagraph('用于渲染美观的小标签。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### add_delete_tag

- 说明：演示 add_delete_tag 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        # 使用FefferyAutoAnimate代替html.Div，为其子元素自动添加增删动画
        fuc.FefferyAutoAnimate(
            [
                fac.AntdTag(
                    content='不可关闭标签',
                    # 调整样式使得内部的关闭按钮居中，字体大小与其他组件统一
                    style={
                        'font-size': 14,
                        'display': 'flex',
                        'align-items': 'center',
                    },
                ),
                fac.AntdTag(
                    content='可关闭标签1',
                    closeIcon=True,
                    id={
                        'type': 'tag-close-counts-closeable-demo',
                        'index': 1,
                    },
                    style={
                        'font-size': 14,
                        'display': 'flex',
                        'align-items': 'center',
                    },
                ),
                fac.AntdTag(
                    content='可关闭标签2',
                    closeIcon=True,
                    id={
                        'type': 'tag-close-counts-closeable-demo',
                        'index': 2,
                    },
                    style={
                        'font-size': 14,
                        'display': 'flex',
                        'align-items': 'center',
                    },
                ),
                html.Div(
                    [
                        # 设置尺寸使得AntdButton的样式大小接近AntdTag
                        fac.AntdButton(
                            '新增标签',
                            icon=fac.AntdIcon(icon='antd-plus'),
                            type='dashed',
                            size='small',
                            id='tag-close-counts-add-btn-demo',
                        ),
                        html.Div(
                            id='tag-close-counts-input-container-demo'
                        ),
                    ]
                ),
            ],
            id='tag-close-counts-closeable-demo-container',
            style={
                'display': 'flex',
                'flex-wrap': 'wrap',
                'gap': 5,
            },
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)


# 添加标签按钮点击后，渲染输入框，并隐藏新增按钮
@app.callback(
    [
        Output('tag-close-counts-input-container-demo', 'children'),
        Output('tag-close-counts-add-btn-demo', 'style'),
    ],
    Input('tag-close-counts-add-btn-demo', 'nClicks'),
    prevent_initial_call=True,
)
def add_tag_callback(nClicks):
    return fac.AntdInput(
        id='tag-close-counts-input-demo',
        autoFocus=True,
        size='small',
        style={'width': 94},
    ), {'display': 'none'}


# 输入框失焦或submit后，删除输入框，并显示新增按钮
@app.callback(
    [
        Output(
            'tag-close-counts-input-container-demo',
            'children',
            allow_duplicate=True,
        ),
        Output('tag-close-counts-add-btn-demo', 'style', allow_duplicate=True),
    ],
    [
        Input('tag-close-counts-input-demo', 'focusing'),
        Input('tag-close-counts-input-demo', 'nSubmit'),
    ],
    prevent_initial_call=True,
)
def switch_show_add_btn_callback(focusing, nSubmit):
    if not focusing or nSubmit:
        return [], {}
    return dash.no_update


# 输入框失焦后或submit后，新增标签
@app.callback(
    Output('tag-close-counts-closeable-demo-container', 'children'),
    [
        Input('tag-close-counts-input-demo', 'focusing'),
        Input('tag-close-counts-input-demo', 'nSubmit'),
    ],
    [
        State('tag-close-counts-input-demo', 'value'),
        State('tag-close-counts-closeable-demo-container', 'children'),
    ],
    prevent_initial_call=True,
)
def add_tag_add_btn_callback(focusing, nSubmit, value, children):
    if not value:
        return dash.no_update
    if not focusing or nSubmit:
        # 替换children末位元素，从AntdButton、AntdInput的容器替换为新增的标签
        children[-1] = fac.AntdTag(
            content=value,
            closeIcon=True,
            id={
                'type': 'tag-close-counts-closeable-demo',
                'index': max(
                    [
                        i['props']['id']['index']
                        for i in children
                        if 'id' in i['props']
                    ]  # 不能使用len，删除前置后新增容易重复导致无法删除
                )
                + 1,
            },
            style={
                'font-size': 14,
                'display': 'flex',
                'align-items': 'center',
            },
        )
        # 将被替换的AntdButton、AntdInput的容器重新添加到末位，实现增删改才会触发的动画效果，同时避免一些显示bug
        children.append(
            html.Div(
                [
                    fac.AntdButton(
                        '新增标签',
                        icon=fac.AntdIcon(icon='antd-plus'),
                        type='dashed',
                        size='small',
                        id='tag-close-counts-add-btn-demo',
                        style={},
                    ),
                    html.Div(id='tag-close-counts-input-container-demo'),
                ]
            )
        )
        return children

    return dash.no_update


# 标签关闭按钮点击事件
@app.callback(
    Output(
        'tag-close-counts-closeable-demo-container',
        'children',
        allow_duplicate=True,
    ),
    Input(
        {
            'type': 'tag-close-counts-closeable-demo',
            'index': ALL,
        },
        'closeCounts',
    ),
    State('tag-close-counts-closeable-demo-container', 'children'),
    prevent_initial_call=True,
)
def close_counts_closeable_callback(closeCounts, children):
    for i in closeCounts:
        if i is not None:
            trigger_id = dash.ctx.triggered_id
            for i, child in enumerate(children.copy()):
                if (
                    'id' in child['props']
                    and trigger_id == child['props']['id']
                ):
                    children.pop(i)
```

### as_link

- 说明：演示 as_link 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTag(
            content='fac.AntdTag',
            href='AntdTag',
            # 跳转行为：当页跳转
            target='_self',
            color='blue',
        ),
        fac.AntdTag(
            content='fmc官网',
            href='https://fmc.feffery.tech',
            # 跳转行为：新标签页跳转（默认）
            target='_blank',
            color='green',
        ),
        fac.AntdTag(
            content='fuc官网', href='https://fuc.feffery.tech', color='cyan'
        ),
    ],
    wrap=True,
    style={
        'width': '100%',
    },
)
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTag(
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

### border

- 说明：演示 border 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=f'标签{i}',
                    bordered=False,
                )
                for i in range(1, 6)
            ],
            wrap=True,
        ),
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=i,
                    color=i,
                    bordered=False,
                )
                for i in [
                    'magenta',
                    'red',
                    'volcano',
                    'orange',
                    'gold',
                    'lime',
                    'green',
                    'cyan',
                    'blue',
                    'geekblue',
                    'purple',
                ]
            ],
            wrap=True,
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
```

### close_counts

- 说明：演示 close_counts 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            '尝试点击标签内的关闭按钮', innerTextOrientation='left'
        ),
        fac.AntdTag(
            content='标签', closeIcon=True, id='tag-close-counts-demo'
        ),
        fac.AntdCard(
            '当前未点击标签关闭按钮',
            id='tag-close-counts-output-demo',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)


@app.callback(
    Output('tag-close-counts-output-demo', 'children'),
    Input('tag-close-counts-demo', 'closeCounts'),
    prevent_initial_call=True,
)
def close_counts_callback(closeCounts):
    return f'当前标签关闭按钮点击次数为：{closeCounts}次'
```

### close_icon

- 说明：演示 close_icon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=f'标签{i}',
                    closeIcon=True,
                )
                for i in range(1, 6)
            ],
            wrap=True,
        ),
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=i,
                    color=i,
                    closeIcon=True,
                )
                for i in [
                    'magenta',
                    'red',
                    'volcano',
                    'orange',
                    'gold',
                    'lime',
                    'green',
                    'cyan',
                    'blue',
                    'geekblue',
                    'purple',
                ]
            ],
            wrap=True,
        ),
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=i,
                    color=i,
                    closeIcon=True,
                )
                for i in [
                    '#8039d6',
                    '#d63987',
                    'hsl(188.51deg 85.45% 32.35%)',
                    'rgb(60, 150, 231)',
                    'rgb(198 143 22 / 100%)',
                    'rgba(231, 76, 60, 1)',
                ]
            ],
            wrap=True,
        ),
    ],
    wrap=True,
    style={
        'width': '100%',
    },
)
```

### color

- 说明：演示 color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('使用内置色彩主题', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=i,
                    color=i,
                )
                for i in [
                    'magenta',
                    'red',
                    'volcano',
                    'orange',
                    'gold',
                    'lime',
                    'green',
                    'cyan',
                    'blue',
                    'geekblue',
                    'purple',
                ]
            ],
            wrap=True,
        ),
        fac.AntdDivider('使用任意css颜色值', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdTag(
                    content=i,
                    color=i,
                )
                for i in [
                    '#8039d6',
                    '#d63987',
                    'hsl(188.51deg 85.45% 32.35%)',
                    'rgb(60, 150, 231)',
                    'rgb(198 143 22 / 100%)',
                    'rgba(231, 76, 60, 1)',
                ]
            ],
            wrap=True,
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)
```

### custom_preset_color

- 说明：演示 custom_preset_color 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('使用示例', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdTag(content=i, style=generate_tag_colors(i))
                for i in [
                    '#8039d6',
                    '#d63987',
                    'rgb(63 215 121)',
                    'rgb(60, 150, 231)',
                    'rgb(198 143 22 / 100%)',
                    'rgba(231, 76, 60, 1)',
                ]
            ],
            wrap=True,
        ),
        fac.AntdDivider('请选择颜色', innerTextOrientation='left'),
        fac.AntdColorPicker(
            id='tag-color-picker-demo',
            placement='top',
            showText=True,
        ),
        fac.AntdTag(
            content='自定义标签',
            id='tag-color-picker-tag-demo',
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)


def generate_tag_colors(font_color):
    """
    根据给定的字体颜色生成适合的标签颜色。
    注：在浅色字体情况下表现不好。

    参数:
    font_color (str): 字体颜色，接受HEX、RGB、HSB格式。

    返回:
    适用于Dash style属性的字典，包含字体颜色、背景颜色、边框颜色。
    """
    import colorsys
    def hex_to_rgb(hex_code):
        if hex_code.startswith('#'):
            hex_code = hex_code.lstrip('#')

        r = int(hex_code[:2], 16)
        g = int(hex_code[2:4], 16)
        b = int(hex_code[4:6], 16)

        return r, g, b

    if '#' in font_color:
        rgb_color = hex_to_rgb(font_color)
        _h, _l, _s = colorsys.rgb_to_hls(*rgb_color)
    elif 'rgb' in font_color:
        rgb = (
            font_color.split('(')[1]
            .split(')')[0]
            .split(',' if ',' in font_color else ' ')[:3]
        )
        r, g, b = (
            int(rgb[0]),
            int(rgb[1]),
            int(rgb[2].split('/')[0]) if '/' in rgb[2] else int(rgb[2]),
        )
        _h, _l, _s = colorsys.rgb_to_hls(r, g, b)
    elif 'hsb' in font_color:
        hsb = (
            font_color.split('(')[1]
            .split(')')[0]
            .split(',' if ',' in font_color else ' ')[:3]
        )
        __h, __s, __b = (
            float(int(hsb[0].strip()) / 360),
            float(hsb[1].strip().replace('%', '')) / 100.0
            if '%' in hsb[1]
            else float(hsb[1].strip()),
            float(hsb[2].strip().replace('%', '')) / 100.0
            if '%' in hsb[1]
            else float(hsb[1].strip()),
        )

        r, g, b = colorsys.hsv_to_rgb(__h, __s, __b)
        _h, _l, _s = colorsys.rgb_to_hls(r, g, b)
        # 转换为hsl格式供web使用
        font_color = f'hsl({_h*360}, {_s*100.0:.2f}%, {_l*100.0:.2f}%)'
    else:
        return None

    background_hsl = f'hsl({_h*360:.0f}, 100%, 95%)'
    border_hsl = f'hsl({_h*360:.0f}, 100%, 70%)'

    return {
        'color': font_color,
        'background-color': background_hsl,
        'border-color': border_hsl,
    }


@app.callback(
    Output('tag-color-picker-tag-demo', 'style'),
    Input('tag-color-picker-demo', 'value'),
)
def callback_func(value):
    value = value or '#1677ff'

    return generate_tag_colors(value)
```

### draggable_tag

- 说明：演示 draggable_tag 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferySortable(
            id='tag-draggable-sortable-demo',
            items=[
                {
                    'key': f'标签{i}',
                    'content': fac.AntdTag(
                        content=f'标签{i}',
                        href='anywhere',
                        style={'marginInlineEnd': 0},
                    ),
                    'style': {
                        'position': 'relative',
                        'display': 'inline-flex',
                        'borderRadius': 8,
                        'marginRight': 8,
                    },
                    'draggingStyle': {
                        'boxShadow': '0px 0px 12px rgba(0, 0, 0, 0.12)',
                    },
                }
                for i in range(1, 6)
            ],
            direction='horizontal',
            itemDraggingScale=1.025,
            # 注：当前示例的实现方式，实际上是将FefferySortable的拖拽handle设为透明并扩大大小覆盖整个AntdTag
            # 因此，如果AntdTag的content中存在任何可交互组件，交互将会失效
            handleStyle={'color': 'transparent'},
            handleClassName={
                'position': 'absolute',
                'width': 'calc(100% - 8px)',
                'height': 'calc(100% - 8px)',
                'padding': '4px',
                'borderRadius': '8px',
            },
        ),
        fac.AntdCard(
            id='tag-draggable-output-demo',
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)


# 展示当前排序的回调
@app.callback(
    Output('tag-draggable-output-demo', 'children'),
    Input('tag-draggable-sortable-demo', 'currentOrder'),
)
def sortable_list_demo(currentOrder):
    return str(currentOrder)
```

### icon

- 说明：演示 icon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdTag(
            content='Loading...',
            icon=fac.AntdIcon(icon='antd-loading'),
            color='#0086ff',
        ),
        fac.AntdTag(
            content='Warning!',
            icon=fac.AntdIcon(
                icon='fc-high-priority',
                style={'position': 'relative', 'top': 1},
            ),
            color='red',
        ),
        fac.AntdTag(
            content='Stars',
            icon=fac.AntdIcon(icon='antd-github'),
            style={
                'fontSize': '14px',
                'fontWeight': 'bold',
                'background': 'linear-gradient(to bottom, #fcfcfc, #e4e4e4)',
            },
        ),
    ],
    wrap=True,
    style={
        'width': '100%',
    },
)
```
