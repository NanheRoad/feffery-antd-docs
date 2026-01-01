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
