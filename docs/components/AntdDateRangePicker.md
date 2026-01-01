# AntdDateRangePicker

## 简介源码：`views/AntdDateRangePicker/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdDateRangePicker 日期范围选择'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdDateRangePicker 日期范围选择', level=2),
        fac.AntdParagraph('提供常见的日期范围选择相关功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo1',
                    style={'width': 300},
                ),
                fac.AntdText(id='date-range-picker-demo1-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo2',
                    placeholder=['开始日期时间', '结束日期时间'],
                    style={'width': 350},
                    showTime=True,
                    needConfirm=True,
                ),
                fac.AntdText(id='date-range-picker-demo2-output'),
            ],
            align='center',
        ),
        fac.AntdSpace(
            [
                fac.AntdDateRangePicker(
                    id='date-range-picker-demo3',
                    placeholder=['配合自定义format', ''],
                    format='YYYY年MM月DD日',
                    style={'width': 300},
                ),
                fac.AntdText(id='date-range-picker-demo3-output'),
            ],
            align='center',
        ),
    ],
    direction='vertical',
)

...

@app.callback(
    Output('date-range-picker-demo1-output', 'children'),
    Input('date-range-picker-demo1', 'value'),
)
def date_range_picker_demo1(value):
    return f'value: {value}'


@app.callback(
    Output('date-range-picker-demo2-output', 'children'),
    Input('date-range-picker-demo2', 'value'),
)
def date_range_picker_demo2(value):
    return f'value: {value}'


@app.callback(
    Output('date-range-picker-demo3-output', 'children'),
    Input('date-range-picker-demo3', 'value'),
)
def date_range_picker_demo3(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(),
        fac.AntdDateRangePicker(
            placeholder=['开始日期时间', '结束日期时间'],
            showTime=True,
            needConfirm=True,
        ),
    ],
    wrap=True,
)
```

### custom_cells

- 说明：演示 custom_cells 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        '精确日期匹配：明天',
        fac.AntdDateRangePicker(
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
        fac.AntdDateRangePicker(
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
        fac.AntdDateRangePicker(
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
```

### custom_format

- 说明：演示 custom_format 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placeholder=['picker="date"', ''],
            format='YYYY年MM月DD日',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="week"', ''],
            picker='week',
            format='YYYY年第w周',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="month"', ''],
            picker='month',
            format='YYYY-MM',
            style={'width': 300},
        ),
        fac.AntdDateRangePicker(
            placeholder=['picker="year"', ''],
            picker='year',
            format='YYYY年',
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### different_picker

- 说明：演示 different_picker 的用法。

#### 代码
```python
fac.AntdSpace(
        [
            fac.AntdDateRangePicker(
                picker=picker, placeholder=['picker:', picker]
            )
            for picker in ['date', 'week', 'month', 'quarter', 'year']
        ],
        direction='vertical',
    )
```

### different_placement

- 说明：演示 different_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placement=placement, placeholder=['placement:', placement]
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
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(disabled=[True, True]),
        fac.AntdDateRangePicker(disabled=[True, False]),
        fac.AntdDateRangePicker(disabled=[False, True]),
    ],
    direction='vertical',
)
```

### disabled_dates

- 说明：演示 disabled_dates 的用法。

#### 代码
```python
[
    fac.AntdDivider("mode='eq'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'eq', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ne'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月非6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'ne', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='le'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月小于等于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'le', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='lt'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月小于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'lt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='ge'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月大于等于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'ge', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='gt'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月大于6号', ''],
        style={'width': 400},
        disabledDatesStrategy=[{'mode': 'gt', 'target': 'day', 'value': 6}],
    ),
    fac.AntdDivider("mode='in'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用每月的5号到25号', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider("mode='not-in'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用非每月的5号到25号', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'not-in', 'target': 'day', 'value': list(range(5, 26))}
        ],
    ),
    fac.AntdDivider(
        "mode='in-enumerate-dates'", innerTextOrientation='left'
    ),
    fac.AntdDateRangePicker(
        placeholder=['禁用枚举列表中的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {
                'mode': 'in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider(
        "mode='not-in-enumerate-dates'", innerTextOrientation='left'
    ),
    fac.AntdDateRangePicker(
        placeholder=['禁用非枚举列表中的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {
                'mode': 'not-in-enumerate-dates',
                'value': [f'2023-01-0{i}' for i in range(1, 10)],
            }
        ],
        pickerValue='2023-01-01',
    ),
    fac.AntdDivider("target='specific-date'", innerTextOrientation='left'),
    fac.AntdDateRangePicker(
        placeholder=['禁用指定日期之前的日期', ''],
        style={'width': 400},
        disabledDatesStrategy=[
            {'mode': 'lt', 'target': 'specific-date', 'value': '2023-01-15'}
        ],
        pickerValue='2023-01-01',
    ),
]
```

### extra_footer

- 说明：演示 extra_footer 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            extraFooter=fac.AntdText('底部额外内容示例')
        ),
        fac.AntdDateRangePicker(
            placeholder=['开始日期时间', '结束日期时间'],
            showTime=True,
            extraFooter=fac.AntdText('底部额外内容示例'),
        ),
    ],
    wrap=True,
)
```

### listen_picker_value

- 说明：演示 listen_picker_value 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            id='date-range-picker-listen-picker-value-demo',
            style={'width': 250},
        ),
        fac.AntdText(
            id='date-range-picker-listen-picker-value-demo-output'
        ),
    ]
)

...

@app.callback(
    Output('date-range-picker-listen-picker-value-demo-output', 'children'),
    Input('date-range-picker-listen-picker-value-demo', 'pickerValue'),
)
def show_picker_value(pickerValue):
    return f'pickerValue: {pickerValue}'
```

### picker_value

- 说明：演示 picker_value 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            pickerValue='1999-12-31', style={'width': 300}
        ),
        fac.AntdDateRangePicker(
            placeholder=['配合自定义format', ''],
            pickerValue='1999年12月31日',
            format='YYYY年MM月DD日',
            style={'width': 300},
        ),
    ],
    direction='vertical',
)
```

### prefix

- 说明：演示 prefix 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'],
    prefix=fac.AntdIcon(icon='antd-user'),
)
```

### read_only

- 说明：演示 read_only 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'], readOnly=True
)
```

### render_status

- 说明：演示 render_status 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDateRangePicker(
            placeholder=[f'status="{status}"', ''],
            status=status,
            style={'width': 300},
        )
        for status in ['warning', 'error']
    ],
    direction='vertical',
)
```

### suffix_icon

- 说明：演示 suffix_icon 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    value=['2023-01-01', '2023-01-20'],
    suffixIcon=fac.AntdIcon(icon='antd-user'),
)
```

### time_default_value

- 说明：演示 time_default_value 的用法。

#### 代码
```python
fac.AntdDateRangePicker(
    placeholder=['开始日期时间', '结束日期时间'],
    showTime={'defaultValue': ['08:30:00', '17:30:00']},
    needConfirm=True,
)
```
