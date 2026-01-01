# AntdCountup

## 简介源码：`views/AntdCountup/intro.py`
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
                {'title': 'AntdCountup 正计时'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCountup 正计时', level=2),
        fac.AntdParagraph('用于渲染实时刷新的正计时信息卡片。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

...

fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCountup(
                title='Countup',
                value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountup(
                title='Million Seconds',
                value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
                format='HH:mm:ss:SSS',
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountup(
                title='Day Level',
                value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
                format='D 天 H 时 m 分 s 秒',
            ),
            span=24,
        ),
    ],
    gutter=16,
)
```

### title_tooltip

- 说明：演示 title_tooltip 的用法。

#### 代码
```python
start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

...

fac.AntdCountup(
    title='Countup',
    titleTooltip='这是信息提示示例',
    value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
)
```

### unit

- 说明：演示 unit 的用法。

#### 代码
```python
start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

...

fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCountup(
                title='Countup',
                value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
                prefix=fac.AntdIcon(icon='antd-history'),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountup(
                title='Countup',
                value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
                suffix=fac.AntdIcon(icon='antd-bell'),
            ),
            span=12,
        ),
    ],
    gutter=16,
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- format (string; optional):
    日期时间显示格式，[参考资料](https://day.js.org/docs/en/display/format)，如`HH:mm:ss`代表`时:分:秒`.

- value (string; optional):
    目标截止日期时间字符串，与`valueFormat`对应.

- valueFormat (string; default 'YYYY-MM-DD hh:mm:ss'):
    针对`value`设置对应的日期时间解析格式，[参考资料](https://day.js.org/docs/en/display/format)
    默认值：`'YYYY-MM-DD hh:mm:ss'`.

- prefix (a list of or a singular dash component, string or number; optional):
    组件型，数值前缀内容.

- suffix (a list of or a singular dash component, string or number; optional):
    组件型，数值后缀内容.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- titleTooltip (string; optional):
    为标题内容添加额外鼠标悬停提示信息.

- valueStyle (dict; optional):
    数值内容css样式.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
