

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- value (string; optional):
    二维码解析结果.

- type (a value equal to: 'canvas', 'svg'; default 'canvas'):
    渲染方式，可选项有`'canvas'`、`'svg'`  默认值：`'canvas'`.

- icon (string; optional):
    二维码内嵌图片地址.

- size (number; default 160):
    二维码像素边长  默认值：`160`.

- iconSize (dict; default 40):
    二维码内嵌图片像素边长  默认值：`40`.

    `iconSize` is a number | dict with keys:

    - width (number; optional)

    - height (number; optional)

- color (string; default '#000'):
    二维码颜色  默认值：`'#000'`.

- bgColor (string; default 'transparent'):
    二维码背景颜色  默认值：`'transparent'`.

- bordered (boolean; default True):
    二维码是否渲染边框  默认值：`True`.

- errorLevel (a value equal to: 'L', 'M', 'Q', 'H'; default 'M'):
    二维码纠错级别，可选项有`'L'`、`'M'`、`'Q'`、`'H'`  默认值：`'M'`.

- status (a value equal to: 'active', 'expired', 'loading', 'scanned'; default 'active'):
    二维码状态，可选项有`'active'`、`'expired'`、`'loading'`、`'scanned'`
    默认值：`'active'`.

- expires (number; optional):
    当前二维码过期时间，单位：秒，到期后二维码状态将会被强制更新为`'expired'`.

- autoSpin (boolean; default False):
    是否在`value`处于回调更新中时，自动切换为`loading`状态  默认值：`False`.

- refreshClicks (number; default 0):
    监听当前"点击刷新"按钮累计点击次数，仅在`status`为`'expired'`时有效  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.