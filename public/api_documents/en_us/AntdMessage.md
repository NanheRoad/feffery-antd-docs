

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string; optional):
    当前组件css类名.

- content (string; optional):
    提示信息内容.

- type (a value equal to: 'default', 'success', 'error', 'info', 'warning'; default 'default'):
    提示信息类型，可选项有`'default'`、`'success'`、`'error'`、`'info'`、`'warning'`
    默认值：'default'.

- duration (number; default 3):
    提示信息自动消失对应的延时，单位：秒，设置为`0`时不会自动消失  默认值：`3`.

- top (number; default 8):
    提示信息距离顶端的像素距离  默认值：`8`.

- maxCount (number; optional):
    最多允许同时出现的提示信息数量.

- icon (string; optional):
    自定义前缀图标，同`AntdIcon`的`icon`参数.

- iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; default 'AntdIcon'):
    自定义前缀图标渲染方式，可选项有`'AntdIcon'`、`'fontawesome'`.