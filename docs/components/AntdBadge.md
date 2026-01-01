# AntdBadge

## 简介源码：`views/AntdBadge/intro.py`
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
                {'title': 'AntdBadge 徽标数'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdBadge 徽标数', level=2),
        fac.AntdParagraph(
            '一般出现在通知图标或头像的右上角，用于显示需要处理的消息条数，通过醒目视觉形式吸引用户处理。'
        ),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

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
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            dot=True,
            offset=[-8, 6],
        ),
    ],
    size=20,
    wrap=True,
)
```

### color

- 说明：演示 color 的用法。

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
            color='#1890ff',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
            color='#1890ff',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
            color='#1890ff',
        ),
    ],
    wrap=True,
    size=20,
)
```

### dynamic_number_change

- 说明：演示 dynamic_number_change 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '计数随机递增', id='badge-demo-generate', type='primary'
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            id='badge-demo-1',
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            id='badge-demo-2',
            count=0,
            dot=True,
        ),
    ],
    size=20,
)

...

@app.callback(
    [Output('badge-demo-1', 'count'), Output('badge-demo-2', 'count')],
    Input('badge-demo-generate', 'nClicks'),
    [State('badge-demo-1', 'count'), State('badge-demo-2', 'count')],
    prevent_initial_call=True,
)
def badge_callback_demo(nClicks, count1, count2):
    return count1 + random.randint(1, 10), count2 + random.randint(1, 10)
```

### just_badge

- 说明：演示 just_badge 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdBadge(count=8),
        fac.AntdBadge(count=101),
        fac.AntdBadge(count=101, size='small'),
        fac.AntdBadge(dot=True, status='success'),
        fac.AntdBadge(dot=True, status='error'),
        fac.AntdBadge(dot=True, status='default'),
        fac.AntdBadge(dot=True, status='processing'),
        fac.AntdBadge(dot=True, status='warning'),
    ],
    size=20,
)
```

### sizes

- 说明：演示 sizes 的用法。

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
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=6,
            size='small',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
            size='small',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
            size='small',
        ),
    ],
    wrap=True,
    size=20,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，定义徽标添加目标元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        控制根元素css样式.

    - indicator (dict; optional):
        控制徽标元素css样式.

- classNames (dict; optional):
    细分控制子元素css类.

    `classNames` is a dict with keys:

    - root (string; optional):
        控制根元素css类.

    - indicator (string; optional):
        控制徽标元素css类.

- color (string; optional):
    徽标颜色.

- count (number; optional):
    徽标显示的数字.

- dot (boolean; default False):
    是否用圆点代替数字显示  默认值：`False`.

- showZero (boolean; default False):
    当`count=0`时，是否强制显示数字  默认值：`False`.

- overflowCount (number; default 99):
    数字显示上限，超出会以显示`+`后缀  默认值：`99`.

- offset (list of numbers; optional):
    徽标在水平、竖直方向上的像素偏移，格式为`[水平偏移, 竖直偏移]`.

- status (a value equal to: 'success', 'processing', 'default', 'error', 'warning'; optional):
    徽标状态，可选项有`'success'`、`'processing'`、`'default'`、`'error'`、`'warning'`.

- text (string; optional):
    参数`status`有效时，设置徽标文本内容.

- title (string; optional):
    徽标鼠标悬停显示文字内容.

- size (a value equal to: 'default', 'small'; default 'default'):
    徽标尺寸规格，可选项有`'default'`、`'small'`.

- nClicks (number; default 0):
    监听徽标累计被点击次数  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
