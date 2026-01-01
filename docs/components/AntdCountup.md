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

## 示例源码（demos）

### `views/AntdCountup/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component
from datetime import datetime, timedelta


def render() -> Component:
    """渲染当前演示用例"""

    start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

    # 构造演示用例相关内容
    demo_contents = fac.AntdRow(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdCountup/demos/title_tooltip.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component
from datetime import datetime, timedelta


def render() -> Component:
    """渲染当前演示用例"""

    start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

    # 构造演示用例相关内容
    demo_contents = fac.AntdCountup(
        title='Countup',
        titleTooltip='这是信息提示示例',
        value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
    )

    return demo_contents


code_string = [
    {
        'code': """
start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

...

fac.AntdCountup(
    title='Countup',
    titleTooltip='这是信息提示示例',
    value=start_time.strftime('%Y-%m-%d %H:%M:%S:%f'),
)
"""
    }
]

```

### `views/AntdCountup/demos/unit.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component
from datetime import datetime, timedelta


def render() -> Component:
    """渲染当前演示用例"""

    start_time = datetime.now() - timedelta(seconds=2 * 24 * 60 * 60 + 30)

    # 构造演示用例相关内容
    demo_contents = fac.AntdRow(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```
