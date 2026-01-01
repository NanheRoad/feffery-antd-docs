# AntdCustomSkeleton

## 简介源码：`views/AntdCustomSkeleton/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '反馈'},
                {'title': '骨架屏'},
                {'title': 'AntdCustomSkeleton 自定义骨架屏'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCustomSkeleton 自定义骨架屏', level=2),
        fac.AntdParagraph('用于自由设计骨架屏加载中内容。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '触发2秒自定义骨架屏动画',
            id='skeleton-custom-demo-input',
            type='primary',
        ),
        fac.AntdCustomSkeleton(
            id='custom-skeleton-demo',
            skeletonContent=html.Div(
                [
                    fac.AntdRow(
                        [
                            fac.AntdCol(
                                fac.AntdSkeletonButton(
                                    block=True, active=True
                                ),
                                span=6,
                                style={'padding': '4px'},
                            )
                        ]
                        * 16
                    ),
                    fac.AntdSpace(
                        [
                            html.Div(
                                fac.AntdSkeletonButton(
                                    active=True, size='small', block=True
                                ),
                                style={'width': '80px'},
                            ),
                            html.Div(
                                fac.AntdSkeletonButton(
                                    active=True, size='small', block=True
                                ),
                                style={'width': '60px'},
                            ),
                        ],
                        style={
                            'float': 'right',
                            'paddingRight': '4px',
                            'paddingTop': '15px',
                        },
                    ),
                ]
            ),
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('custom-skeleton-demo', 'children'),
    Input('skeleton-custom-demo-input', 'nClicks'),
)
def skeleton_custom_callback_demo(nClicks):
    time.sleep(2)

    return fac.AntdTable(
        columns=[
            {'title': '国家名示例', 'dataIndex': '国家名示例', 'width': '25%'},
            {'title': '省份名示例', 'dataIndex': '省份名示例', 'width': '25%'},
            {'title': '城市名示例', 'dataIndex': '城市名示例', 'width': '25%'},
            {'title': '日期示例', 'dataIndex': '日期示例', 'width': '25%'},
        ],
        bordered=True,
        data=[
            {
                'key': i,
                '国家名示例': faker.country(),
                '省份名示例': faker.province(),
                '城市名示例': faker.city_name(),
                '日期示例': faker.date(pattern='%Y-%m-%d', end_datetime=None),
            }
            for i in range(3)
        ],
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

- skeletonContent (a list of or a singular dash component, string or number; optional):
    组件型，加载状态下显示的内容.

- loading (boolean; default False):
    是否处于加载中状态.

- delay (number; optional):
    加载动画渲染延时，单位：毫秒  默认值：`0`.

- debug (boolean; default False):
    是否开启debug模式，开启后，每次动画加载都会在开发者工具的控制台打印相关`prop`信息  默认值：`False`.

- listenPropsMode (a value equal to: 'default', 'exclude', 'include'; default 'default'):
    监听模式，可选项有`'default'`、`'exclude'`、`'include'`  默认值：`'default'`.

- excludeProps (list of strings; optional):
    `listenPropsMode='exclude'`时，设置需要排除监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- includeProps (list of strings; optional):
    `listenPropsMode='include'`时，设置需要包含监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- manual (boolean; default False):
    是否开启手动控制模式，开启后是否处于加载状态将由`loading`参数控制，与内部元素参与的回调状态无关  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
