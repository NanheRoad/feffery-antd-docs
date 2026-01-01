# AntdIcon

## 简介源码：`views/AntdIcon/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('通用')},
                {'title': translator.t('AntdIcon 图标')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdIcon 图标'), level=2),
        fac.AntdParagraph(translator.t('用于提示不同的功能及场景。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 回调监听

- 说明：通过`nClicks`进行图标点击事件的监听，特别地，在有效设置参数`debounceWait`后，将针对点击事件进行防抖监听，避免过于频繁的触发。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdText('常规点击事件：'),
                fac.AntdIcon(
                    id='icon-basic-event',
                    icon='antd-thunderbolt',
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-basic-event-output'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdText('防抖点击事件：'),
                fac.AntdIcon(
                    id='icon-debounce-event',
                    icon='antd-thunderbolt',
                    debounceWait=300,
                    style={'cursor': 'pointer'},
                ),
                fac.AntdText(id='icon-debounce-event-output'),
            ]
        ),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('icon-basic-event-output', 'children'),
    Input('icon-basic-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_basic_event(nClicks):
    return f'nClicks: {nClicks}'


@app.callback(
    Output('icon-debounce-event-output', 'children'),
    Input('icon-debounce-event', 'nClicks'),
    prevent_initial_call=True,
)
def icon_debounce_event(nClicks):
    return f'nClicks: {nClicks}'
```

### 基础使用

- 说明：通过参数`icon`来使用对应的不同类别的图标。

#### 代码
```python
fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdSpace(
                [
                    # 懒加载优化
                    fuc.FefferyLazyLoad(
                        fac.AntdIcon(icon=icon, style={'fontSize': 26}),
                        height=44,
                    ),
                    fac.AntdText(
                        icon,
                        locale='zh-cn',
                        copyable=True,
                        style={'borderBottom': '1px dashed #e1dfdd'},
                    ),
                ],
                direction='vertical',
                size=0,
                style={
                    'display': 'flex',
                    'alignItems': 'center',
                    'justifyContent': 'center',
                    'marginBottom': '5px',
                },
            ),
            # 响应式显示优化
            xs=24,
            sm=12,
            md=12,
            lg=12,
            xl=8,
            xxl=6,
        )
        for icon in DemosConfig.all_icons
    ]
)
```

### 配合iconfont图标资源

- 说明：设置参数`mode='iconfont'`后可使用参数`scriptUrl`引用单个或多个基于[iconfont](https://www.iconfont.cn/)项目导出的图标资源。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdIcon(
                    icon=icon,
                    mode='iconfont',
                    scriptUrl='//at.alicdn.com/t/font_8d5l8fzk5b87iudi.js',
                )
                for icon in ['icon-tuichu', 'icon-facebook', 'icon-twitter']
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdIcon(
                    icon=icon,
                    mode='iconfont',
                    scriptUrl=[
                        '//at.alicdn.com/t/font_1788044_0dwu4guekcwr.js',
                        '//at.alicdn.com/t/font_1788592_a5xf2bdic3u.js',
                    ],
                )
                for icon in [
                    'icon-javascript',
                    'icon-java',
                    'icon-shoppingcart',
                    'icon-python',
                ]
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明

- id (string; optional):
    Unique identifier for the component.

- aria-* (string; optional):
    Wildcard for attributes in the `aria-*` format.

- className (string | dict; optional):
    CSS class name for the current component, supports [dynamic CSS](/advanced-classname).

- data-* (string; optional):
    Wildcard for attributes in the `data-*` format.

- debounceWait (number; default 0):
    Debounce delay for the icon click event listener, in milliseconds. Default value: `0`.

- icon (string; optional):
    Name of the icon.

- key (string; optional):
    Updating the `key` value of the current component can force a redraw of the component.

- loading_state (dict; optional):
    `loading_state` is a dictionary with keys:
    - component_name (string; optional):
        Holds the name of the component that is loading.
    - is_loading (boolean; optional):
        Determines if the component is loading or not.
    - prop_name (string; optional):
        Holds which property is loading.

- nClicks (number; default 0):
    Number of times the icon has been clicked, used to monitor icon click behavior. Default value: `0`.

- style (dict; optional):
    CSS styles for the current component.
