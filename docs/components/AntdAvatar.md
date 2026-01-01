# AntdAvatar

## 简介源码：`views/AntdAvatar/intro.py`
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
                {'title': 'AntdAvatar 头像'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdAvatar 头像', level=2),
        fac.AntdParagraph('用于渲染图标、文字或图片形式的头像。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### background

- 说明：演示 background 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(id='avatar-bg-color-input'),
        fac.AntdSpace(
            [
                fac.AntdAvatar(id='avatar-bg-color-icon-demo'),
                fac.AntdAvatar(
                    id='avatar-bg-color-text-demo', mode='text', text='F'
                ),
            ]
        ),
    ],
    style={'width': '100%'},
)

...

@app.callback(
    [
        Output('avatar-bg-color-icon-demo', 'style'),
        Output('avatar-bg-color-text-demo', 'style'),
    ],
    Input('avatar-bg-color-input', 'color'),
)
def avatar_bg_color_demo(color):
    return [{'background': color}] * 2
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAvatar(),
        fac.AntdAvatar(mode='text', text='F'),
        fac.AntdAvatar(
            mode='image',
            src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
        ),
    ]
)
```

### responsive_sizes

- 说明：演示 responsive_sizes 的用法。

#### 代码
```python
fac.AntdAvatar(
    mode='image',
    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    size={'xs': 24, 'sm': 28, 'md': 32, 'lg': 36, 'xl': 40, 'xxl': 45},
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAvatar(size='small'),
        fac.AntdAvatar(),
        fac.AntdAvatar(size='large'),
        fac.AntdAvatar(size=64),
    ],
    align='center',
)
```

### square_shape

- 说明：演示 square_shape 的用法。

#### 代码
```python
fac.AntdAvatar(
    mode='image',
    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    size='large',
    shape='square',
)
```

### use_with_AntdBadge

- 说明：演示 use_with_AntdBadge 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
    ],
    size=20,
)
```

### use_with_AntdIcon

- 说明：演示 use_with_AntdIcon 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdAvatar(icon=icon, style={'background': '#4551f5'})
        for icon in [
            'antd-user',
            'antd-team',
            'antd-github',
            'antd-fire',
            'antd-thunderbolt',
            'antd-robot',
        ]
    ],
    wrap=True,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- mode (a value equal to: 'text', 'icon', 'image'; default 'icon'):
    头像模式，可选项有`'text'`、`'icon'`、`'image'`  默认值：`'icon'`.

- gap (number; default 4):
    `mode='text'`时，设置字符距离左右两侧边界的像素距离  默认值：`4`.

- text (string; optional):
    `mode='text'`时，设置文字内容.

- icon (string; optional):
    `mode='icon'`时，设置图标，同**AntdIcon**的`icon`参数.

- iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; default 'AntdIcon'):
    `mode='icon'`时，设置图标渲染方式，可选项有`'AntdIcon'`、`'fontawesome'`.

- alt (string; optional):
    `mode='image'`时，设置图像无法显示时的占位文字.

- src (string; optional):
    `mode='image'`时，设置图片地址.

- srcSet (string; optional):
    `mode='image'`时，设置图片base64地址.

- draggable (boolean | a value equal to: 'true', 'false'; optional):
    `mode='image'`时，设置图片是否允许拖拽.

- crossOrigin (a value equal to: 'anonymous', 'use-credentials', ''; optional):
    `mode='image'`时，设置图片的CORS属性，可选项有`'anonymous'`、`'use-credentials'`、`''`.

- size (dict; optional):
    配置头像尺寸，可传入数值型代表像素尺寸（支持响应式），或传入字符型使用预设尺寸规格，可选项有`'large'`、`'small'`、`'default'`.

    `size` is a number | a value equal to: 'large', 'small', 'default'
    | dict with keys:

    - xs (number; optional)

    - sm (number; optional)

    - md (number; optional)

    - lg (number; optional)

    - xl (number; optional)

    - xxl (number; optional)

- shape (a value equal to: 'circle', 'square'; default 'circle'):
    头像形状，可选项有`'circle'`、`'square'`  默认值：`'circle'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
