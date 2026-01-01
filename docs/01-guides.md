# 指南与概览

## `views/what_is_fac.py`
```python
from dash import html
from flask import request
from datetime import datetime
import feffery_antd_components as fac
from dash.dependencies import Component

from server import app

# 国际化
from i18n import translator

latest_deploy_datetime = datetime.today().strftime('%Y-%m-%d')


def render() -> Component:
    """渲染“fac是什么”文档页"""

    current_locale = request.cookies.get(translator.cookie_name, 'zh-cn')

    return html.Div(
        [
            html.Div(
                [
                    fac.AntdBackTop(),
                    fac.AntdParagraph(
                        [
                            fac.AntdText(
                                translator.t(
                                    'feffery-antd-components: Ant Design在Dash中的最佳实现'
                                ),
                                strong=True,
                                style={'fontSize': '30px'},
                            ),
                            fac.AntdText('🐣', style={'fontSize': '30px'}),
                        ],
                        id='🐣',
                    ),
                    fac.AntdParagraph(
                        [
                            fac.AntdText(
                                translator.t('文档最近更新：'), strong=True
                            ),
                            fac.AntdText(latest_deploy_datetime, code=True),
                        ]
                    ),
                    fac.AntdDivider(),
                    fac.AntdParagraph(
                        (
                            [
                                fac.AntdText(
                                    '　　feffery-antd-components', strong=True
                                ),
                                fac.AntdText('（简称'),
                                fac.AntdText('fac', strong=True),
                                fac.AntdText('），基于著名的React UI组件库'),
                                fac.AntdText('ant design', strong=True),
                                fac.AntdText('进行大量二次开发，将'),
                                fac.AntdText('ant design', strong=True),
                                fac.AntdText('中的诸多实用组件及特性引入'),
                                fac.AntdText('Dash', italic=True),
                                fac.AntdText('，帮助开发者纯'),
                                fac.AntdText('Python', strong=True),
                                fac.AntdText(
                                    '构建现代化高质量且任意复杂程度的交互式web应用，帮助你将有关web应用的美好憧憬✨高效地实现。'
                                ),
                            ]
                            if current_locale == 'zh-cn'
                            else 'feffery-antd-components (fac), based on the famous React UI component library ant design, carries out a large number of secondary development, and introduces many practical components and features from ant design into Dash. Help developers build modern, high-quality and interactive web applications of any complexity in pure Python, and help you to realize the beautiful vision of web applications ✨ efficiently.'
                        )
                    ),
                    html.Div(
                        [
                            html.Img(
                                src=app.get_asset_url(
                                    'imgs/index/react-logo.svg'
                                ),
                                style={'height': '150px'},
                            ),
                            fac.AntdText(
                                '+',
                                style={
                                    'fontSize': '30px',
                                    'color': 'rgba(170, 170, 170, 1)',
                                    'padding': '0 15px 0 15px',
                                },
                            ),
                            html.Img(
                                src=app.get_asset_url(
                                    'imgs/index/antd-logo.svg'
                                ),
                                style={'height': '150px'},
                            ),
                            fac.AntdText(
                                '+',
                                style={
                                    'fontSize': '30px',
                                    'color': 'rgba(170, 170, 170, 1)',
                                    'padding': '0 15px 0 15px',
                                },
                            ),
                            html.Img(
                                src=app.get_asset_url(
                                    'imgs/index/dash-logo.png'
                                ),
                                style={'height': '140px'},
                            ),
                            fac.AntdText(
                                '=',
                                style={
                                    'fontSize': '30px',
                                    'color': 'rgba(170, 170, 170, 1)',
                                    'padding': '0 15px 0 15px',
                                },
                            ),
                            html.Img(
                                src=app.get_asset_url('imgs/fac-logo.svg'),
                                style={'height': '155px'},
                            ),
                        ],
                        style={
                            'display': 'flex',
                            'justifyContent': 'center',
                            'alignItems': 'center',
                            'paddingTop': 25,
                            'paddingBottom': 25,
                        },
                    ),
                    fac.AntdDivider(),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('🤩', style={'fontSize': '26px'}),
                            fac.AntdText(
                                translator.t('特性'),
                                strong=True,
                                style={'fontSize': '26px'},
                            ),
                        ],
                        id=translator.t('特性'),
                    ),
                    fac.AntdRow(
                        [
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/Python.svg',
                                                        style={
                                                            'height': '3rem',
                                                            'transform': 'translateY(12px)',
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '纯Python开发'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        translator.t(
                                                            '基于Dash框架，只需编写Python\n即可完成企业级应用开发全过程'
                                                        ),
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/MBE风格多色图标-组件.svg',
                                                        style={
                                                            'height': '4rem'
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '组件种类齐全'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        translator.t(
                                                            '内置上百种网页功能组件\n满足通用场景需求'
                                                        ),
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/表格.svg',
                                                        style={
                                                            'height': '2.5rem',
                                                            'transform': 'translateY(15px)',
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '丰富的表格功能'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        [
                                                            translator.t(
                                                                '内置功能强大的表格组件'
                                                            ),
                                                            html.A(
                                                                'AntdTable',
                                                                href='/AntdTable-basic',
                                                                target='_blank',
                                                            ),
                                                            translator.t(
                                                                '\n充分展示交互表格数据'
                                                            ),
                                                        ],
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/结构树.svg',
                                                        style={
                                                            'height': '2.5rem',
                                                            'transform': 'translateY(15px)',
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '强大的树形控件'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        [
                                                            translator.t(
                                                                '内置功能强大的树形控件'
                                                            ),
                                                            html.A(
                                                                'AntdTree',
                                                                href='/AntdTree',
                                                                target='_blank',
                                                            ),
                                                            translator.t(
                                                                '\n树形结构交互展示能力拉满'
                                                            ),
                                                        ],
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/MBE风格多色图标-时间.svg',
                                                        style={
                                                            'height': '4rem'
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '实用的日期选择器'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        [
                                                            translator.t(
                                                                '内置日期及日期范围选择组件\n'
                                                            ),
                                                            html.A(
                                                                'AntdDatePicker',
                                                                href='/AntdDatePicker',
                                                                target='_blank',
                                                            ),
                                                            translator.t('、'),
                                                            html.A(
                                                                'AntdDateRangePicker',
                                                                href='/AntdDateRangePicker',
                                                                target='_blank',
                                                            ),
                                                            translator.t(
                                                                '\n可灵活配置使用策略'
                                                            ),
                                                        ],
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/MBE风格多色图标-文档.svg',
                                                        style={
                                                            'height': '4rem'
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '便捷的表单功能'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        [
                                                            translator.t(
                                                                '基于内置表单整合组件\n'
                                                            ),
                                                            html.A(
                                                                'AntdForm',
                                                                href='/AntdForm',
                                                                target='_blank',
                                                            ),
                                                            translator.t('、'),
                                                            html.A(
                                                                'AntdFormItem',
                                                                href='/AntdFormItem',
                                                                target='_blank',
                                                            ),
                                                            translator.t(
                                                                '\n轻松构建整张表单'
                                                            ),
                                                        ],
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/翻译.svg',
                                                        style={
                                                            'height': '4rem'
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '支持中英双语言'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        translator.t(
                                                            '内置各组件文案信息支持在\n简体中文与英文之间进行设置切换'
                                                        ),
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                            fac.AntdCol(
                                html.Div(
                                    [
                                        fac.AntdSpace(
                                            [
                                                html.Div(
                                                    html.Img(
                                                        src='assets/imgs/index/应用.svg',
                                                        style={
                                                            'height': '3rem',
                                                            'transform': 'translateY(10px)',
                                                        },
                                                    ),
                                                    style={'height': '4rem'},
                                                ),
                                                fac.AntdText(
                                                    translator.t(
                                                        '联动更多组件库'
                                                    ),
                                                    style={
                                                        'fontSize': 20,
                                                        'whiteSpace': 'nowrap',
                                                    },
                                                ),
                                                html.Div(
                                                    fac.AntdText(
                                                        [
                                                            translator.t(
                                                                '高效联动feffery-components生态中\n'
                                                            ),
                                                            html.A(
                                                                'fuc',
                                                                href='https://fuc.feffery.tech/',
                                                                target='_blank',
                                                            ),
                                                            translator.t('、'),
                                                            html.A(
                                                                'fmc',
                                                                href='https://fmc.feffery.tech/',
                                                                target='_blank',
                                                            ),
                                                            translator.t(
                                                                '等组件库，实现更多功能'
                                                            ),
                                                        ],
                                                        style={
                                                            'color': '#697b8c',
                                                            'whiteSpace': 'pre',
                                                        },
                                                    ),
                                                    style={
                                                        'textAlign': 'center'
                                                    },
                                                ),
                                            ],
                                            direction='vertical',
                                            align='center',
                                            style={'width': 175},
                                        )
                                    ],
                                    className='hover-shadow-box',
                                    style={
                                        'height': 220,
                                        'borderRadius': 6,
                                        'position': 'relative',
                                        'display': 'flex',
                                        'alignItems': 'center',
                                        'justifyContent': 'center',
                                    },
                                ),
                                xs=24,
                                sm=24,
                                md=12,
                                lg=12,
                                xl=12,
                                xxl=6,
                            ),
                        ],
                        gutter=[25, 25],
                        style={'padding': '75px 0'},
                    ),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('🛫', style={'fontSize': '26px'}),
                            fac.AntdText(
                                translator.t('版本'),
                                strong=True,
                                style={'fontSize': '26px'},
                            ),
                        ],
                        id=translator.t('版本'),
                    ),
                    html.Ul(
                        [
                            html.Li(
                                fac.AntdParagraph(
                                    [
                                        fac.AntdText(
                                            translator.t('pypi最新稳定版本：')
                                        ),
                                        fac.AntdTag(content=fac.__version__),
                                        html.Img(
                                            src='https://img.shields.io/pypi/v/feffery-antd-components.svg?color=dark-green',
                                            style={
                                                'height': 20,
                                                'transform': 'translateY(5px)',
                                            },
                                        ),
                                    ]
                                ),
                                style={'listStyleType': 'circle'},
                            )
                        ]
                    ),
                    fac.AntdParagraph(
                        [
                            fac.AntdText('📦', style={'fontSize': '26px'}),
                            fac.AntdText(
                                translator.t('安装'),
                                strong=True,
                                style={'fontSize': '26px'},
                            ),
                        ],
                        id=translator.t('安装'),
                    ),
                    fac.AntdTitle(translator.t('最新稳定版本：'), level=5),
                    fac.AntdText(
                        f'pip install feffery-antd-components=={fac.__version__}',
                        keyboard=True,
                        copyable=True,
                    ),
                    fac.AntdTitle(translator.t('最新预发布版本：'), level=5),
                    fac.AntdText(
                        'pip install feffery-antd-components --pre -U',
                        keyboard=True,
                        copyable=True,
                    ),
                    *(
                        [
                            fac.AntdDivider(),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText(
                                        '🎩', style={'fontSize': '26px'}
                                    ),
                                    fac.AntdText(
                                        '加入交流群',
                                        strong=True,
                                        style={'fontSize': '26px'},
                                    ),
                                ],
                                id='加入交流群',
                            ),
                            fac.AntdCollapse(
                                html.Div(
                                    fac.AntdImage(
                                        src=app.get_asset_url(
                                            'imgs/index/feffery-添加好友二维码.jpg'
                                        ),
                                        style={
                                            'width': '300px',
                                            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
                                            'borderRadius': '5px',
                                        },
                                    ),
                                    style={
                                        'display': 'flex',
                                        'justifyContent': 'center',
                                    },
                                ),
                                title='微信扫码添加好友，备注【dash学习】',
                                isOpen=True,
                                ghost=True,
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText(
                                        '👉', style={'fontSize': '26px'}
                                    ),
                                    fac.AntdText(
                                        '玩转dash公众号',
                                        strong=True,
                                        style={'fontSize': '26px'},
                                    ),
                                ],
                                id='玩转dash公众号',
                            ),
                            fac.AntdCollapse(
                                html.Div(
                                    fac.AntdImage(
                                        src=app.get_asset_url(
                                            'imgs/index/玩转dash公众号.png'
                                        ),
                                        style={
                                            'height': '300px',
                                            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
                                            'borderRadius': '5px',
                                        },
                                    ),
                                    style={
                                        'display': 'flex',
                                        'justifyContent': 'center',
                                    },
                                ),
                                title='扫码关注我的知识分享公众号【玩转dash】',
                                isOpen=True,
                                ghost=True,
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText(
                                        '🌏', style={'fontSize': '26px'}
                                    ),
                                    fac.AntdText(
                                        '玩转dash知识星球',
                                        strong=True,
                                        style={'fontSize': '26px'},
                                    ),
                                ],
                                id='玩转dash知识星球',
                            ),
                            fac.AntdCollapse(
                                html.Div(
                                    fac.AntdImage(
                                        src=app.get_asset_url(
                                            'imgs/index/玩转dash星球二维码.jpg'
                                        ),
                                        style={
                                            'width': '300px',
                                            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
                                            'borderRadius': '5px',
                                        },
                                    ),
                                    style={
                                        'display': 'flex',
                                        'justifyContent': 'center',
                                    },
                                ),
                                title='更多dash高级知识技巧及海量应用案例模板，欢迎加入我的知识星球【玩转dash】',
                                isOpen=True,
                                ghost=True,
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText(
                                        '💪', style={'fontSize': '26px'}
                                    ),
                                    fac.AntdText(
                                        '赞助支持',
                                        strong=True,
                                        style={'fontSize': '26px'},
                                    ),
                                ],
                                id='赞助支持',
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText('　　fac', strong=True),
                                    fac.AntdText(
                                        '是我为了方便日常工作需要，逐渐积累优化从而开发并开源出的一个完整的框架，'
                                        '它给予了我很多工作上的便捷，帮助我完成了很多以前无法实现，或实现起来较麻烦的功能和想法，'
                                        '希望也可以帮助到你。'
                                    ),
                                ]
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText(
                                        '　　作为一个开源项目，'
                                        '任何人都可以以任何形式，免费使用它，来打造你心中理想的'
                                        'web应用，如果你有意愿为我分担有关服务器等开销，亦或是赞助鼓励我对于'
                                    ),
                                    fac.AntdText('fac', strong=True),
                                    fac.AntdText(
                                        '过去已做出以及未来将要做出的贡献，可以微信扫一扫下方“赞助二维码”随意赞助，感谢支持。'
                                    ),
                                ]
                            ),
                            fac.AntdCollapse(
                                html.Div(
                                    fac.AntdImage(
                                        src=app.get_asset_url(
                                            'imgs/index/weixin-pay.png'
                                        ),
                                        style={
                                            'width': '300px',
                                            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
                                            'borderRadius': '5px',
                                        },
                                    ),
                                    style={
                                        'display': 'flex',
                                        'justifyContent': 'center',
                                    },
                                ),
                                title='赞助二维码',
                                isOpen=True,
                                ghost=True,
                            ),
                        ]
                        if current_locale == 'zh-cn'
                        else []
                    ),
                    html.Div(style={'height': '200px'}),
                ],
                style={'flex': 'auto'},
            ),
            html.Div(
                fac.AntdAnchor(
                    linkDict=[
                        {'title': '🐣' + translator.t('简介'), 'href': '#🐣'},
                        {
                            'title': '🤩' + translator.t('特性'),
                            'href': '#' + translator.t('特性'),
                        },
                        {
                            'title': '🛫' + translator.t('版本'),
                            'href': '#' + translator.t('版本'),
                        },
                        {
                            'title': '📦' + translator.t('安装'),
                            'href': '#' + translator.t('安装'),
                        },
                        *(
                            [
                                {
                                    'title': '🎩加入交流群',
                                    'href': '#加入交流群',
                                },
                                {
                                    'title': '👉玩转dash公众号',
                                    'href': '#玩转dash公众号',
                                },
                                {
                                    'title': '🌏玩转dash知识星球',
                                    'href': '#玩转dash知识星球',
                                },
                                {'title': '💪赞助支持', 'href': '#赞助支持'},
                            ]
                            if current_locale == 'zh-cn'
                            else []
                        ),
                    ],
                    offsetTop=65,
                ),
                style={'flex': 'none'},
            ),
        ],
        style={'display': 'flex', 'padding': 25},
    )

```

## `views/getting_started.py`
```python
from dash import html
from functools import partial
import feffery_antd_components as fac
import feffery_markdown_components as fmc
from dash.dependencies import Component

from i18n import translator, get_current_locale
from utils.doc_renderer import MarkdownRenderer

md_renderer = MarkdownRenderer()


def render() -> Component:
    """渲染“Dash+fac快速上手”文档页"""

    t = partial(translator.t, locale_topic='getting_started')
    current_locale = get_current_locale()

    return html.Div(
        [
            fac.AntdBackTop(),
            html.Div(
                [
                    fac.AntdTitle(t('环境搭建'), id='环境搭建', level=3),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                '在基于**Dash**和**fac**进行应用开发之前，我们需要先搭建好所需的环境，推荐使用**conda**或**mamba**作为环境管理工具，这里以Python 3.10版本为例，在终端执行下列命令进行相关环境的创建及激活：'
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    (
                        fac.AntdParagraph(
                            [
                                fac.AntdText(
                                    '注：由于国内pypi相关镜像的更新延迟，通过其进行相关库的安装，版本可能滞后于原始pypi中的最新版本'
                                )
                            ],
                            style={'textIndent': '2rem'},
                        )
                        if current_locale == 'zh-cn'
                        else None
                    ),
                    fac.AntdTabs(
                        items=[
                            {
                                'label': t('默认方式'),
                                'key': t('默认方式'),
                                'children': html.Div(
                                    [
                                        fmc.FefferySyntaxHighlighter(
                                            codeString="""conda create -n dash-apps python=3.10 -y
conda activate dash-apps""",
                                            language='bash',
                                            showCopyButton=True,
                                        )
                                    ]
                                ),
                            },
                            *(
                                [
                                    {
                                        'label': '国内使用镜像',
                                        'key': '国内使用镜像',
                                        'children': html.Div(
                                            [
                                                fmc.FefferySyntaxHighlighter(
                                                    codeString="""conda create -n dash-apps python=3.10 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main -y
conda activate dash-apps""",
                                                    language='bash',
                                                    showCopyButton=True,
                                                )
                                            ]
                                        ),
                                    }
                                ]
                                if current_locale == 'zh-cn'
                                else []
                            ),
                        ]
                    ),
                    fac.AntdParagraph(
                        t(
                            '完成环境的创建及激活后，我们在对应环境中直接通过pip进行相关基础依赖库的安装即可：'
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdTabs(
                        items=[
                            {
                                'label': t('默认方式'),
                                'key': t('默认方式'),
                                'children': html.Div(
                                    [
                                        fmc.FefferySyntaxHighlighter(
                                            codeString="""pip install dash feffery-antd-components -U""",
                                            language='bash',
                                            showCopyButton=True,
                                        )
                                    ]
                                ),
                            },
                            *(
                                [
                                    {
                                        'label': '国内使用镜像',
                                        'key': '国内使用镜像',
                                        'children': html.Div(
                                            [
                                                fmc.FefferySyntaxHighlighter(
                                                    codeString="""pip install dash feffery-antd-components -U -i https://pypi.tuna.tsinghua.edu.cn/simple""",
                                                    language='bash',
                                                    showCopyButton=True,
                                                )
                                            ]
                                        ),
                                    }
                                ]
                                if current_locale == 'zh-cn'
                                else []
                            ),
                        ]
                    ),
                    fac.AntdTitle(
                        t('构建示例应用'), id='构建示例应用', level=3
                    ),
                    fac.AntdParagraph(
                        t(
                            '完成前面所述的环境部署后，下面我们来开发一个简单的小应用，实现根据用户输入的目标值和实际值来生成对应的环形进度条，操作效果如下面动图所示：'
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    html.Div(
                        fac.AntdImage(
                            src=(
                                'assets/imgs/getting_started/dash+fac上手示例应用.gif'
                                if current_locale == 'zh-cn'
                                else 'assets/imgs/getting_started/dash+fac上手示例应用_en-us.gif'
                            ),
                            preview=False,
                        ),
                        style={'textAlign': 'center'},
                    ),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                '对应代码如下，在激活对应环境的前提下，终端执行`python app.py`即可启动该示例应用：'
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdTabs(
                        tabBarRightExtraContent=fac.AntdSpace(
                            [
                                html.Img(
                                    src='/assets/imgs/pycafe_logo.png',
                                    height=28,
                                ),
                                fac.AntdTooltip(
                                    fac.AntdButton(
                                        (
                                            '在Py.Cafe中实时编辑'
                                            if current_locale == 'zh-cn'
                                            else 'Edit live on Py.Cafe'
                                        ),
                                        type='link',
                                        href=(
                                            'https://py.cafe/CNFeffery/fac-getting-started-demo-zh-cn'
                                            if current_locale == 'zh-cn'
                                            else 'https://py.cafe/CNFeffery/fac-getting-started-demo-en-us'
                                        ),
                                        style={'padding': '4px 2px'},
                                    ),
                                    title=(
                                        '国内用户建议开启代理，以加速访问Py.Cafe'
                                        if current_locale == 'zh-cn'
                                        else None
                                    ),
                                ),
                            ],
                            size=0,
                            align='center',
                        ),
                        items=[
                            {
                                'label': 'app.py',
                                'key': 'app.py',
                                'children': fmc.FefferySyntaxHighlighter(
                                    codeString=(
                                        """
import dash
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Input, Output

# 实例化Dash应用对象
app = dash.Dash(__name__)

# 添加初始化页面内容
app.layout = html.Div(
    fac.AntdCard(
        [
            # 输入表单
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInputNumber(id="target-value", style={"width": "100%"}),
                        label="目标值",
                    ),
                    fac.AntdFormItem(
                        fac.AntdInputNumber(id="actual-value", style={"width": "100%"}),
                        label="实际值",
                    ),
                ],
                layout="inline",
                style={"marginBottom": 25, "width": "100%"},
            ),
            # 输出目标容器
            html.Div(
                id="output-container",
                style={
                    # 基于css中的flex布局实现水平垂直居中
                    "width": "100%",
                    "display": "flex",
                    "justifyContent": "center",
                    "alignItems": "center",
                },
            ),
        ],
        title="dash+fac应用示例",
        hoverable=True,
        style={
            # 这里利用到css中的fixed布局
            "position": "fixed",
            "top": "40%",
            "left": "50%",
            "transform": "translate(-50%, -50%)",
            "width": 560,
            "height": 350,
        },
    )
)


# 定义回调函数串起相关交互逻辑
@app.callback(
    Output("output-container", "children"),
    [Input("target-value", "value"), Input("actual-value", "value")],
)
def handle_progress_render(target_value, actual_value):
    # 判断传入的目标值和实际值是否有效
    if target_value and actual_value:
        return fac.AntdProgress(
            percent=round(100 * actual_value / target_value, 2), type="dashboard"
        )

    return fac.AntdResult(subTitle="请输入有效的目标值和实际值", status="warning")


if __name__ == "__main__":
    app.run(debug=False)
"""
                                        if current_locale == 'zh-cn'
                                        else """
import dash
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Input, Output

# Instantiate the Dash application object
app = dash.Dash(__name__)

# Add initial page content
app.layout = html.Div(
    fac.AntdCard(
        [
            # Input form
            fac.AntdForm(
                [
                    fac.AntdFormItem(
                        fac.AntdInputNumber(id="target-value", style={"width": "100%"}),
                        label="Target Value",
                    ),
                    fac.AntdFormItem(
                        fac.AntdInputNumber(id="actual-value", style={"width": "100%"}),
                        label="Actual Value",
                    ),
                ],
                layout="inline",
                style={"marginBottom": 25, "width": "100%"},
            ),
            # Output target container
            html.Div(
                id="output-container",
                style={
                    # Using flex layout from CSS for center alignment
                    "width": "100%",
                    "display": "flex",
                    "justifyContent": "center",
                    "alignItems": "center",
                },
            ),
        ],
        title="Dash + FAC Application Example",
        hoverable=True,
        style={
            # Using fixed layout from CSS
            "position": "fixed",
            "top": "40%",
            "left": "50%",
            "transform": "translate(-50%, -50%)",
            "width": 630,
            "height": 350,
        },
    )
)


# Define callback function to connect interaction logic
@app.callback(
    Output("output-container", "children"),
    [Input("target-value", "value"), Input("actual-value", "value")],
)
def handle_progress_render(target_value, actual_value):
    # Check if the input target and actual values are valid
    if target_value and actual_value:
        return fac.AntdProgress(
            percent=round(100 * actual_value / target_value, 2), type="dashboard"
        )

    return fac.AntdResult(
        subTitle="Please enter valid target and actual values", status="warning"
    )


if __name__ == "__main__":
    app.run(debug=False)
"""
                                    ),
                                    language='python',
                                    showCopyButton=True,
                                    codeBlockStyle={'height': 600},
                                ),
                            }
                        ],
                    ),
                    *(
                        [
                            fac.AntdDivider(isDashed=True),
                            fac.AntdTitle('拓展阅读', id='拓展阅读', level=3),
                            fac.AntdSpace(
                                [
                                    html.A(
                                        fac.AntdCard(
                                            title='10分钟极速入门dash应用开发',
                                            coverImg={
                                                'src': 'assets/imgs/getting_started/cover_10分钟极速入门dash应用开发.png',
                                                'style': {
                                                    'width': 275,
                                                    'height': 325,
                                                    'objectFit': 'cover',
                                                },
                                            },
                                            hoverable=True,
                                            styles={'body': {'padding': 0}},
                                        ),
                                        href='https://mp.weixin.qq.com/s/BvGJT7DPHP2dYExZgifgiw',
                                        target='_blank',
                                    ),
                                    html.A(
                                        fac.AntdCard(
                                            title='Dash应用页面整体布局技巧',
                                            coverImg={
                                                'src': 'assets/imgs/getting_started/cover_Dash应用页面整体布局技巧.png',
                                                'style': {
                                                    'width': 275,
                                                    'height': 325,
                                                    'objectFit': 'cover',
                                                },
                                            },
                                            hoverable=True,
                                            styles={'body': {'padding': 0}},
                                        ),
                                        href='https://mp.weixin.qq.com/s/6Ee1FpCyjlHU4W3JjoL8sQ',
                                        target='_blank',
                                    ),
                                    html.A(
                                        fac.AntdCard(
                                            title=fac.AntdText(
                                                '在Dash应用中更灵活地编写回调函数',
                                                style={'fontSize': '13px'},
                                            ),
                                            coverImg={
                                                'src': 'assets/imgs/getting_started/cover_在Dash应用中更灵活地编写回调函数.png',
                                                'style': {
                                                    'width': 275,
                                                    'height': 325,
                                                    'objectFit': 'cover',
                                                },
                                            },
                                            hoverable=True,
                                            styles={'body': {'padding': 0}},
                                            style={'width': 275},
                                        ),
                                        href='https://mp.weixin.qq.com/s/IJGeAz5V8jqrtoVm3vHcUw',
                                        target='_blank',
                                    ),
                                    html.A(
                                        fac.AntdCard(
                                            title=fac.AntdText(
                                                'Dash应用浏览器端回调常用方法总结',
                                                style={'fontSize': '13px'},
                                            ),
                                            coverImg={
                                                'src': 'assets/imgs/getting_started/cover_Dash应用浏览器端回调常用方法总结.jpg',
                                                'style': {
                                                    'width': 275,
                                                    'height': 325,
                                                    'objectFit': 'cover',
                                                },
                                            },
                                            hoverable=True,
                                            styles={'body': {'padding': 0}},
                                            style={'width': 275},
                                        ),
                                        href='https://mp.weixin.qq.com/s/WjhrxBuS_xL-kBkBEK2GCg',
                                        target='_blank',
                                    ),
                                ],
                                size='large',
                                wrap=True,
                            ),
                            fac.AntdDivider(isDashed=True),
                            fac.AntdTitle(
                                '更多dash专业知识',
                                id='更多dash专业知识',
                                level=3,
                            ),
                            fac.AntdParagraph(
                                [
                                    fac.AntdText('fac', strong=True),
                                    '中有超过100种具有不同功能特点的组件，你可以通过左侧菜单栏浏览它们各自的文档说明和使用示例，从而组合构建出具有任意功能的',
                                    fac.AntdText('dash', strong=True),
                                    '应用✨。',
                                ],
                                style={'textIndent': '2rem'},
                            ),
                            fac.AntdParagraph(
                                [
                                    '同时我也在持续运营名为',
                                    fac.AntdText('玩转dash', italic=True),
                                    '的知识星球学习社区，目前已经更新了数套系统性的',
                                    fac.AntdText('dash', strong=True),
                                    '应用开发教程，以及围绕',
                                    fac.AntdText('dash', strong=True),
                                    '应用开发相关的各种前沿知识和使用技巧，是国内最专业的',
                                    fac.AntdText('dash', strong=True),
                                    '应用知识社区，如果你对此感兴趣，欢迎扫描下方二维码加入我的学习社区：',
                                ],
                                style={'textIndent': '2rem'},
                            ),
                            html.Div(
                                fac.AntdImage(
                                    src='assets/imgs/index/玩转dash星球二维码.jpg',
                                    style={'height': 450},
                                ),
                                style={'textAlign': 'center'},
                            ),
                        ]
                        if current_locale == 'zh-cn'
                        else []
                    ),
                ],
                style={'flex': 'auto'},
            ),
            html.Div(
                fac.AntdAnchor(
                    linkDict=[
                        {'title': t('环境搭建'), 'href': '#环境搭建'},
                        {'title': t('构建示例应用'), 'href': '#构建示例应用'},
                        *(
                            [
                                {'title': '拓展阅读', 'href': '#拓展阅读'},
                                {
                                    'title': '更多dash专业知识',
                                    'href': '#更多dash专业知识',
                                },
                            ]
                            if current_locale == 'zh-cn'
                            else []
                        ),
                    ],
                    offsetTop=65,
                ),
                style={'flex': 'none'},
            ),
        ],
        style={'display': 'flex', 'padding': 25},
    )

```

## `views/version_migration_guide.py`
```python
from dash import html
from functools import partial
import feffery_antd_components as fac
from dash.dependencies import Component

from i18n import translator
from utils.doc_renderer import MarkdownRenderer

md_renderer = MarkdownRenderer()


def render() -> Component:
    """渲染“版本迁移指南”文档页"""

    t = partial(translator.t, locale_topic='version_migration_guide')

    return html.Div(
        [
            fac.AntdBackTop(),
            html.Div(
                [
                    fac.AntdTitle(
                        t('从0.3到0.4版本'), id='从0.3到0.4版本', level=2
                    ),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                '`fac`从`0.3`版本迁移到`0.4`版本，除了新增的大量功能外，还需要注意少量组件的参数调整情况，具体如下：'
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdTitle(t('AntdCard移除bordered参数'), level=4),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                "跟随底层`Antd`框架的变化，`AntdCard`移除了`bordered`参数，请改为设置`variant='borderless'`代替。"
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdTitle(
                        t(
                            '部分组件xxxStyle、xxxClassName格式参数重构到styles、classNames参数中'
                        ),
                        level=4,
                    ),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                '跟随底层`Antd`框架的变化，相关参数重构至语义化结构参数`styles`、`classNames`对应字段中，具体涉及组件及参数见[0.4.0更新日志](/changelog-0.4.0)中的**变化**章节。'
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                    fac.AntdTitle(
                        t('AntdAvatarGroup部分参数重构到max参数中'),
                        level=4,
                    ),
                    fac.AntdParagraph(
                        md_renderer.render(
                            t(
                                '跟随底层`Antd`框架的变化，AntdAvatarGroup部分参数重构至`max`参数中，具体涉及组件及参数见[0.4.0更新日志](/changelog-0.4.0)中的**变化**章节。'
                            )
                        ),
                        style={'textIndent': '2rem'},
                    ),
                ],
                style={'flex': 'auto'},
            ),
            html.Div(
                fac.AntdAnchor(
                    linkDict=[
                        {
                            'title': t('从0.3到0.4版本'),
                            'href': '#从0.3到0.4版本',
                        },
                    ],
                    offsetTop=65,
                ),
                style={'flex': 'none'},
            ),
        ],
        style={'display': 'flex', 'padding': 25},
    )

```
