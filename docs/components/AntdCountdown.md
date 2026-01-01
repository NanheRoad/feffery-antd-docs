# AntdCountdown

## 简介源码：`views/AntdCountdown/intro.py`
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
                {'title': 'AntdCountdown 倒计时'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdCountdown 倒计时', level=2),
        fac.AntdParagraph('用于渲染实时刷新的倒计时信息卡片。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '创建新的倒计时', id='countdown-create-new', type='primary'
        ),
        fac.Fragment(id='countdown-new-demo-container'),
    ],
    direction='vertical',
    style={'width': '100%'},
)

...

@app.callback(
    Output('countdown-new-demo-container', 'children'),
    Input('countdown-create-new', 'nClicks'),
    prevent_initial_call=True,
)
def create_new_countdown(nClicks):
    return fac.AntdSpace(
        [
            fac.AntdCountdown(
                id='countdown-new-demo',
                title='Countdown',
                value=(datetime.now() + timedelta(seconds=5)).strftime(
                    '%Y-%m-%d %H:%M:%S:%f'
                ),
            ),
            fac.AntdText(id='countdown-new-demo-finish-event'),
        ],
        direction='vertical',
        style={'width': '100%'},
    )


@app.callback(
    Output('countdown-new-demo-finish-event', 'children'),
    Input('countdown-new-demo', 'finishEvent'),
    prevent_initial_call=True,
)
def show_countdown_finish_event(finishEvent):
    return json.dumps(
        {'finishEvent': finishEvent}, ensure_ascii=False, indent=4
    )
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
deadline = datetime.now() + timedelta(seconds=2 * 24 * 60 * 60 + 30)

fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCountdown(
                title='Countdown',
                value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountdown(
                title='Million Seconds',
                value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
                format='HH:mm:ss:SSS',
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountdown(
                title='Day Level',
                value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
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
deadline = datetime.now() + timedelta(seconds=2 * 24 * 60 * 60 + 30)

fac.AntdCountdown(
    title='Countdown',
    value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
    titleTooltip='这是信息提示示例',
)
```

### unit

- 说明：演示 unit 的用法。

#### 代码
```python
deadline = datetime.now() + timedelta(seconds=2 * 24 * 60 * 60 + 30)

fac.AntdRow(
    [
        fac.AntdCol(
            fac.AntdCountdown(
                title='Countdown',
                value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
                prefix=fac.AntdIcon(icon='antd-history'),
            ),
            span=12,
        ),
        fac.AntdCol(
            fac.AntdCountdown(
                title='Countdown',
                value=deadline.strftime('%Y-%m-%d %H:%M:%S:%f'),
                suffix=fac.AntdIcon(icon='antd-bell'),
            ),
            span=12,
        ),
    ],
    gutter=16,
)
```
