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

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdImage(
    src='/assets/imgs/components/AntdImage/示例图片1.jpg.jpg', height=400
)
```

### fallback

- 说明：演示 fallback 的用法。

#### 代码
```python
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
```

### multi

- 说明：演示 multi 的用法。

#### 代码
```python
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
```

### preview_false

- 说明：演示 preview_false 的用法。

#### 代码
```python
fac.AntdImage(
    src='/assets/imgs/components/AntdImage/示例图片1.jpg',
    height=400,
    preview=False,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- alt (string; optional):
    图片alt信息.

- width (number | string; optional):
    图片宽度.

- height (number | string; optional):
    图片高度.

- src (string | list of strings; optional):
    配置图片资源地址，当传入数组时为多图片模式.

- fallback (string; optional):
    图片加载失败占位图资源地址.

- multiImageMode (a value equal to: 'fold', 'unfold'; default 'fold'):
    多图片模式展示方式，可选项有`'fold'`、`'unfold'`  默认值：`'fold'`.

- previewVisible (boolean; optional):
    监听或控制当前图片预览层是否处于打开状态.

- previewCurrent (number; optional):
    监听或控制当前图片预览对应切换到的图片下标.

- preview (dict; default True):
    配置图片预览相关功能，传入`False`时会禁用预览功能  默认值：`True`.

    `preview` is a boolean | dict with keys:

    - src (string; optional):
        自定义预览图链接地址.

    - movable (boolean; optional):
        预览模式下是否可移动图片.

    - mask (a list of or a singular dash component, string or number; optional):
        组件型，用于自定义缩略图遮罩元素.

    - maskClassName (string; optional):
        缩略图遮罩元素css类名.

    - rootClassName (string; optional):
        缩略图根节点css类名.

    - scaleStep (number; optional):
        `1+scaleStep`值为每一步缩放的倍数  默认值：`0.5`.

    - minScale (number; optional):
        最小缩放倍数  默认值：`1`.

    - maxScale (number; optional):
        最大缩放倍数  默认值：`50`.

- toolbarExtra (a list of or a singular dash component, string or number; optional):
    针对预览模式下的工具栏，末尾扩充自定义工具图标元素.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
