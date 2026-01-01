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

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素css样式.

    - image (dict; optional):
        图标元素css样式.

    - description (dict; optional):
        描述元素css样式.

    - footer (dict; optional):
        底部元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素css类名.

    - image (string; optional):
        图标元素css类名.

    - description (string; optional):
        描述元素css类名.

    - footer (string; optional):
        底部元素css类名.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- description (a list of or a singular dash component, string or number | boolean; optional):
    描述信息内容.

- image (string | a value equal to: 'default', 'simple'; default 'default'):
    状态图片地址，也可以使用内置图片，可选项有`'default'`、`'simple'`  默认值：`'default'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
