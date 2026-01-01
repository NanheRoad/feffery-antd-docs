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

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdEmpty()
```

### custom_image

- 说明：演示 custom_image 的用法。

#### 代码
```python
fac.AntdEmpty(
    image='/assets/imgs/components/AntdEmpty/自定义占位图.png'
)
```

### hide_description

- 说明：演示 hide_description 的用法。

#### 代码
```python
fac.AntdEmpty(description=False)
```

### image_style

- 说明：演示 image_style 的用法。

#### 代码
```python
fac.AntdEmpty(
    image='/assets/imgs/components/AntdEmpty/自定义占位图.png',
    description=fac.AntdText('当前页面开发中...', type='secondary'),
    styles={'image': {'height': 250}},
)
```

### simple

- 说明：演示 simple 的用法。

#### 代码
```python
fac.AntdEmpty(image='simple')
```
