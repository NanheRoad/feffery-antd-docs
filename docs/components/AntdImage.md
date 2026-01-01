# AntdImage

## 简介源码：`views/AntdImage/intro.py`
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
                {'title': 'AntdImage 图片'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdImage 图片', level=2),
        fac.AntdParagraph('用于展示单张或一组图片。'),
    ]

```

## 示例源码（demos）

### `views/AntdImage/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdImage(
        src='/assets/imgs/components/AntdImage/示例图片1.jpg', height=400
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdImage(
    src='/assets/imgs/components/AntdImage/示例图片1.jpg.jpg', height=400
)
"""
    }
]

```

### `views/AntdImage/demos/fallback.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider('默认占位图', innerTextOrientation='left'),
        fac.AntdImage(
            src='/assets/imgs/不存在图片示例.jpg', preview=False, height=100
        ),
        fac.AntdDivider('自定义占位图', innerTextOrientation='left'),
        fac.AntdImage(
            src='/assets/imgs/不存在图片示例.jpg',
            fallback='/assets/imgs/components/AntdImage/示例占位图.png',
            preview=False,
            height=100,
        ),
    ]

    return demo_contents


code_string = [
    {
        'code': """
[
    fac.AntdDivider('默认占位图', innerTextOrientation='left'),
    fac.AntdImage(
        src='/assets/imgs/不存在图片示例.jpg', preview=False, height=100
    ),
    fac.AntdDivider('自定义占位图', innerTextOrientation='left'),
    fac.AntdImage(
        src='/assets/imgs/不存在图片示例.jpg',
        fallback='/assets/imgs/components/AntdImage/示例占位图.png',
        preview=False,
        height=100,
    ),
]
"""
    }
]

```

### `views/AntdImage/demos/multi.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdDivider(
            'multiImageMode="fold"（默认）', innerTextOrientation='left'
        ),
        fac.AntdImage(
            src=[
                f'/assets/imgs/components/AntdImage/示例图片{i}.png'
                for i in range(2, 9)
            ],
            height=80,
        ),
        fac.AntdDivider(
            'multiImageMode="unfold"（默认）', innerTextOrientation='left'
        ),
        fac.AntdImage(
            src=[
                f'/assets/imgs/components/AntdImage/示例图片{i}.png'
                for i in range(2, 9)
            ],
            multiImageMode='unfold',
            height=80,
        ),
    ]

    return demo_contents


code_string = [
    {
        'code': """
[
    fac.AntdDivider(
        'multiImageMode="fold"（默认）', innerTextOrientation='left'
    ),
    fac.AntdImage(
        src=[
            f'/assets/imgs/components/AntdImage/示例图片{i}.png'
            for i in range(2, 9)
        ],
        height=80,
    ),
    fac.AntdDivider(
        'multiImageMode="unfold"（默认）', innerTextOrientation='left'
    ),
    fac.AntdImage(
        src=[
            f'/assets/imgs/components/AntdImage/示例图片{i}.png'
            for i in range(2, 9)
        ],
        multiImageMode='unfold',
        height=80,
    ),
]
"""
    }
]

```

### `views/AntdImage/demos/preview_false.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdImage(
        src='/assets/imgs/components/AntdImage/示例图片1.jpg',
        height=400,
        preview=False,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdImage(
    src='/assets/imgs/components/AntdImage/示例图片1.jpg',
    height=400,
    preview=False,
)
"""
    }
]

```
