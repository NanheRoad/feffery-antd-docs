

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- mode (a value equal to: 'text', 'icon', 'image'; default 'icon'):
    头像模式，可选项有`'text'`、`'icon'`、`'image'`  默认值：`'icon'`.

- gap (number; default 4):
    `mode='text'`时，设置字符距离左右两侧边界的像素距离  默认值：`4`.

- text (string; optional):
    `mode='text'`时，设置文字内容.

- icon (string; optional):
    `mode='icon'`时，设置图标，同**AntdIcon**的`icon`参数.

- iconRenderer (a value equal to: 'AntdIcon', 'fontawesome'; default 'AntdIcon'):
    `mode='icon'`时，设置图标渲染方式，可选项有`'AntdIcon'`、`'fontawesome'`.

- alt (string; optional):
    `mode='image'`时，设置图像无法显示时的占位文字.

- src (string; optional):
    `mode='image'`时，设置图片地址.

- srcSet (string; optional):
    `mode='image'`时，设置图片base64地址.

- draggable (boolean | a value equal to: 'true', 'false'; optional):
    `mode='image'`时，设置图片是否允许拖拽.

- crossOrigin (a value equal to: 'anonymous', 'use-credentials', ''; optional):
    `mode='image'`时，设置图片的CORS属性，可选项有`'anonymous'`、`'use-credentials'`、`''`.

- size (dict; optional):
    配置头像尺寸，可传入数值型代表像素尺寸（支持响应式），或传入字符型使用预设尺寸规格，可选项有`'large'`、`'small'`、`'default'`.

    `size` is a number | a value equal to: 'large', 'small', 'default'
    | dict with keys:

    - xs (number; optional)

    - sm (number; optional)

    - md (number; optional)

    - lg (number; optional)

    - xl (number; optional)

    - xxl (number; optional)

- shape (a value equal to: 'circle', 'square'; default 'circle'):
    头像形状，可选项有`'circle'`、`'square'`  默认值：`'circle'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.