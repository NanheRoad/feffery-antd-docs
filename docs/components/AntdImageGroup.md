# AntdImageGroup

## 简介源码：`views/AntdImageGroup/intro.py`
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
                {'title': 'AntdImageGroup 图片组'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdImageGroup 图片组', level=2),
        fac.AntdParagraph('用于灵活整合一系列图片。'),
    ]

```

## 示例源码（demos）

### `views/AntdImageGroup/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdImageGroup(
        fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdImage(
                            src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                            height=100,
                        )
                        for i in range(2, 5)
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdImage(
                            src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                            height=100,
                        )
                        for i in range(5, 7)
                    ]
                ),
                fac.AntdSpace(
                    [
                        fac.AntdImage(
                            src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                            height=100,
                        )
                        for i in range(7, 9)
                    ]
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        )
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdImageGroup(
    fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdImage(
                        src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                        height=100,
                    )
                    for i in range(2, 5)
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdImage(
                        src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                        height=100,
                    )
                    for i in range(5, 7)
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdImage(
                        src=f'/assets/imgs/components/AntdImage/示例图片{i}.png',
                        height=100,
                    )
                    for i in range(7, 9)
                ]
            ),
        ],
        direction='vertical',
        style={'width': '100%'},
    )
)
"""
    }
]

```

### `views/AntdImageGroup/demos/items.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdImageGroup(
        fac.AntdImage(
            src='/assets/imgs/components/AntdImage/示例图片2.png',
            height=200,
        ),
        items=[
            f'/assets/imgs/components/AntdImage/示例图片{i}.png'
            for i in range(2, 9)
        ],
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdImageGroup(
    fac.AntdImage(
        src='/assets/imgs/components/AntdImage/示例图片2.png',
        height=200,
    ),
    items=[
        f'/assets/imgs/components/AntdImage/示例图片{i}.png'
        for i in range(2, 9)
    ],
)
"""
    }
]

```
