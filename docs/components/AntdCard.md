# AntdCard

## 简介源码：`views/AntdCard/intro.py`
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
                {'title': '卡片'},
                {'title': 'AntdCard 卡片'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCard 卡片', level=2),
        fac.AntdParagraph('用于构建美观的内容展示卡片。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### actions

- 说明：演示 actions 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            '社交软件常见交互演示', innerTextOrientation='left'
        ),
        fac.AntdCard(
            fac.AntdCardMeta(
                avatar=fac.AntdAvatar(
                    mode='image',
                    src='https://images.pexels.com/users/avatars/426868/mantas-sinkevicius-653.jpeg?auto=compress&fit=crop&h=130&w=130&dpr=1',
                ),
                description='https://www.pexels.com/@mantasink/',
                title='Mantas Sinkevičius',
            ),
            coverImg={
                'alt': 'demo pictrue',
                'src': 'https://images.pexels.com/photos/18664364/pexels-photo-18664364/free-photo-of-rock-formation-on-sea-shore-in-greece.jpeg',
            },
            actions=[
                fac.AntdIcon(
                    id={
                        'type': 'card-meta-actions-icon-demo',
                        'index': 'like',
                    },
                    icon='md-favorite-border',
                    style={'fontSize': 20},
                ),
                fac.AntdIcon(
                    id={
                        'type': 'card-meta-actions-icon-demo',
                        'index': 'fav',
                    },
                    icon='md-star-border',
                    style={'fontSize': 20},
                ),
                fac.AntdPopover(
                    fac.AntdIcon(
                        icon='md-forward',
                        style={'fontSize': 20},
                    ),
                    content=fac.AntdSpace(
                        [
                            '分享到：',
                            fac.AntdSpace(
                                [
                                    fac.AntdIcon(icon='antd-weibo'),
                                    fac.AntdIcon(icon='antd-alipay-circle'),
                                    fac.AntdIcon(icon='antd-github'),
                                    fac.AntdIcon(icon='antd-link'),
                                ],
                                style={'fontSize': 20},
                            ),
                        ],
                        direction='vertical',
                        style={'color': 'rgba(0,0,0,0.65)'},
                    ),
                    trigger=['hover', 'click'],
                ),
            ],
            hoverable=True,
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
)


# 点击like/favourite icon时切换icon样式
@app.callback(
    Output({'type': 'card-meta-actions-icon-demo', 'index': MATCH}, 'icon'),
    Input({'type': 'card-meta-actions-icon-demo', 'index': MATCH}, 'nClicks'),
    State({'type': 'card-meta-actions-icon-demo', 'index': MATCH}, 'icon'),
    prevent_initial_call=True,
)
def change_icon_style(nClicks, icon):
    if '-border' in icon:
        return icon.replace('-border', '')
    return icon + '-border'
```

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('卡片点击回调监听', innerTextOrientation='left'),
        fac.AntdSpace(
            [
                fac.AntdCard(
                    f'卡片{i}',
                    id={'type': 'card-click-demo', 'index': i},
                    # 设置鼠标悬浮指针为点击样式
                    style={'cursor': 'pointer'},
                    styles={'header': {'display': 'none'}},
                )
                for i in range(1, 4)
            ],
            wrap=True,
        ),
        html.Div('未点击卡片', id='card-click-demo-output'),
        fac.AntdDivider(
            '卡片网格点击回调监听', innerTextOrientation='left'
        ),
        fac.AntdCard(
            [
                fac.AntdCardGrid(
                    f'卡片网格{i}',
                    id={'type': 'card-grid-click-demo', 'index': i},
                    # 设置鼠标悬浮指针为点击样式
                    style={'cursor': 'pointer'},
                )
                for i in range(1, 4)
            ],
            style={'width': 300, 'marginBottom': 10},
            styles={'header': {'display': 'none'}},
        ),
        html.Div('未点击卡片网格', id='card-grid-click-demo-output'),
    ],
    direction='vertical',
)


# 点击卡片回调函数
@app.callback(
    Output('card-click-demo-output', 'children'),
    Input({'type': 'card-click-demo', 'index': ALL}, 'nClicks'),
    prevent_initial_call=True,
)
def card_click_callback(nClicks):
    nClicks = [i for i in nClicks if i is not None]
    num = sum(nClicks)
    current_card = f"卡片{dash.ctx.triggered_id['index']}"
    return f'卡片已点击{num}次，当前点击的是：{current_card}'


# 点击卡片网格回调函数
@app.callback(
    Output('card-grid-click-demo-output', 'children'),
    Input({'type': 'card-grid-click-demo', 'index': ALL}, 'nClicks'),
    prevent_initial_call=True,
)
def card_grid_click_callback(nClicks):
    nClicks = [i for i in nClicks if i is not None]
    num = sum(nClicks)
    current_card = f"卡片网格{dash.ctx.triggered_id['index']}"
    return f'卡片网格已点击{num}次，当前点击的是：{current_card}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCard(
            '''
从来就没有什么救世主，
也不靠神仙皇帝。
要创造人类的幸福，
全靠我们自己。
我们要夺回劳动果实，
让思想冲破牢笼。
快把那炉火烧得通红，
趁热打铁才能成功！
这是最后的斗争，
团结起来，到明天，
英特纳雄耐尔就一定要实现。
''',
            title='卡片示例',
            style={'width': 300, 'marginBottom': 10},
        ),
        fac.AntdCard(
            '''
从来就没有什么救世主，
也不靠神仙皇帝。
要创造人类的幸福，
全靠我们自己。
我们要夺回劳动果实，
让思想冲破牢笼。
快把那炉火烧得通红，
趁热打铁才能成功！
这是最后的斗争，
团结起来，到明天，
英特纳雄耐尔就一定要实现。
''',
            title='无边框卡片示例',
            variant='borderless',
            style={'width': 300, 'marginBottom': 10},
        ),
    ],
    direction='vertical',
)
```

### body_style

- 说明：演示 body_style 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('隐藏内容区示例', innerTextOrientation='left'),
        fac.AntdCard(
            '隐藏内容区示例',
            title='标题',
            styles={'body': {'display': 'none'}},
        ),
        fac.AntdDivider('设置内容区背景示例', innerTextOrientation='left'),
        fac.AntdCard(
            '设置内容区背景示例',
            title='标题',
            styles={'body': {'background': 'rgba(0, 0, 0, 0.3)'}},
        ),
    ],
    direction='vertical',
    style={'width': 300},
)
```

### card_grid

- 说明：演示 card_grid 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            'AntdCardGrid基础使用', innerTextOrientation='left'
        ),
        fac.AntdCard(
            [fac.AntdCardGrid(f'内容{i}') for i in range(1, 16)],
            title='AntdCardGrid基础使用',
        ),
        fac.AntdDivider(
            '调整浏览器窗口尺寸以观察换行效果', innerTextOrientation='left'
        ),
        fac.AntdCard(
            [
                fac.AntdCardGrid(f'内容{i}', style={'width': 95})
                for i in range(1, 16)
            ],
            title='固定AntdCardGrid宽度以支持自动换行',
        ),
        fac.AntdDivider('紧凑的网格内容区', innerTextOrientation='left'),
        fac.AntdCard(
            [fac.AntdCardGrid(f'内容{i}') for i in range(1, 16)],
            title='调整各类样式以实现紧凑的网格内容区',
            variant='borderless',
            style={'borderRadius': '8px 8px 0 0'},
            styles={
                'body': {'padding': '0px 1px 0px 0px', 'border': 0},
                'header': {'border': '1px solid #f0f0f0'},
            },
        ),
        fac.AntdDivider('关闭悬停阴影效果', innerTextOrientation='left'),
        fac.AntdCard(
            [
                fac.AntdCardGrid(f'内容{i}', hoverable=False)
                for i in range(1, 16)
            ],
            title='关闭悬停阴影效果',
        ),
    ],
    direction='vertical',
)
```

### card_meta

- 说明：演示 card_meta 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('AntdCardMeta基础使用', innerTextOrientation='left'),
        fac.AntdCard(
            fac.AntdCardMeta(
                avatar=fac.AntdAvatar(
                    mode='image',
                    src='https://images.pexels.com/users/avatars/426868/mantas-sinkevicius-653.jpeg?auto=compress&fit=crop&h=130&w=130&dpr=1',
                ),
                description='https://www.pexels.com/@mantasink/',
                title='Mantas Sinkevičius',
            ),
            coverImg={
                'alt': 'demo pictrue',
                'src': 'https://images.pexels.com/photos/18664364/pexels-photo-18664364/free-photo-of-rock-formation-on-sea-shore-in-greece.jpeg',
            },
            hoverable=True,
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider(
            'AntdCardMeta可与其他组件自由组合', innerTextOrientation='left'
        ),
        fac.AntdCard(
            [
                fac.AntdDivider('Card Meta 1'),
                fac.AntdCardMeta(
                    avatar=fac.AntdAvatar(
                        mode='image',
                        src='https://images.pexels.com/users/avatars/426868/mantas-sinkevicius-653.jpeg?auto=compress&fit=crop&h=130&w=130&dpr=1',
                    ),
                    description='https://www.pexels.com/@mantasink/',
                    title='Mantas Sinkevičius',
                ),
                fac.AntdDivider('Card Meta 2'),
                fac.AntdCardMeta(
                    avatar=fac.AntdAvatar(
                        mode='image',
                        src='https://images.pexels.com/users/avatars/426868/mantas-sinkevicius-653.jpeg?auto=compress&fit=crop&h=130&w=130&dpr=1',
                    ),
                    description='https://www.pexels.com/@mantasink/',
                    title='Mantas Sinkevičius',
                ),
            ],
            coverImg={
                'alt': 'demo pictrue',
                'src': 'https://images.pexels.com/photos/18664364/pexels-photo-18664364/free-photo-of-rock-formation-on-sea-shore-in-greece.jpeg',
            },
            styles={
                'body': {'flexDirection': 'column'},
                'header': {'display': 'none'},
            },
            hoverable=True,
        ),
        fac.AntdDivider(
            '组件化使用description', innerTextOrientation='left'
        ),
        fac.AntdCard(
            fac.AntdCardMeta(
                description=fac.AntdRow(
                    [
                        fac.AntdCol(
                            [
                                fac.AntdText(i[0], type='secondary'),
                                fac.AntdText(i[1]),
                            ],
                            span=6,
                            style={
                                'display': 'flex',
                                'flex-direction': 'column',
                            },
                        )
                        for i in [
                            ['Dimensions', '3880x5820'],
                            ['Aspect Ratio', '2:3'],
                            ['Camera', 'ILCE-6000'],
                            ['Focal', '24.0mm'],
                            ['Aperture', 'f/2.8'],
                            ['ISO', '100'],
                            ['Shutter Speed', '1/2000s'],
                            ['Taken At', 'Apr23,2023'],
                        ]
                    ],
                    gutter=[5, 10],
                ),
                title='Rock Formation on Sea Shore in Greece',
            ),
            coverImg={
                'alt': 'demo pictrue',
                'src': 'https://images.pexels.com/photos/18664364/pexels-photo-18664364/free-photo-of-rock-formation-on-sea-shore-in-greece.jpeg',
            },
            hoverable=True,
            styles={'header': {'display': 'none'}},
        ),
    ],
    direction='vertical',
    style={'width': 450},
)
```

### cover

- 说明：演示 cover 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('封面图片示例', innerTextOrientation='left'),
        fac.AntdCard(
            '内容',
            title='标题',
            coverImg={
                'alt': '图片加载失败！',
                'src': 'https://images.pexels.com/photos/18664364/pexels-photo-18664364/free-photo-of-rock-formation-on-sea-shore-in-greece.jpeg',
            },
            style={'width': 300, 'marginBottom': 10},
        ),
        fac.AntdDivider('加载失败alt信息示例', innerTextOrientation='left'),
        fac.AntdCard(
            '内容',
            title='标题',
            coverImg={
                'alt': '图片加载失败！',
                'src': 'https://错误的src地址',
            },
            style={'width': 300, 'marginBottom': 10},
        ),
    ],
    direction='vertical',
)
```

### extra

- 说明：演示 extra 的用法。

#### 代码
```python
fac.AntdCard(
    '''
从来就没有什么救世主，
也不靠神仙皇帝。
要创造人类的幸福，
全靠我们自己。
我们要夺回劳动果实，
让思想冲破牢笼。
快把那炉火烧得通红，
趁热打铁才能成功！
这是最后的斗争，
团结起来，到明天，
英特纳雄耐尔就一定要实现。
''',
    title='卡片示例',
    # 因设置了extra，extraLink将不会生效
    extraLink={
        'content': '链接示例',
        'href': 'https://zh.wikipedia.org/zh-hans/国际歌',
    },
    extra=fac.AntdButton(
        'extra示例',
        type='primary',
        href='https://zh.wikipedia.org/zh-hans/国际歌',
    ),
    style={'width': 300, 'marginBottom': 10},
)
```

### extra_link

- 说明：演示 extra_link 的用法。

#### 代码
```python
fac.AntdCard(
    '''
从来就没有什么救世主，
也不靠神仙皇帝。
要创造人类的幸福，
全靠我们自己。
我们要夺回劳动果实，
让思想冲破牢笼。
快把那炉火烧得通红，
趁热打铁才能成功！
这是最后的斗争，
团结起来，到明天，
英特纳雄耐尔就一定要实现。
''',
    title='卡片示例',
    extraLink={
        'content': '链接示例',
        'href': 'https://zh.wikipedia.org/zh-hans/国际歌',
    },
    style={'width': 300, 'marginBottom': 10},
)
```

### head_style

- 说明：演示 head_style 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('隐藏标题栏示例', innerTextOrientation='left'),
        fac.AntdCard(
            '隐藏标题栏示例',
            title='卡片示例',
            styles={'header': {'display': 'none'}},
        ),
        fac.AntdDivider('设置标题栏背景示例', innerTextOrientation='left'),
        fac.AntdCard(
            '设置标题栏背景示例',
            title='标题',
            styles={'header': {'background': 'rgba(0, 0, 0, 0.3)'}},
        ),
    ],
    direction='vertical',
    style={'width': 300},
)
```

### hoverable

- 说明：演示 hoverable 的用法。

#### 代码
```python
fac.AntdCard(
    """
    从来就没有什么救世主，
也不靠神仙皇帝。
要创造人类的幸福，
全靠我们自己。
我们要夺回劳动果实，
让思想冲破牢笼。
快把那炉火烧得通红，
趁热打铁才能成功！
这是最后的斗争，
团结起来，到明天，
英特纳雄耐尔就一定要实现。
    """,
    title='卡片示例',
    hoverable=True,
    style={'width': 300, 'marginBottom': 10},
)
```

### size

- 说明：演示 size 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdCard(
            'size="default"',
            title='卡片示例'
        ),

        fac.AntdCard(
            'size="small"',
            title='卡片示例',
            size='small'
        )
    ],
    direction='vertical'
)
```
