

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，定义走马灯中需要轮播的若干元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- arrows (boolean; default False):
    是否显示箭头  默认值：`False`.

- autoplay (dict; default False):
    是否自动轮播，可传入字典型进行更多配置  默认值：`False`.

    `autoplay` is a boolean | dict with keys:

    - dotDuration (boolean; optional):
        是否展示指示点进度条.

- dotPosition (a value equal to: 'top', 'bottom', 'left', 'right'; default 'bottom'):
    面板指示器位置，可选项有`'top'`、`'bottom'`、`'left'`、`'right'`  默认值：`'bottom'`.

- easing (string; default 'linear'):
    调整动画效果，同css中的`animation-timing-function`  默认值：'linear'.

- effect (a value equal to: 'scrollx', 'fade'; default 'scrollx'):
    动化效果，可选项有`'scrollx'`、`'fade'`  默认值：'scrollx'.

- autoplaySpeed (number; default 3000):
    轮播间隔时长，单位：毫秒  默认值：`3000`.

- speed (number; default 500):
    轮播动画耗时，单位：毫秒  默认值：`500`.

- pauseOnHover (boolean; default False):
    是否在鼠标悬停时暂停轮播  默认值：`False`.

- infinite (boolean; default True):
    是否启用无限循环轮播  默认值：`True`.

- lazyLoad (boolean; default False):
    是否针对走马灯中的子项实施懒加载效果  默认值：`False`.

- slidesToShow (number; default 1):
    同时展示的子项数量  默认值：`1`.

- slidesToScroll (number; default 1):
    一次轮播划过的子项数量  默认值：`1`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.