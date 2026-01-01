

- id (string; optional):
    组件唯一id.

- children (a list of or a singular dash component, string or number; optional):
    传入内部嵌套的评论组件.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- commentId (string; optional):
    评论唯一id，可用于数据库匹配等场景.

- authorName (string; optional):
    评论发布用户名.

- authorNameHref (string; optional):
    评论发布用户名附带链接地址.

- publishTime (dict; required):
    必填，配置发布日期时间相关参数.

    `publishTime` is a dict with keys:

    - value (string; required):
        必填，日期时间字符串.

    - format (string; optional):
        与日期时间字符串匹配的格式.

- fromNow (boolean; default False):
    是否以相对时间格式呈现发布日期时间.

- showLikeDislike (boolean; default True):
    是否显示“支持/反对”按钮  默认值：`True`.

- showReply (boolean; default True):
    是否显示“添加回复”按钮  默认值：`True`.

- showDelete (boolean; default False):
    是否显示“删除”按钮  默认值：`False`.

- replyClicks (number; default 0):
    监听“添加回复”按钮累计点击次数  默认值：`0`.

- deleteClicks (number; default 0):
    监听“删除”按钮累计点击次数  默认值：`0`.

- commentContent (a list of or a singular dash component, string or number; optional):
    组件型，评论正文内容.

- likesCount (number; default 0):
    监听或设置“支持”次数.

- dislikesCount (number; default 0):
    监听或设置“反对”次数.

- action (a value equal to: 'liked', 'disliked', 'default'; optional):
    监听或设置当前评论“支持/反对”状态，可选项有`'liked'`、`'disliked'`、`'default'`
    默认值：`'default'`.

- defaultAction (a value equal to: 'liked', 'disliked', 'default'; optional):
    设置当前评论初始化时的“支持/反对”状态，可选项有`'liked'`、`'disliked'`、`'default'`.

- avatarProps (dict; optional):
    配置评论用户头像，同`AntdAvatar`.

- popupContainer (a value equal to: 'parent', 'body'; default 'body'):
    相关展开层锚定策略，可选项有`'parent'`、`'body'`  默认值：`'body'`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- loading_state (dict; optional)

    `loading_state` is a dict with keys:

    - is_loading (boolean; optional):
        Determines if the component is loading or not.

    - prop_name (string; optional):
        Holds which property is loading.

    - component_name (string; optional):
        Holds the name of the component that is loading.