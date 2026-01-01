# AntdDatePicker

## 简介源码：`views/AntdDatePicker/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {"title": translator.t("组件介绍")},
                {"title": translator.t("数据录入")},
                {"title": translator.t("AntdDatePicker 日期选择")},
            ],
            style={"marginBottom": 8},
        ),
        fac.AntdTitle(translator.t("AntdDatePicker 日期选择"), level=2),
        fac.AntdParagraph(translator.t("提供常见的日期选择相关功能。")),
    ]

```

## 示例源码（demos）

### `views/AntdDatePicker/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo1",
                            style={"width": 175},
                        ),
                        fac.AntdText(id="date-picker-demo1-output"),
                    ],
                    align="center",
                ),
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo2",
                            placeholder="请选择日期时间",
                            style={"width": 175},
                            showTime=True,
                        ),
                        fac.AntdText(id="date-picker-demo2-output"),
                    ],
                    align="center",
                ),
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo3",
                            placeholder="配合自定义format",
                            format="YYYY年MM月DD日",
                            style={"width": 175},
                        ),
                        fac.AntdText(id="date-picker-demo3-output"),
                    ],
                    align="center",
                ),
            ],
            direction="vertical",
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo1", style={"width": 175}, locale="en-us"
                        ),
                        fac.AntdText(id="date-picker-demo1-output"),
                    ],
                    align="center",
                ),
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo2",
                            placeholder="Please select date & time",
                            style={"width": 175},
                            showTime=True,
                            locale="en-us",
                        ),
                        fac.AntdText(id="date-picker-demo2-output"),
                    ],
                    align="center",
                ),
                fac.AntdSpace(
                    [
                        fac.AntdDatePicker(
                            id="date-picker-demo3",
                            placeholder="With custom format",
                            format="YYYY-MM-DD",
                            style={"width": 175},
                            locale="en-us",
                        ),
                        fac.AntdText(id="date-picker-demo3-output"),
                    ],
                    align="center",
                ),
            ],
            direction="vertical",
        )

    return demo_contents


@app.callback(
    Output("date-picker-demo1-output", "children"),
    Input("date-picker-demo1", "value"),
)
def date_picker_demo1(value):
    return f"value: {value}"


@app.callback(
    Output("date-picker-demo2-output", "children"),
    Input("date-picker-demo2", "value"),
)
def date_picker_demo2(value):
    return f"value: {value}"


@app.callback(
    Output("date-picker-demo3-output", "children"),
    Input("date-picker-demo3", "value"),
)
def date_picker_demo3(value):
    return f"value: {value}"


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo1',
                    style={'width': 175},
                ),
                fac.AntdText(id='date-picker-demo1-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo2',
                    placeholder='请选择日期时间',
                    style={'width': 175},
                    showTime=True,
                ),
                fac.AntdText(id='date-picker-demo2-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo3',
                    placeholder='配合自定义format',
                    format='YYYY年MM月DD日',
                    style={'width': 175},
                ),
                fac.AntdText(id='date-picker-demo3-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('date-picker-demo1-output', 'children'),
    Input('date-picker-demo1', 'value'),
)
def date_picker_demo1(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo2-output', 'children'),
    Input('date-picker-demo2', 'value'),
)
def date_picker_demo2(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo3-output', 'children'),
    Input('date-picker-demo3', 'value'),
)
def date_picker_demo3(value):
    return f'value: {value}'
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo1',
                    style={'width': 175},
                    locale="en-us"
                ),
                fac.AntdText(id='date-picker-demo1-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo2',
                    placeholder='Please select date & time',
                    style={'width': 175},
                    showTime=True,
                    locale="en-us"
                ),
                fac.AntdText(id='date-picker-demo2-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id='date-picker-demo3',
                    placeholder='With custom format',
                    format='YYYY-MM-DD',
                    style={'width': 175},
                    locale="en-us"
                ),
                fac.AntdText(id='date-picker-demo3-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('date-picker-demo1-output', 'children'),
    Input('date-picker-demo1', 'value'),
)
def date_picker_demo1(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo2-output', 'children'),
    Input('date-picker-demo2', 'value'),
)
def date_picker_demo2(value):
    return f'value: {value}'


@app.callback(
    Output('date-picker-demo3-output', 'children'),
    Input('date-picker-demo3', 'value'),
)
def date_picker_demo3(value):
    return f'value: {value}'
"""
            }
        ]

```

### `views/AntdDatePicker/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(),
                fac.AntdDatePicker(placeholder="请选择日期时间", showTime=True),
            ],
            wrap=True,
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(locale="en-us"),
                fac.AntdDatePicker(
                    placeholder="Please select date & time",
                    showTime=True,
                    locale="en-us",
                ),
            ],
            wrap=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(),
        fac.AntdDatePicker(placeholder='请选择日期时间', showTime=True),
    ],
    wrap=True,
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(locale="en-us"),
        fac.AntdDatePicker(placeholder='Please select date & time', showTime=True, locale="en-us"),
    ],
    wrap=True,
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/custom_cells.py`
```python
from datetime import datetime, timedelta

import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                "精确日期匹配：明天",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "year": datetime.now().year,
                            "month": datetime.now().month,
                            "date": (datetime.now() + timedelta(days=1)).day,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ]
                ),
                "年份通配：每年的本月第10天",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "month": datetime.now().month,
                            "date": 10,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ]
                ),
                "年份+月份通配：每月的第10天",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "date": 10,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ]
                ),
            ],
            direction="vertical",
            style={"width": "100%"},
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                "Exact date match: tomorrow",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "year": datetime.now().year,
                            "month": datetime.now().month,
                            "date": (datetime.now() + timedelta(days=1)).day,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ],
                    locale="en-us",
                ),
                "Year wildcard: the 10th day of this month each year",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "month": datetime.now().month,
                            "date": 10,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ],
                    locale="en-us",
                ),
                "Year+month wildcard: the 10th day of each month",
                fac.AntdDatePicker(
                    customCells=[
                        {
                            "date": 10,
                            "style": {"border": "1px dashed #595959"},
                        }
                    ],
                    locale="en-us",
                ),
            ],
            direction="vertical",
            style={"width": "100%"},
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        '精确日期匹配：明天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'year': datetime.now().year,
                    'month': datetime.now().month,
                    'date': (datetime.now() + timedelta(days=1)).day,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
        '年份通配：每年的本月第10天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'month': datetime.now().month,
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
        '年份+月份通配：每月的第10天',
        fac.AntdDatePicker(
            customCells=[
                {
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ]
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        'Exact date match: tomorrow',
        fac.AntdDatePicker(
            customCells=[
                {
                    'year': datetime.now().year,
                    'month': datetime.now().month,
                    'date': (datetime.now() + timedelta(days=1)).day,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ],
            locale="en-us"
        ),
        'Year wildcard: the 10th day of this month each year',
        fac.AntdDatePicker(
            customCells=[
                {
                    'month': datetime.now().month,
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ],
            locale="en-us"
        ),
        'Year+month wildcard: the 10th day of each month',
        fac.AntdDatePicker(
            customCells=[
                {
                    'date': 10,
                    'style': {
                        'border': '1px dashed #595959',
                    },
                }
            ],
            locale="en-us"
        ),
    ],
    direction='vertical',
    style={'width': '100%'},
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/custom_format.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    placeholder='picker="date"',
                    format="YYYY年MM月DD日",
                    style={"width": 175},
                ),
                fac.AntdDatePicker(
                    placeholder='picker="week"',
                    picker="week",
                    format="YYYY年第w周",
                    style={"width": 175},
                ),
                fac.AntdDatePicker(
                    placeholder='picker="month"',
                    picker="month",
                    format="YYYY-MM",
                    style={"width": 175},
                ),
                fac.AntdDatePicker(
                    placeholder='picker="year"',
                    picker="year",
                    format="YYYY年",
                    style={"width": 175},
                ),
            ],
            direction="vertical",
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    placeholder='picker="date"',
                    format="YYYY-MM-DD",
                    style={"width": 175},
                    locale="en-us",
                ),
                fac.AntdDatePicker(
                    placeholder='picker="week"',
                    picker="week",
                    format="YYYY [Week] w",
                    style={"width": 175},
                    locale="en-us",
                ),
                fac.AntdDatePicker(
                    placeholder='picker="month"',
                    picker="month",
                    format="YYYY-MM",
                    style={"width": 175},
                    locale="en-us",
                ),
                fac.AntdDatePicker(
                    placeholder='picker="year"',
                    picker="year",
                    format="YYYY",
                    style={"width": 175},
                    locale="en-us",
                ),
            ],
            direction="vertical",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placeholder='picker="date"',
            format='YYYY年MM月DD日',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="week"',
            picker='week',
            format='YYYY年第w周',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="month"',
            picker='month',
            format='YYYY-MM',
            style={'width': 175},
        ),
        fac.AntdDatePicker(
            placeholder='picker="year"',
            picker='year',
            format='YYYY年',
            style={'width': 175},
        ),
    ],
    direction='vertical',
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placeholder='picker="date"',
            format='YYYY-MM-DD',
            style={'width': 175},
            locale="en-us"
        ),
        fac.AntdDatePicker(
            placeholder='picker="week"',
            picker='week',
            format='YYYY [Week] w',
            style={'width': 175},
            locale="en-us"
        ),
        fac.AntdDatePicker(
            placeholder='picker="month"',
            picker='month',
            format='YYYY-MM',
            style={'width': 175},
            locale="en-us"
        ),
        fac.AntdDatePicker(
            placeholder='picker="year"',
            picker='year',
            format='YYYY',
            style={'width': 175},
            locale="en-us"
        ),
    ],
    direction='vertical',
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/different_picker.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    demo_contents = fac.AntdSpace(
        [
            fac.AntdDatePicker(picker=picker, placeholder=f'picker="{picker}"')
            for picker in ["date", "week", "month", "quarter", "year"]
        ],
        direction="vertical",
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    return [
        {
            "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(picker=picker, placeholder=f'picker="{picker}"')
        for picker in ['date', 'week', 'month', 'quarter', 'year']
    ],
    direction='vertical',
)
"""
        }
    ]

```

### `views/AntdDatePicker/demos/different_placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    demo_contents = fac.AntdSpace(
        [
            fac.AntdDatePicker(
                placement=placement, placeholder=f'placement="{placement}"'
            )
            for placement in [
                "bottomLeft",
                "bottomRight",
                "topLeft",
                "topRight",
            ]
        ],
        direction="vertical",
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    return [
        {
            "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placement=placement, placeholder=f'placement="{placement}"'
        )
        for placement in [
            'bottomLeft',
            'bottomRight',
            'topLeft',
            'topRight',
        ]
    ],
    direction='vertical',
)
"""
        }
    ]

```

### `views/AntdDatePicker/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(disabled=True)
    else:
        demo_contents = fac.AntdDatePicker(disabled=True, locale="en-us")

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    return [
        {
            "code": """
fac.AntdDatePicker(disabled=True)
"""
        }
    ]

```

### `views/AntdDatePicker/demos/disabled_dates.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = [
            fac.AntdDivider("mode='eq'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "eq", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='ne'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月非6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "ne", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='le'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月小于等于6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "le", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='lt'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月小于6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "lt", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='ge'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月大于等于6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "ge", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='gt'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月大于6号",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "gt", "target": "day", "value": 6}],
            ),
            fac.AntdDivider("mode='in'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用每月的5号到25号",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "in", "target": "day", "value": list(range(5, 26))}
                ],
            ),
            fac.AntdDivider("mode='not-in'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用非每月的5号到25号",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "not-in", "target": "day", "value": list(range(5, 26))}
                ],
            ),
            fac.AntdDivider("mode='in-enumerate-dates'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用枚举列表中的日期",
                style={"width": 200},
                disabledDatesStrategy=[
                    {
                        "mode": "in-enumerate-dates",
                        "value": [f"2023-01-0{i}" for i in range(1, 10)],
                    }
                ],
                pickerValue="2023-01-01",
            ),
            fac.AntdDivider(
                "mode='not-in-enumerate-dates'", innerTextOrientation="left"
            ),
            fac.AntdDatePicker(
                placeholder="禁用非枚举列表中的日期",
                style={"width": 200},
                disabledDatesStrategy=[
                    {
                        "mode": "not-in-enumerate-dates",
                        "value": [f"2023-01-0{i}" for i in range(1, 10)],
                    }
                ],
                pickerValue="2023-01-01",
            ),
            fac.AntdDivider("target='specific-date'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="禁用指定日期之前的日期",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "lt", "target": "specific-date", "value": "2023-01-15"}
                ],
                pickerValue="2023-01-01",
            ),
        ]
    else:  # en-us
        demo_contents = [
            fac.AntdDivider("mode='eq'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable the 6th of each month",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "eq", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='ne'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable all days except the 6th",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "ne", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='le'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable days ≤ 6th each month",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "le", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='lt'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable days < 6th each month",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "lt", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='ge'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable days ≥ 6th each month",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "ge", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='gt'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable days > 6th each month",
                style={"width": 200},
                disabledDatesStrategy=[{"mode": "gt", "target": "day", "value": 6}],
                locale="en-us",
            ),
            fac.AntdDivider("mode='in'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable the 5th–25th each month",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "in", "target": "day", "value": list(range(5, 26))}
                ],
                locale="en-us",
            ),
            fac.AntdDivider("mode='not-in'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable dates not between the 5th and 25th",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "not-in", "target": "day", "value": list(range(5, 26))}
                ],
                locale="en-us",
            ),
            fac.AntdDivider("mode='in-enumerate-dates'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable dates in the enumeration list",
                style={"width": 200},
                disabledDatesStrategy=[
                    {
                        "mode": "in-enumerate-dates",
                        "value": [f"2023-01-0{i}" for i in range(1, 10)],
                    }
                ],
                pickerValue="2023-01-01",
                locale="en-us",
            ),
            fac.AntdDivider(
                "mode='not-in-enumerate-dates'", innerTextOrientation="left"
            ),
            fac.AntdDatePicker(
                placeholder="Disable dates not in the enumeration list",
                style={"width": 200},
                disabledDatesStrategy=[
                    {
                        "mode": "not-in-enumerate-dates",
                        "value": [f"2023-01-0{i}" for i in range(1, 10)],
                    }
                ],
                pickerValue="2023-01-01",
                locale="en-us",
            ),
            fac.AntdDivider("target='specific-date'", innerTextOrientation="left"),
            fac.AntdDatePicker(
                placeholder="Disable dates before the specified date",
                style={"width": 200},
                disabledDatesStrategy=[
                    {"mode": "lt", "target": "specific-date", "value": "2023-01-15"}
                ],
                pickerValue="2023-01-01",
                locale="en-us",
            ),
        ]

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
[
    fac.AntdDivider("mode='eq'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'eq', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ne'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月非6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ne', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='le'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月小于等于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'le', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='lt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月小于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'lt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ge'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月大于等于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ge', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='gt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月大于6号',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'gt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用每月的5号到25号',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='not-in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用非每月的5号到25号',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'not-in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用枚举列表中的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("mode='not-in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用非枚举列表中的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'not-in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("target='specific-date'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='禁用指定日期之前的日期',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'lt', 'target': 'specific-date', 'value': '2023-01-15'}
        ],
        pickerValue='2023-01-01',
    ),
]
"""
            }
        ]
    else:
        return [
            {
                "code": """
[
    fac.AntdDivider("mode='eq'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable the 6th of each month',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'eq', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='ne'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable all days except the 6th',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ne', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='le'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable days ≤ 6th each month',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'le', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='lt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable days < 6th each month',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'lt', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='ge'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable days ≥ 6th each month',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'ge', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='gt'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable days > 6th each month',
        style={'width': 200},
        disabledDatesStrategy=[{'mode': 'gt', 'target': 'day', 'value': 6}],
        locale="en-us"
    ),
    fac.AntdDivider("mode='in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable the 5th-25th each month',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'in', 'target': 'day', 'value': list(range(5, 26))}
        ],
        locale="en-us"
    ),
    fac.AntdDivider("mode='not-in'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable dates not between the 5th and 25th',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'not-in', 'target': 'day', 'value': list(range(5, 26))}
        ],
        locale="en-us"
    ),
    fac.AntdDivider("mode='in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable dates in the enumeration list',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
        locale="en-us"
    ),
    fac.AntdDivider("mode='not-in-enumerate-dates'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable dates not in the enumeration list',
        style={'width': 200},
        disabledDatesStrategy=[
            {
                'mode': 'not-in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
        locale="en-us"
    ),
    fac.AntdDivider("target='specific-date'", innerTextOrientation='left'),
    fac.AntdDatePicker(
        placeholder='Disable dates before the specified date',
        style={'width': 200},
        disabledDatesStrategy=[
            {'mode': 'lt', 'target': 'specific-date', 'value': '2023-01-15'}
        ],
        pickerValue='2023-01-01',
        locale="en-us"
    ),
]
"""
            }
        ]

```

### `views/AntdDatePicker/demos/dynamic_disabled_dates.py`
```python
from datetime import datetime, timedelta

import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(id="date-picker-dynamic-forbidden-demo")
    else:
        demo_contents = fac.AntdDatePicker(
            id="date-picker-dynamic-forbidden-demo", locale="en-us"
        )

    return demo_contents


@app.callback(
    Output("date-picker-dynamic-forbidden-demo", "disabledDatesStrategy"),
    Input("date-picker-dynamic-forbidden-demo", "id"),
)
def date_picker_dynamic_forbidden_demo(_):
    return [
        {
            "mode": "lt",
            "target": "specific-date",
            "value": datetime.now().strftime("%Y-%m-%d"),
        },
        {
            "mode": "gt",
            "target": "specific-date",
            "value": (datetime.now() + timedelta(days=7)).strftime("%Y-%m-%d"),
        },
    ]


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    return [
        {
            "code": """
from datetime import datetime, timedelta

...

fac.AntdDatePicker(id='date-picker-dynamic-forbidden-demo')

...

@app.callback(
    Output('date-picker-dynamic-forbidden-demo', 'disabledDatesStrategy'),
    Input('date-picker-dynamic-forbidden-demo', 'id'),
)
def date_picker_dynamic_forbidden_demo(_):

    return [
        {
            'mode': 'lt',
            'target': 'specific-date',
            'value': datetime.now().strftime('%Y-%m-%d'),
        },
        {
            'mode': 'gt',
            'target': 'specific-date',
            'value': (datetime.now() + timedelta(days=7)).strftime('%Y-%m-%d'),
        },
    ]
"""
        }
    ]

```

### `views/AntdDatePicker/demos/extra_footer.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(extraFooter=fac.AntdText("底部额外内容示例")),
                fac.AntdDatePicker(
                    placeholder="请选择日期时间",
                    showTime=True,
                    extraFooter=fac.AntdText("底部额外内容示例"),
                ),
            ],
            wrap=True,
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    extraFooter=fac.AntdText("Example of extra footer content"),
                    locale="en-us",
                ),
                fac.AntdDatePicker(
                    placeholder="Please select date & time",
                    showTime=True,
                    extraFooter=fac.AntdText("Example of extra footer content"),
                    locale="en-us",
                ),
            ],
            wrap=True,
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""

    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(extraFooter=fac.AntdText('底部额外内容示例')),
        fac.AntdDatePicker(
            placeholder='请选择日期时间',
            showTime=True,
            extraFooter=fac.AntdText('底部额外内容示例'),
        ),
    ],
    wrap=True,
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(extraFooter=fac.AntdText('Example of extra footer content'), locale="en-us"),
        fac.AntdDatePicker(
            placeholder='Please select date & time',
            showTime=True,
            extraFooter=fac.AntdText('Example of extra footer content'),
            locale="en-us"
        ),
    ],
    wrap=True,
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/hide_today.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(showToday=False)
    else:
        demo_contents = fac.AntdDatePicker(showToday=False, locale="en-us")

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdDatePicker(showToday=False)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdDatePicker(showToday=False, locale='en-us')
"""
            }
        ]

```

### `views/AntdDatePicker/demos/listen_picker_value.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from i18n import get_current_locale
from server import app


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id="date-picker-listen-picker-value-demo",
                    style={"width": 175},
                ),
                fac.AntdText(id="date-picker-listen-picker-value-demo-output"),
            ]
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    id="date-picker-listen-picker-value-demo",
                    style={"width": 175},
                    locale="en-us",
                ),
                fac.AntdText(id="date-picker-listen-picker-value-demo-output"),
            ]
        )

    return demo_contents


@app.callback(
    Output("date-picker-listen-picker-value-demo-output", "children"),
    Input("date-picker-listen-picker-value-demo", "pickerValue"),
)
def show_picker_value(pickerValue):
    return f"pickerValue: {pickerValue}"


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            id='date-picker-listen-picker-value-demo',
            style={'width': 175},
        ),
        fac.AntdText(id='date-picker-listen-picker-value-demo-output'),
    ]
)

...

@app.callback(
    Output('date-picker-listen-picker-value-demo-output', 'children'),
    Input('date-picker-listen-picker-value-demo', 'pickerValue'),
)
def show_picker_value(pickerValue):
    return f'pickerValue: {pickerValue}'
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            id='date-picker-listen-picker-value-demo',
            style={'width': 175},
            locale='en-us',
        ),
        fac.AntdText(id='date-picker-listen-picker-value-demo-output'),
    ]
)

...

@app.callback(
    Output('date-picker-listen-picker-value-demo-output', 'children'),
    Input('date-picker-listen-picker-value-demo', 'pickerValue'),
)
def show_picker_value(pickerValue):
    return f'pickerValue: {pickerValue}'
"""
            }
        ]

```

### `views/AntdDatePicker/demos/picker_value.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(pickerValue="1999-12-31", style={"width": 175}),
                fac.AntdDatePicker(
                    placeholder="配合自定义format",
                    pickerValue="1999年12月31日",
                    format="YYYY年MM月DD日",
                    style={"width": 175},
                ),
            ],
            direction="vertical",
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    pickerValue="1999-12-31", style={"width": 175}, locale="en-us"
                ),
                fac.AntdDatePicker(
                    placeholder="With custom format",
                    pickerValue="1999-12-31",
                    format="YYYY-MM-DD",
                    style={"width": 175},
                    locale="en-us",
                ),
            ],
            direction="vertical",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            pickerValue='1999-12-31', style={'width': 175}
        ),
        fac.AntdDatePicker(
            placeholder='配合自定义format',
            pickerValue='1999年12月31日',
            format='YYYY年MM月DD日',
            style={'width': 175},
        ),
    ],
    direction='vertical',
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            pickerValue='1999-12-31', style={'width': 175}, locale='en-us'
        ),
        fac.AntdDatePicker(
            placeholder='With custom format',
            pickerValue='1999-12-31',
            format='YYYY-MM-DD',
            style={'width': 175},
            locale='en-us',
        ),
    ],
    direction='vertical',
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/prefix.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(
            value="2024-01-01", prefix=fac.AntdIcon(icon="antd-user")
        )
    else:
        demo_contents = fac.AntdDatePicker(
            value="2024-01-01",
            prefix=fac.AntdIcon(icon="antd-user"),
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdDatePicker(
    value='2024-01-01', prefix=fac.AntdIcon(icon='antd-user')
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdDatePicker(
    value='2024-01-01',
    prefix=fac.AntdIcon(icon='antd-user'),
    locale='en-us',
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/read_only.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(value="2024-01-01", readOnly=True)
    else:
        demo_contents = fac.AntdDatePicker(
            value="2024-01-01", readOnly=True, locale="en-us"
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdDatePicker(value='2024-01-01', readOnly=True)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdDatePicker(value='2024-01-01', readOnly=True, locale='en-us')
"""
            }
        ]

```

### `views/AntdDatePicker/demos/render_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(placeholder=f'status="{status}"', status=status)
                for status in ["warning", "error"]
            ],
            direction="vertical",
        )
    else:
        demo_contents = fac.AntdSpace(
            [
                fac.AntdDatePicker(
                    placeholder=f'status="{status}"', status=status, locale="en-us"
                )
                for status in ["warning", "error"]
            ],
            direction="vertical",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(placeholder=f'status="{status}"', status=status)
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdSpace(
    [
        fac.AntdDatePicker(
            placeholder=f'status="{status}"', status=status, locale='en-us'
        )
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/suffix_icon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(
            value="2024-01-01", suffixIcon=fac.AntdIcon(icon="antd-user")
        )
    else:
        demo_contents = fac.AntdDatePicker(
            value="2024-01-01",
            suffixIcon=fac.AntdIcon(icon="antd-user"),
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdDatePicker(
    value='2024-01-01', suffixIcon=fac.AntdIcon(icon='antd-user')
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdDatePicker(
    value='2024-01-01',
    suffixIcon=fac.AntdIcon(icon='antd-user'),
    locale='en-us',
)
"""
            }
        ]

```

### `views/AntdDatePicker/demos/time_default_value.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import get_current_locale


def render() -> Component:
    """渲染当前演示用例 / Render the current demo"""

    locale = get_current_locale()

    if locale == "zh-cn":
        demo_contents = fac.AntdDatePicker(
            placeholder="请选择日期时间", showTime={"defaultValue": "18:33:33"}
        )
    else:
        demo_contents = fac.AntdDatePicker(
            placeholder="Please select date & time",
            showTime={"defaultValue": "18:33:33"},
            locale="en-us",
        )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码 / Return demo code for the current locale"""
    locale = get_current_locale()

    if locale == "zh-cn":
        return [
            {
                "code": """
fac.AntdDatePicker(
    placeholder='请选择日期时间', showTime={'defaultValue': '18:33:33'}
)
"""
            }
        ]
    else:
        return [
            {
                "code": """
fac.AntdDatePicker(
    placeholder='Please select date & time',
    showTime={'defaultValue': '18:33:33'},
    locale='en-us',
)
"""
            }
        ]

```

## API 文档

- id (string; optional):  
   Unique component id.

- key (string; optional):  
   Update the `key` value of the current component to force re-rendering of the component.

- className (string | dict; optional):  
   CSS class name of the current component, supports [dynamic css](/advanced-classname).

- popupClassName (string; optional):  
   CSS class name of the dropdown menu.

- name (string; optional):  
   Used with the `AntdForm` batch value collection/control function, serving as the field name of the current form item. Defaults to `id`.

- enableBatchControl (boolean; default True):  
   Controls whether the current component participates in the effective `AntdForm` batch value collection/control function. Default: `True`.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):  
   Language of the component text. Options: `'zh-cn'` (Simplified Chinese), `'en-us'` (English), `'de-de'` (German), `'ru-ru'` (Russian).  
   Default: `'zh-cn'`.

- format (string; optional):  
   Date/time display format, [reference](https://day.js.org/docs/en/display/format).  
   Default: `'YYYY-MM-DD'`.

- picker (a value equal to: 'date', 'week', 'month', 'quarter', 'year'; default 'date'):  
   Date selection granularity. Options: `'date'`, `'week'`, `'month'`, `'quarter'`, `'year'`.  
   Default: `'date'`.

- firstDayOfWeek (number; optional):  
   Custom index of the first day of the week.

- disabled (boolean; default False):  
   Whether to disable the component. Default: `False`.

- showTime (dict; default False):  
   Configure parameters related to the time selection panel. Default: `False`.

  `showTime` is a boolean | dict with keys:

  - defaultValue (string; optional):  
     Initial selected time string for the time selection panel.

  - format (string; optional):  
     Time format corresponding to `defaultValue`, [reference](https://day.js.org/docs/en/display/format).  
     Default: `'HH:mm:ss'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):  
   Size specification of the component. Options: `'small'`, `'middle'`, `'large'`.  
   Default: `'middle'`.

- bordered (boolean; default True):  
   Whether to show a border. Equivalent to `variant='outlined'` when set to `True`. Default: `True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):  
   Variant type. Options: `'outlined'`, `'borderless'`, `'filled'`, `'underlined'`. `'outlined'` is equivalent to `bordered=True`, but takes higher priority.

- placeholder (string; optional):  
   Placeholder text in the input box.

- placement (a value equal to: 'bottomLeft', 'bottomRight', 'topLeft', 'topRight'; default 'bottomLeft'):  
   Direction in which the panel expands. Options: `'bottomLeft'`, `'bottomRight'`, `'topLeft'`, `'topRight'`.  
   Default: `'bottomLeft'`.

- value (string; optional):  
   Listen to or set the selected value, corresponding to `format`.

- defaultValue (string; optional):  
   Initial selected value, corresponding to `format`.

- pickerValue (string; optional):  
   Listen to or set the panel’s displayed date, corresponding to `format`.

- disabledDatesStrategy (list of dicts; optional):  
   Configure an array of disabled date strategies. Dates matching at least one rule will be disabled.

  `disabledDatesStrategy` is a list of dicts with keys:

  - mode (a value equal to: 'eq', 'ne', 'le', 'lt', 'ge', 'gt', 'in', 'not-in', 'in-enumerate-dates', 'not-in-enumerate-dates'; optional):  
     Current strategy type. Options: `'eq'` (equal), `'ne'` (not equal), `'le'` (less than or equal), `'lt'` (less than), `'ge'` (greater than or equal),  
     `'gt'` (greater than), `'in'` (in), `'not-in'` (not in), `'in-enumerate-dates'` (in list of date strings), `'not-in-enumerate-dates'` (not in list of date strings).

  - target (a value equal to: 'day', 'month', 'quarter', 'year', 'dayOfYear', 'dayOfWeek', 'specific-date'; optional):  
     Strategy target. Options: `'dayOfYear'` (by day of year), `'dayOfWeek'` (by day of week), `'day'` (by day), `'month'` (by month), `'quarter'` (by quarter), `'year'` (by year), `'specific-date'` (specific date).  
     For `'specific-date'`, the `value` must strictly follow the `'YYYY-MM-DD'` format.

  - value (number | string | list of numbers | list of strings; optional):  
     The actual constraint value corresponding to the strategy type and target.

- status (a value equal to: 'error', 'warning'; optional):  
   Validation status. Options: `'error'`, `'warning'`.

- allowClear (boolean; default True):  
   Whether to allow clearing the selected value with one click. Default: `True`.

- autoFocus (boolean; default False):  
   Whether to automatically focus. Default: `False`.

- readOnly (boolean; optional):  
   Whether to render as read-only. Default: `False`.

- extraFooter (a list of or a singular dash component, string or number; optional):  
   Component type, extra footer content.

- showToday (boolean; default True):  
   Whether to show the “Today” quick selection button. Default: `True`.

- presets (list of dicts; optional):  
   Configure a list of presets.

  `presets` is a list of dicts with keys:

  - label (a list of or a singular dash component, string or number; optional):  
     Component type, label for the preset item.

  - value (string; optional):  
     Value of the preset item, corresponding to `format`.

- clickedPreset (dict; optional):  
   Works with the `presets` parameter, listens for the most recent preset item click event information.

  `clickedPreset` is a dict with keys:

  - value (string | number; optional):  
     Value of the preset item.

  - timestamp (number; optional):  
     Timestamp of the event.

- needConfirm (boolean; default False):  
   Whether clicking a button is required to confirm selection. If `False`, losing focus means selection is made. Default: `False`.

- customCells (list of dicts; optional):  
   Customize cell styles for specific dates.

  `customCells` is a list of dicts with keys:

  - year (number; optional):  
     Year value for matching.

  - month (number; optional):  
     Month value for matching.

  - date (number; optional):  
     Day value for matching.

  - style (dict; optional):  
     Custom CSS style.

  - className (string; optional):  
     Custom CSS class name.

- prefix (a list of or a singular dash component, string or number; optional):  
   Component type, embedded prefix content.

- suffixIcon (a list of or a singular dash component, string or number; optional):  
   Custom suffix icon content for the selection box.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):  
   Anchoring strategy for the dropdown layer. Options: `'parent'`, `'body'`. Default: `'body'`.

- batchPropsNames (list of strings; optional):  
   List of property names to include in [batch property listening](/batch-props-values).

- batchPropsValues (dict; optional):  
   Listen to the values of properties specified in `batchPropsNames`.

- data-_ (string; optional):  
   Wildcard attribute in `data-_` format.

- aria-_ (string; optional):  
   Wildcard attribute in `aria-_` format.

- persistence (boolean | string | number; optional):  
   Whether to enable [property persistence](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):  
   Properties enabled for persistence. Options: `'value'`.  
   Default: `['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):  
   Type of persistence storage. Options: `'local'` (local storage), `'session'` (session storage), `'memory'` (in-memory).  
   Default: `'local'`.
