# AntdConfigProvider

## 简介源码：`views/AntdConfigProvider/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '其他'},
                {'title': 'AntdConfigProvider 参数配置'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdConfigProvider 参数配置', level=2),
        fac.AntdParagraph(
            '用于对所包裹内容的主题色、尺寸规格、禁用状态、国际化等进行统一强制设置。'
        ),
    ]

```

## 示例源码（demos）

### `views/AntdConfigProvider/demos/algorithm.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='config-provider-algorithm',
                options=[
                    {'label': algorithm, 'value': algorithm}
                    for algorithm in ['default', 'dark', 'compact']
                ],
                optionType='button',
                defaultValue='default',
            ),
            label='algorithm',
        ),
        fac.AntdDivider(isDashed=True),
        fac.AntdConfigProvider(
            fac.AntdSpace(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': '表格测试', 'dataIndex': '表格测试'}
                        ],
                        bordered=True,
                        style={'width': 300},
                    ),
                    fac.AntdTable(
                        columns=[
                            {'title': '表格测试', 'dataIndex': '表格测试'}
                        ],
                        data=[{'表格测试': 999}],
                        bordered=True,
                        style={'width': 300},
                    ),
                    fac.AntdCalendar(
                        defaultValue='2023-01-01', style={'width': '300px'}
                    ),
                    fac.AntdCascader(options=[]),
                    fac.AntdComment(
                        authorName='费弗里',
                        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                        publishTime={
                            'value': '2022-01-01 19:29:01',
                            'format': 'YYYY-MM-DD hh:mm:ss',
                        },
                        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                        avatarProps={
                            'mode': 'image',
                            'src': '/assets/imgs/avatar-demo.jpg',
                        },
                        fromNow=True,
                    ),
                    fac.AntdCopyText(
                        text='AntdCopyText复制示例',
                        beforeIcon='点我复制',
                        afterIcon='复制成功',
                    ),
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker(),
                    fac.AntdEmpty(),
                    fac.AntdImage(
                        src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                        height=400,
                    ),
                    fac.AntdPagination(defaultPageSize=10, total=100),
                    fac.AntdPopconfirm(
                        fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                    ),
                    fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                    fac.AntdTimePicker(),
                    fac.AntdTimeRangePicker(),
                    fac.AntdTransfer(dataSource=[], style={'width': 500}),
                    fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                    fac.AntdParagraph('AntdParagraph测试', copyable=True),
                    fac.AntdText('AntdText测试', copyable=True),
                    fac.AntdTitle('AntdTitle测试', copyable=True),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            id='config-provider-algorithm-demo',
            algorithm='default',
        ),
    ]

    return demo_contents


app.clientside_callback(
    '(value) => value',
    Output('config-provider-algorithm-demo', 'algorithm'),
    Input('config-provider-algorithm', 'value'),
    prevent_initial_call=True,
)


code_string = [
    {
        'code': """
[
    fac.AntdFormItem(
        fac.AntdRadioGroup(
            id='config-provider-algorithm',
            options=[
                {'label': algorithm, 'value': algorithm}
                for algorithm in ['default', 'dark', 'compact']
            ],
            optionType='button',
            defaultValue='default',
        ),
        label='algorithm',
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdConfigProvider(
        fac.AntdSpace(
            [
                fac.AntdTable(
                    columns=[
                        {'title': '表格测试', 'dataIndex': '表格测试'}
                    ],
                    bordered=True,
                    style={'width': 300},
                ),
                fac.AntdTable(
                    columns=[
                        {'title': '表格测试', 'dataIndex': '表格测试'}
                    ],
                    data=[{'表格测试': 999}],
                    bordered=True,
                    style={'width': 300},
                ),
                fac.AntdCalendar(
                    defaultValue='2023-01-01', style={'width': '300px'}
                ),
                fac.AntdCascader(options=[]),
                fac.AntdComment(
                    authorName='费弗里',
                    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                    publishTime={
                        'value': '2022-01-01 19:29:01',
                        'format': 'YYYY-MM-DD hh:mm:ss',
                    },
                    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                    avatarProps={
                        'mode': 'image',
                        'src': '/assets/imgs/avatar-demo.jpg',
                    },
                    fromNow=True,
                ),
                fac.AntdCopyText(
                    text='AntdCopyText复制示例',
                    beforeIcon='点我复制',
                    afterIcon='复制成功',
                ),
                fac.AntdDatePicker(),
                fac.AntdDateRangePicker(),
                fac.AntdEmpty(),
                fac.AntdImage(
                    src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                    height=400,
                ),
                fac.AntdPagination(defaultPageSize=10, total=100),
                fac.AntdPopconfirm(
                    fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                ),
                fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                fac.AntdTimePicker(),
                fac.AntdTimeRangePicker(),
                fac.AntdTransfer(dataSource=[], style={'width': 500}),
                fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                fac.AntdParagraph('AntdParagraph测试', copyable=True),
                fac.AntdText('AntdText测试', copyable=True),
                fac.AntdTitle('AntdTitle测试', copyable=True),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        id='config-provider-algorithm-demo',
        algorithm='default',
    ),
]

...

app.clientside_callback(
    '(value) => value',
    Output('config-provider-algorithm-demo', 'algorithm'),
    Input('config-provider-algorithm', 'value'),
    prevent_initial_call=True,
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdFormItem(
            fac.AntdSwitch(
                id='config-provider-component-disabled',
                checkedChildren='True',
                unCheckedChildren='False',
            ),
            label='componentDisabled',
        ),
        fac.AntdDivider(isDashed=True),
        fac.AntdConfigProvider(
            fac.AntdSpace(
                [
                    fac.AntdButton('按钮测试'),
                    fac.AntdCascader(options=[], placeholder='级联选择测试'),
                    fac.AntdCheckbox(),
                    fac.AntdCheckboxGroup(
                        options=[
                            {'label': f'选项{i}', 'value': f'选项{i}'}
                            for i in range(5)
                        ]
                    ),
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker(),
                    fac.AntdDropdown(
                        title='下拉选择测试',
                        menuItems=[
                            {'title': '选项1'},
                            {'title': '选项2'},
                            {'isDivider': True},
                            {'title': '选项3-1'},
                            {'title': '选项3-2'},
                        ],
                    ),
                    fac.AntdInput(
                        placeholder='输入框测试', style={'width': 200}
                    ),
                    fac.AntdInputNumber(
                        placeholder='数值输入框测试', style={'width': 200}
                    ),
                    fac.AntdMentions(
                        defaultValue='提及测试',
                        options=[
                            {'label': f'用户{c}', 'value': f'用户{c}'}
                            for c in list('abcdef')
                        ],
                        style={'width': 200},
                    ),
                    fac.AntdPagination(defaultPageSize=10, total=100),
                    fac.AntdPopconfirm(
                        fac.AntdButton('气泡确认测试', type='primary'),
                        title='气泡确认测试',
                    ),
                    fac.AntdRadioGroup(
                        options=[
                            {'label': f'选项{i}', 'value': f'选项{i}'}
                            for i in range(5)
                        ],
                        defaultValue='选项1',
                    ),
                    fac.AntdRate(count=10, value=7.5, allowHalf=True),
                    fac.AntdSegmented(
                        options=[
                            {'label': f'选项{i}', 'value': f'选项{i}'}
                            for i in range(5)
                        ],
                        defaultValue='选项1',
                    ),
                    fac.AntdSegmentedColoring(
                        size='small',
                        min=-10,
                        max=10,
                        breakpoints=[0, 1, 2, 3, 4, 5],
                        colors=[
                            '#deecf9',
                            '#71afe5',
                            '#2b88d8',
                            '#0078d4',
                            '#106ebe',
                        ],
                    ),
                    fac.AntdSelect(
                        placeholder='请选择国家：',
                        options=[
                            {'label': '中国', 'value': '中国'},
                            {'label': '美国', 'value': '美国'},
                            {'label': '俄罗斯', 'value': '俄罗斯'},
                            {
                                'label': '德国',
                                'value': '德国',
                                'disabled': True,
                            },
                            {'label': '加拿大', 'value': '加拿大'},
                        ],
                        style={
                            # 使用css样式固定宽度
                            'width': '200px'
                        },
                    ),
                    fac.AntdSlider(
                        min=0, max=100, defaultValue=66, style={'width': 200}
                    ),
                    fac.AntdSwitch(),
                    fac.AntdTimePicker(),
                    fac.AntdTimeRangePicker(),
                    fac.AntdTransfer(
                        dataSource=[
                            {'key': i, 'title': f'选项{i}'}
                            for i in range(1, 10)
                        ],
                        targetKeys=[2, 3, 4],
                        style={'width': 300},
                    ),
                    fac.AntdTreeSelect(
                        treeData=[
                            {
                                'key': '节点1',
                                'value': '1',
                                'title': '节点1',
                                'children': [
                                    {
                                        'key': f'节点1-{i}',
                                        'value': f'1-{i}',
                                        'title': f'节点1-{i}',
                                    }
                                    for i in range(1, 5)
                                ],
                            },
                            {'key': '节点2', 'value': '2', 'title': '节点2'},
                        ],
                        placeholder='请选择',
                        style={'width': 256},
                    ),
                    fac.AntdCheckCard(fac.AntdText('选择卡片示例' * 10)),
                    fac.AntdCheckCardGroup(
                        [
                            fac.AntdCheckCard(f'选项{i}', value=i)
                            for i in range(1, 6)
                        ],
                        defaultValue=3,
                    ),
                    fac.AntdUpload(buttonContent='上传测试'),
                    fac.AntdDraggerUpload(text='拖拽上传测试'),
                    fac.AntdPictureUpload(buttonContent='图片上传测试'),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            id='config-provider-component-disabled-demo',
        ),
    ]

    return demo_contents


app.clientside_callback(
    '(checked) => checked',
    Output('config-provider-component-disabled-demo', 'componentDisabled'),
    Input('config-provider-component-disabled', 'checked'),
)

code_string = [
    {
        'code': """
[
    fac.AntdFormItem(
        fac.AntdSwitch(
            id='config-provider-component-disabled',
            checkedChildren='True',
            unCheckedChildren='False',
        ),
        label='componentDisabled',
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdConfigProvider(
        fac.AntdSpace(
            [
                fac.AntdButton('按钮测试'),
                fac.AntdCascader(options=[], placeholder='级联选择测试'),
                fac.AntdCheckbox(),
                fac.AntdCheckboxGroup(
                    options=[
                        {'label': f'选项{i}', 'value': f'选项{i}'}
                        for i in range(5)
                    ]
                ),
                fac.AntdDatePicker(),
                fac.AntdDateRangePicker(),
                fac.AntdDropdown(
                    title='下拉选择测试',
                    menuItems=[
                        {'title': '选项1'},
                        {'title': '选项2'},
                        {'isDivider': True},
                        {'title': '选项3-1'},
                        {'title': '选项3-2'},
                    ],
                ),
                fac.AntdInput(
                    placeholder='输入框测试', style={'width': 200}
                ),
                fac.AntdInputNumber(
                    placeholder='数值输入框测试', style={'width': 200}
                ),
                fac.AntdMentions(
                    defaultValue='提及测试',
                    options=[
                        {'label': f'用户{c}', 'value': f'用户{c}'}
                        for c in list('abcdef')
                    ],
                    style={'width': 200},
                ),
                fac.AntdPagination(defaultPageSize=10, total=100),
                fac.AntdPopconfirm(
                    fac.AntdButton('气泡确认测试', type='primary'),
                    title='气泡确认测试',
                ),
                fac.AntdRadioGroup(
                    options=[
                        {'label': f'选项{i}', 'value': f'选项{i}'}
                        for i in range(5)
                    ],
                    defaultValue='选项1',
                ),
                fac.AntdRate(count=10, value=7.5, allowHalf=True),
                fac.AntdSegmented(
                    options=[
                        {'label': f'选项{i}', 'value': f'选项{i}'}
                        for i in range(5)
                    ],
                    defaultValue='选项1',
                ),
                fac.AntdSegmentedColoring(
                    size='small',
                    min=-10,
                    max=10,
                    breakpoints=[0, 1, 2, 3, 4, 5],
                    colors=[
                        '#deecf9',
                        '#71afe5',
                        '#2b88d8',
                        '#0078d4',
                        '#106ebe',
                    ],
                ),
                fac.AntdSelect(
                    placeholder='请选择国家：',
                    options=[
                        {'label': '中国', 'value': '中国'},
                        {'label': '美国', 'value': '美国'},
                        {'label': '俄罗斯', 'value': '俄罗斯'},
                        {
                            'label': '德国',
                            'value': '德国',
                            'disabled': True,
                        },
                        {'label': '加拿大', 'value': '加拿大'},
                    ],
                    style={
                        # 使用css样式固定宽度
                        'width': '200px'
                    },
                ),
                fac.AntdSlider(
                    min=0, max=100, defaultValue=66, style={'width': 200}
                ),
                fac.AntdSwitch(),
                fac.AntdTimePicker(),
                fac.AntdTimeRangePicker(),
                fac.AntdTransfer(
                    dataSource=[
                        {'key': i, 'title': f'选项{i}'}
                        for i in range(1, 10)
                    ],
                    targetKeys=[2, 3, 4],
                    style={'width': 300},
                ),
                fac.AntdTreeSelect(
                    treeData=[
                        {
                            'key': '节点1',
                            'value': '1',
                            'title': '节点1',
                            'children': [
                                {
                                    'key': f'节点1-{i}',
                                    'value': f'1-{i}',
                                    'title': f'节点1-{i}',
                                }
                                for i in range(1, 5)
                            ],
                        },
                        {'key': '节点2', 'value': '2', 'title': '节点2'},
                    ],
                    placeholder='请选择',
                    style={'width': 256},
                ),
                fac.AntdCheckCard(fac.AntdText('选择卡片示例' * 10)),
                fac.AntdCheckCardGroup(
                    [
                        fac.AntdCheckCard(f'选项{i}', value=i)
                        for i in range(1, 6)
                    ],
                    defaultValue=3,
                ),
                fac.AntdUpload(buttonContent='上传测试'),
                fac.AntdDraggerUpload(text='拖拽上传测试'),
                fac.AntdPictureUpload(buttonContent='图片上传测试'),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        id='config-provider-component-disabled-demo',
    ),
]

...

app.clientside_callback(
    '(checked) => checked',
    Output('config-provider-component-disabled-demo', 'componentDisabled'),
    Input('config-provider-component-disabled', 'checked'),
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/locale.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='config-provider-locale',
                options=[
                    {'label': locale, 'value': locale}
                    for locale in ['zh-cn', 'en-us', 'de-de', 'ru-ru']
                ],
                optionType='button',
                defaultValue='zh-cn',
            ),
            label='locale',
        ),
        fac.AntdDivider(isDashed=True),
        fac.AntdConfigProvider(
            fac.AntdSpace(
                [
                    fac.AntdCalendar(
                        defaultValue='2023-01-01', style={'width': '300px'}
                    ),
                    fac.AntdCascader(options=[]),
                    fac.AntdComment(
                        authorName='费弗里',
                        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                        publishTime={
                            'value': '2022-01-01 19:29:01',
                            'format': 'YYYY-MM-DD hh:mm:ss',
                        },
                        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                        avatarProps={
                            'mode': 'image',
                            'src': '/assets/imgs/avatar-demo.jpg',
                        },
                        fromNow=True,
                    ),
                    fac.AntdCopyText(
                        text='AntdCopyText复制示例',
                        beforeIcon='点我复制',
                        afterIcon='复制成功',
                    ),
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker(),
                    fac.AntdEmpty(),
                    fac.AntdImage(
                        src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                        height=400,
                    ),
                    fac.AntdPagination(defaultPageSize=10, total=100),
                    fac.AntdPopconfirm(
                        fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                    ),
                    fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                    fac.AntdTimePicker(),
                    fac.AntdTimeRangePicker(),
                    fac.AntdTransfer(dataSource=[], style={'width': 500}),
                    fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                    fac.AntdParagraph('AntdParagraph测试', copyable=True),
                    fac.AntdText('AntdText测试', copyable=True),
                    fac.AntdTitle('AntdTitle测试', copyable=True),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            id='config-provider-locale-demo',
            locale='zh-cn',
        ),
    ]

    return demo_contents


app.clientside_callback(
    '(value) => value',
    Output('config-provider-locale-demo', 'locale'),
    Input('config-provider-locale', 'value'),
    prevent_initial_call=True,
)

code_string = [
    {
        'code': """
[
    fac.AntdFormItem(
        fac.AntdRadioGroup(
            id='config-provider-locale',
            options=[
                {'label': locale, 'value': locale}
                for locale in ['zh-cn', 'en-us', 'de-de', 'ru-ru']
            ],
            optionType='button',
            defaultValue='zh-cn',
        ),
        label='locale',
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdConfigProvider(
        fac.AntdSpace(
            [
                fac.AntdCalendar(
                    defaultValue='2023-01-01', style={'width': '300px'}
                ),
                fac.AntdCascader(options=[]),
                fac.AntdComment(
                    authorName='费弗里',
                    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                    publishTime={
                        'value': '2022-01-01 19:29:01',
                        'format': 'YYYY-MM-DD hh:mm:ss',
                    },
                    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                    avatarProps={
                        'mode': 'image',
                        'src': '/assets/imgs/avatar-demo.jpg',
                    },
                    fromNow=True,
                ),
                fac.AntdCopyText(
                    text='AntdCopyText复制示例',
                    beforeIcon='点我复制',
                    afterIcon='复制成功',
                ),
                fac.AntdDatePicker(),
                fac.AntdDateRangePicker(),
                fac.AntdEmpty(),
                fac.AntdImage(
                    src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                    height=400,
                ),
                fac.AntdPagination(defaultPageSize=10, total=100),
                fac.AntdPopconfirm(
                    fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                ),
                fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                fac.AntdTimePicker(),
                fac.AntdTimeRangePicker(),
                fac.AntdTransfer(dataSource=[], style={'width': 500}),
                fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                fac.AntdParagraph('AntdParagraph测试', copyable=True),
                fac.AntdText('AntdText测试', copyable=True),
                fac.AntdTitle('AntdTitle测试', copyable=True),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        id='config-provider-locale-demo',
        locale='zh-cn',
    ),
]

...

app.clientside_callback(
    '(value) => value',
    Output('config-provider-locale-demo', 'locale'),
    Input('config-provider-locale', 'value'),
    prevent_initial_call=True,
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/primary_color.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fuc.FefferyHexColorPicker(
                id='config-provider-primary-color', color='#1890ff'
            ),
            fac.AntdConfigProvider(
                fac.AntdButton('按钮示例', type='primary'),
                id='config-provider-primary-color-demo',
            ),
        ],
        direction='vertical',
    )

    return demo_contents


app.clientside_callback(
    '(color) => color',
    Output('config-provider-primary-color-demo', 'primaryColor'),
    Input('config-provider-primary-color', 'color'),
)

code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='config-provider-primary-color', color='#1890ff'
        ),
        fac.AntdConfigProvider(
            fac.AntdButton('按钮示例', type='primary'),
            id='config-provider-primary-color-demo',
        ),
    ],
    direction='vertical',
)

...

app.clientside_callback(
    '(color) => color',
    Output('config-provider-primary-color-demo', 'primaryColor'),
    Input('config-provider-primary-color', 'color'),
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/size.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='config-provider-component-size',
                options=[
                    {'label': size, 'value': size}
                    for size in ['small', 'middle', 'large']
                ],
                optionType='button',
                defaultValue='small',
            ),
            label='componentSize',
        ),
        fac.AntdDivider(isDashed=True),
        fac.AntdConfigProvider(
            fac.AntdSpace(
                [
                    fac.AntdButton('按钮测试'),
                    fac.AntdCascader(options=[], placeholder='级联选择测试'),
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker(),
                    fac.AntdInput(
                        placeholder='输入框测试', style={'width': 256}
                    ),
                    fac.AntdInputNumber(
                        placeholder='数字输入框测试', style={'width': 256}
                    ),
                    fac.AntdRadioGroup(
                        options=[
                            {'label': f'选项{i}', 'value': f'选项{i}'}
                            for i in range(5)
                        ],
                        defaultValue='选项1',
                        optionType='button',
                    ),
                    fac.AntdSegmented(
                        options=[
                            {'label': f'选项{i}', 'value': f'选项{i}'}
                            for i in range(5)
                        ],
                        defaultValue='选项1',
                    ),
                    fac.AntdSegmentedColoring(
                        size='small',
                        min=-10,
                        max=10,
                        breakpoints=[0, 1, 2, 3, 4, 5],
                        colors=[
                            '#deecf9',
                            '#71afe5',
                            '#2b88d8',
                            '#0078d4',
                            '#106ebe',
                        ],
                    ),
                    fac.AntdSelect(
                        placeholder='请选择国家：',
                        options=[
                            {'label': '中国', 'value': '中国'},
                            {'label': '美国', 'value': '美国'},
                            {'label': '俄罗斯', 'value': '俄罗斯'},
                            {
                                'label': '德国',
                                'value': '德国',
                                'disabled': True,
                            },
                            {'label': '加拿大', 'value': '加拿大'},
                        ],
                        style={
                            # 使用css样式固定宽度
                            'width': '200px'
                        },
                    ),
                    fac.AntdTimePicker(),
                    fac.AntdTimeRangePicker(),
                    fac.AntdTreeSelect(
                        treeData=[
                            {
                                'key': '节点1',
                                'value': '1',
                                'title': '节点1',
                                'children': [
                                    {
                                        'key': f'节点1-{i}',
                                        'value': f'1-{i}',
                                        'title': f'节点1-{i}',
                                    }
                                    for i in range(1, 5)
                                ],
                            },
                            {'key': '节点2', 'value': '2', 'title': '节点2'},
                        ],
                        placeholder='请选择',
                        style={'width': 256},
                    ),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            id='config-provider-component-size-demo',
            componentSize='small',
        ),
    ]

    return demo_contents


app.clientside_callback(
    '(value) => value',
    Output('config-provider-component-size-demo', 'componentSize'),
    Input('config-provider-component-size', 'value'),
)

code_string = [
    {
        'code': """
[
    fac.AntdFormItem(
        fac.AntdRadioGroup(
            id='config-provider-component-size',
            options=[
                {'label': size, 'value': size}
                for size in ['small', 'middle', 'large']
            ],
            optionType='button',
            defaultValue='small',
        ),
        label='componentSize',
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdConfigProvider(
        fac.AntdSpace(
            [
                fac.AntdButton('按钮测试'),
                fac.AntdCascader(options=[], placeholder='级联选择测试'),
                fac.AntdDatePicker(),
                fac.AntdDateRangePicker(),
                fac.AntdInput(
                    placeholder='输入框测试', style={'width': 256}
                ),
                fac.AntdInputNumber(
                    placeholder='数字输入框测试', style={'width': 256}
                ),
                fac.AntdRadioGroup(
                    options=[
                        {'label': f'选项{i}', 'value': f'选项{i}'}
                        for i in range(5)
                    ],
                    defaultValue='选项1',
                    optionType='button',
                ),
                fac.AntdSegmented(
                    options=[
                        {'label': f'选项{i}', 'value': f'选项{i}'}
                        for i in range(5)
                    ],
                    defaultValue='选项1',
                ),
                fac.AntdSegmentedColoring(
                    size='small',
                    min=-10,
                    max=10,
                    breakpoints=[0, 1, 2, 3, 4, 5],
                    colors=[
                        '#deecf9',
                        '#71afe5',
                        '#2b88d8',
                        '#0078d4',
                        '#106ebe',
                    ],
                ),
                fac.AntdSelect(
                    placeholder='请选择国家：',
                    options=[
                        {'label': '中国', 'value': '中国'},
                        {'label': '美国', 'value': '美国'},
                        {'label': '俄罗斯', 'value': '俄罗斯'},
                        {
                            'label': '德国',
                            'value': '德国',
                            'disabled': True,
                        },
                        {'label': '加拿大', 'value': '加拿大'},
                    ],
                    style={
                        # 使用css样式固定宽度
                        'width': '200px'
                    },
                ),
                fac.AntdTimePicker(),
                fac.AntdTimeRangePicker(),
                fac.AntdTreeSelect(
                    treeData=[
                        {
                            'key': '节点1',
                            'value': '1',
                            'title': '节点1',
                            'children': [
                                {
                                    'key': f'节点1-{i}',
                                    'value': f'1-{i}',
                                    'title': f'节点1-{i}',
                                }
                                for i in range(1, 5)
                            ],
                        },
                        {'key': '节点2', 'value': '2', 'title': '节点2'},
                    ],
                    placeholder='请选择',
                    style={'width': 256},
                ),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        id='config-provider-component-size-demo',
        componentSize='small',
    ),
]

...

app.clientside_callback(
    '(value) => value',
    Output('config-provider-component-size-demo', 'componentSize'),
    Input('config-provider-component-size', 'value'),
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/use_old_theme.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdFormItem(
            fac.AntdRadioGroup(
                id='config-provider-use-old-theme',
                options=[
                    {'label': theme, 'value': theme}
                    for theme in ['None', 'default', 'dark']
                ],
                optionType='button',
                defaultValue='None',
            ),
            label='useOldTheme',
        ),
        fac.AntdDivider(isDashed=True),
        fac.AntdConfigProvider(
            fac.AntdSpace(
                [
                    fac.AntdTable(
                        columns=[
                            {'title': '表格测试', 'dataIndex': '表格测试'}
                        ],
                        bordered=True,
                        style={'width': 300},
                    ),
                    fac.AntdTable(
                        columns=[
                            {'title': '表格测试', 'dataIndex': '表格测试'}
                        ],
                        data=[{'表格测试': 999}],
                        bordered=True,
                        style={'width': 300},
                    ),
                    fac.AntdCalendar(
                        defaultValue='2023-01-01', style={'width': '300px'}
                    ),
                    fac.AntdCascader(options=[]),
                    fac.AntdComment(
                        authorName='费弗里',
                        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                        publishTime={
                            'value': '2022-01-01 19:29:01',
                            'format': 'YYYY-MM-DD hh:mm:ss',
                        },
                        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                        avatarProps={
                            'mode': 'image',
                            'src': '/assets/imgs/avatar-demo.jpg',
                        },
                        fromNow=True,
                    ),
                    fac.AntdCopyText(
                        text='AntdCopyText复制示例',
                        beforeIcon='点我复制',
                        afterIcon='复制成功',
                    ),
                    fac.AntdDatePicker(),
                    fac.AntdDateRangePicker(),
                    fac.AntdEmpty(),
                    fac.AntdImage(
                        src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                        height=400,
                    ),
                    fac.AntdPagination(defaultPageSize=10, total=100),
                    fac.AntdPopconfirm(
                        fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                    ),
                    fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                    fac.AntdTimePicker(),
                    fac.AntdTimeRangePicker(),
                    fac.AntdTransfer(dataSource=[], style={'width': 500}),
                    fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                    fac.AntdParagraph('AntdParagraph测试', copyable=True),
                    fac.AntdText('AntdText测试', copyable=True),
                    fac.AntdTitle('AntdTitle测试', copyable=True),
                ],
                direction='vertical',
                style={'width': '100%'},
            ),
            id='config-provider-use-old-theme-demo',
        ),
    ]

    return demo_contents


app.clientside_callback(
    '(value) => (value === "None" ? null : value)',
    Output('config-provider-use-old-theme-demo', 'useOldTheme'),
    Input('config-provider-use-old-theme', 'value'),
    prevent_initial_call=True,
)


code_string = [
    {
        'code': """
[
    fac.AntdFormItem(
        fac.AntdRadioGroup(
            id='config-provider-use-old-theme',
            options=[
                {'label': theme, 'value': theme}
                for theme in ['None', 'default', 'dark']
            ],
            optionType='button',
            defaultValue='None',
        ),
        label='useOldTheme',
    ),
    fac.AntdDivider(isDashed=True),
    fac.AntdConfigProvider(
        fac.AntdSpace(
            [
                fac.AntdTable(
                    columns=[
                        {'title': '表格测试', 'dataIndex': '表格测试'}
                    ],
                    bordered=True,
                    style={'width': 300},
                ),
                fac.AntdTable(
                    columns=[
                        {'title': '表格测试', 'dataIndex': '表格测试'}
                    ],
                    data=[{'表格测试': 999}],
                    bordered=True,
                    style={'width': 300},
                ),
                fac.AntdCalendar(
                    defaultValue='2023-01-01', style={'width': '300px'}
                ),
                fac.AntdCascader(options=[]),
                fac.AntdComment(
                    authorName='费弗里',
                    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
                    publishTime={
                        'value': '2022-01-01 19:29:01',
                        'format': 'YYYY-MM-DD hh:mm:ss',
                    },
                    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
                    avatarProps={
                        'mode': 'image',
                        'src': '/assets/imgs/avatar-demo.jpg',
                    },
                    fromNow=True,
                ),
                fac.AntdCopyText(
                    text='AntdCopyText复制示例',
                    beforeIcon='点我复制',
                    afterIcon='复制成功',
                ),
                fac.AntdDatePicker(),
                fac.AntdDateRangePicker(),
                fac.AntdEmpty(),
                fac.AntdImage(
                    src='http://fac-next.feffery.tech/assets/imgs/%E6%B5%81%E6%B5%AA%E5%9C%B0%E7%90%832%E6%B5%B7%E6%8A%A5.jpg',
                    height=400,
                ),
                fac.AntdPagination(defaultPageSize=10, total=100),
                fac.AntdPopconfirm(
                    fac.AntdButton('气泡确认测试'), title='气泡确认测试'
                ),
                fac.AntdSelect(placeholder='下拉选择测试', options=[]),
                fac.AntdTimePicker(),
                fac.AntdTimeRangePicker(),
                fac.AntdTransfer(dataSource=[], style={'width': 500}),
                fac.AntdTreeSelect(treeData=[], style={'width': 256}),
                fac.AntdParagraph('AntdParagraph测试', copyable=True),
                fac.AntdText('AntdText测试', copyable=True),
                fac.AntdTitle('AntdTitle测试', copyable=True),
            ],
            direction='vertical',
            style={'width': '100%'},
        ),
        id='config-provider-use-old-theme-demo',
    ),
]

...

app.clientside_callback(
    '(value) => (value === "None" ? null : value)',
    Output('config-provider-use-old-theme-demo', 'useOldTheme'),
    Input('config-provider-use-old-theme', 'value'),
    prevent_initial_call=True,
)
"""
    }
]

```

### `views/AntdConfigProvider/demos/waves_disabled.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(
                '未禁用',
                type='primary',
            ),
            fac.AntdConfigProvider(
                fac.AntdButton(
                    '已禁用',
                    type='primary',
                ),
                wavesDisabled=True,
            ),
        ]
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            '未禁用',
            type='primary',
        ),
        fac.AntdConfigProvider(
            fac.AntdButton(
                '已禁用',
                type='primary',
            ),
            wavesDisabled=True,
        ),
    ]
)
"""
    }
]

```
