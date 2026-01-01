# AntdResult

## 简介源码：`views/AntdResult/intro.py`
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
                {'title': 'AntdResult 结果'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdResult 结果', level=2),
        fac.AntdParagraph('用于为用户提供不同场景下的状态提示。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdResult(title='标题示例', subTitle='副标题示例')
```

### complex_usage

- 说明：演示 complex_usage 的用法。

#### 代码
```python
fac.AntdResult(
    status='success',
    title='任务创建成功',
    subTitle=fac.AntdSpace(
        [
            fac.AntdText('创建时间：2023-01-01 12:00:00', type='secondary'),
            fac.AntdSpace(
                [
                    fac.AntdButton('查看详情', type='primary'),
                    fac.AntdButton('回到首页'),
                ]
            ),
        ],
        direction='vertical',
        align='center',
    ),
)
```

### custom_icon

- 说明：演示 custom_icon 的用法。

#### 代码
```python
fac.AntdResult(
    title='标题示例',
    subTitle='副标题示例',
    icon=fac.AntdIcon(
        icon='antd-bulb', style={'fontSize': 60, 'color': '#fcd53f'}
    ),
)
```

### extra

- 说明：演示 extra 的用法。

#### 代码
```python
fac.AntdResult(
    title='标题示例',
    subTitle='副标题示例',
    extra=fac.AntdButton('额外内容', type='primary'),
)
```

### status_usage

- 说明：演示 status_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdResult(
            title='标题示例', subTitle=f'status="{status}"', status=status
        )
        for status in [
            'info',
            'success',
            'warning',
            'error',
            '404',
            '403',
            '500',
            'loading',
        ]
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- extra (a list of or a singular dash component, string or number; optional):
    组件型，操作区域.

- status (a value equal to: 'success', 'error', 'info', 'warning', '404', '403', '500', 'loading'; default 'info'):
    状态，可选项有`'success'`、`'error'`、`'info'`、`'warning'`、`'404'`、`'403'`、`'500'`
    默认值：`'info'`.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- subTitle (a list of or a singular dash component, string or number; optional):
    组件型，副标题内容.

- icon (a list of or a singular dash component, string or number; optional):
    组件型，图标内容.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
