# AntdEmpty

## 简介源码：`views/AntdEmpty/intro.py`
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
                {'title': 'AntdEmpty 空状态'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdEmpty 空状态', level=2),
        fac.AntdParagraph('用于在信息缺失时起到占位说明的作用。'),
    ]

```

## 示例源码（demos）

### `views/AntdEmpty/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdEmpty()

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdEmpty()
"""
    }
]

```

### `views/AntdEmpty/demos/custom_image.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdEmpty(
        image='/assets/imgs/components/AntdEmpty/自定义占位图.png'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdEmpty(
    image='/assets/imgs/components/AntdEmpty/自定义占位图.png'
)
"""
    }
]

```

### `views/AntdEmpty/demos/hide_description.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdEmpty(description=False)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdEmpty(description=False)
"""
    }
]

```

### `views/AntdEmpty/demos/image_style.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdEmpty(
        image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
        description=fac.AntdText('当前页面开发中...', type='secondary'),
        styles={'image': {'height': 250}},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdEmpty(
    image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
    description=fac.AntdText('当前页面开发中...', type='secondary'),
    styles={'image': {'height': 250}},
)
"""
    }
]

```

### `views/AntdEmpty/demos/simple.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdEmpty(image='simple')

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdEmpty(image='simple')
"""
    }
]

```
