# API Document

这是中国海洋大学 2021 年软件工程综合实践课夕夕项目的接口文档。

## 总体

以下为对所有接口的总体概述

### 域名

域名为 [https://weparallelines.top](https://weparallelines.top/)

**注意：** 使用 HTTPS

### 接口格式

接口的请求格式一般为 JSON 格式，少数为 MultiForm 格式。

接口的响应格式为 JSON 格式。

### 响应字段

响应字段必定包含**状态码 code** 和**状态信息 msg**。

其他额外字段均包含在**数据 data** 字段中。

**注意：** 以下所有接口的响应字段除 code 和 msg 字段均在 data 字段中，为了书写文档简便其他字段与 code 和 msg 字段并列。

### 响应状态码和状态信息

响应状态码 code 和状态信息 msg 一一对应，无重复。

> 20000: 成功
> 50403: Forbidden
> 50000: 意外错误
> 40000: 请求方法错误
> 40001: JSON 解析错误
> 40002: 缺少参数
> 40003: 参数错误
> 41001: 不支持当前图片格式
> 42001: 用户名应不少于 4 位
> 42002: 用户名应不多于 20 位
> 42003: 用户名仅能含有字母、数字和下划线
> 42004: 密码应不少于 6 位
> 42005: 密码应不多于 20 位
> 42006: 密码应仅包含合法字符
> 42007: 密码必须包含数字
> 42008: 密码必须包含字母
> 42009: 邮箱格式错误
> 42010: 用户名已存在
> 42011: 邮箱已存在
> 42012: 用户名不存在
> 42013: 密码错误
> 42014: 验证码不匹配
> 43001: 未登陆
> 43002: 权限不足
> 44001: 已在购物车

## 接口

### 上传图片

**接口功能**

> 上传图片

**URL**

> /api/upload

**请求方式**

> POST

**请求格式**

> MultiForm

**请求字段**

> | 参数  | 必选 | 类型   | 说明                                 |
> | :---- | :--- | :----- | ------------------------------------ |
> | img   | true | file   | 图片文件（jpg、png）                 |

**响应格式**

>JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |
> | path     | string   | 图片路径 |

**示例**

```json
// request MultiForm
{
  "img": "file",
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "path": "/media/20210430135155wJ6YykfxBe.jpg"
    }
}
```

----

### 获取验证码

**接口功能**

> 获取验证码

**URL**

> /api/verification_code

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数  | 必选  | 类型    | 说明                                |
> | :---- | :---- | :------ | ----------------------------------- |
> | email | true  | string  | 邮箱                                |
> | check | false | boolean | 是否检测邮箱未注册（注册需为 true） |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request MultiForm
{
  "email": "example@example.com",
  "check": true
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
}
```

----

### 注册

**接口功能**

> 注册

**URL**

> /api/account/register

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数              | 必选 | 类型   | 说明                       |
> | :---------------- | :--- | :----- | -------------------------- |
> | username          | true | string | 用户名                     |
> | email             | true | string | 邮箱                       |
> | password          | true | string | 密码                       |
> | verification_code | true | string | 验证码（验证接口发至邮箱） |
> | role              | true | string | 角色（0: 买家，1: 卖家）   |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request JSON
{
    "username": "249606097",
    "email": "249606097@qq.com",
    "password": "liu123",
    "verification_code": "585399",
    "role": "0"
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
}
```

----

### 登录

**接口功能**

> 登录（不区分买家和卖家）

**URL**

> /api/account/login

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数     | 必选 | 类型   | 说明        |
> | :------- | :--- | :----- | ----------- |
> | username | true | string | 用户名/邮箱 |
> | password | true | string | 密码        |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request JSON
{
    "username": "249606097",
    "password": "liu123"
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 注销

**接口功能**

> 注销

**URL**

> /api/account/logout

**请求方式**

> POST

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 获取状态

**接口功能**

> 获取状态

**URL**

> /api/account/status

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段   | 字段类型 | 说明                                     |
> | ---------- | -------- | ---------------------------------------- |
> | code       | int      | 状态码                                   |
> | msg        | string   | 状态信息                                 |
> | account_id | int      | 账户 id                                  |
> | login      | boolean  | 是否登录                                 |
> | username   | string   | 用户名                                   |
> | email      | string   | 邮箱                                     |
> | role       | string   | 角色                                     |
> | nickname   | string   | 昵称                                     |
> | avatar     | string   | 头像                                     |
> | balance    | string   | 账户收入（当前为卖家登录时，才有本字段） |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "login": false
    }
}

{
    "code": 20000,
    "msg": "成功",
    "data": {
        "account_id": 1,
        "login": true,
        "username": "249606097",
        "email": "249606097@qq.com",
        "role": "0",
        "nickname": "",
        "avatar": "/media/default.png"
    }
}
```

----

### 修改昵称

**接口功能**

> 修改昵称（要求登录）

**URL**

> /api/account/change_nickname

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数     | 必选 | 类型   | 说明   |
> | :------- | :--- | :----- | ------ |
> | nickname | true | string | 新昵称 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request JSON
{
    "nickname": "123"
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 更换头像

**接口功能**

> 更换头像（要求登录）

**URL**

> /api/account/change_avatar

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数 | 必选 | 类型   | 说明                         |
> | :--- | :--- | :----- | ---------------------------- |
> | path | true | string | 图片路径（上传图片接口给出） |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request JSON
{
    "path": "/media/20210903155523MvMZdsY824.jpg"
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 获取用户基本信息

**接口功能**

> 获取用户基本信息

**URL**

> /api/account/get_account_information

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数       | 必选 | 类型 | 说明    |
> | :--------- | :--- | :--- | ------- |
> | account_id | true |      | 账户 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段   | 字段类型 | 说明     |
> | ---------- | -------- | -------- |
> | code       | int      | 状态码   |
> | msg        | string   | 状态信息 |
> | account_id | int      | 账户 id  |
> | role       | string   | 角色     |
> | nickname   | string   | 昵称     |
> | avatar     | string   | 头像     |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "account_id": 1,
        "role": "0",
        "nickname": "123",
        "avatar": "/media/20210903155523MvMZdsY824.jpg"
    }
}
```

----

### 创建新课程

**接口功能**

> 创建新课程

**URL**

> /api/course/create_new_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数    | 必选 | 类型   | 说明                         |
> | :------ | :--- | :----- | ---------------------------- |
> | title   | true | string | 标题                         |
> | content | true | string | 内容                         |
> | cover   | true | string | 封面路径（上传图片接口给出） |
> | price   | true | string | 价格 形式必须为 X···X.XX     |
> | tags    | true | list   | 选中标签的 id 列表           |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明     |
> | ----------- | -------- | -------- |
> | code        | int      | 状态码   |
> | msg         | string   | 状态信息 |
> | course_id   | int      | 课程 id  |
> | snapshot_id | int      | 快照 id  |

**示例**

```json
// request 
{
    "title": "1111",
    "content": "0000",
    "cover": "/media/20210903155523MvMZdsY824.jpg",
    "price": "10.10",
    "tags": [
        1,
        2
    ]
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "course_id": 1,
        "snapshot_id": 1
    }
}
```

----

### 获取课程详情

**接口功能**

> 获取课程详情

**URL**

> /api/course/get_course_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明                               |
> | ----------- | -------- | ---------------------------------- |
> | code        | int      | 状态码                             |
> | msg         | string   | 状态信息                           |
> | course_id   | int      | 课程 id                            |
> | title       | string   | 课程名                             |
> | seller_id   | int      | 卖家账户 id                        |
> | seller_name | string   | 卖家名                             |
> | published   | boolean  | 是否上架                           |
> | tags        | list     | 标签列表                           |
> | deleted     | boolean  | 是否被删除                         |
> | sales       | int      | 销量                               |
> | snapshot_id | int      | 最新快照 id                        |
> | content     | string   | 内容                               |
> | cover       | string   | 封面                               |
> | price       | string   | 价格 形式为 X···X.XX               |
> | create_time | string   | 创建时间 形式为 XXX-XX-XX XX:XX:XX |

**示例**

```json
// request 


// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "course_id": 1,
        "title": "1111",
        "seller_id": 1,
        "seller_name": "123",
        "published": false,
        "tags": [
            {
                "tag_id": 1,
                "tag_name": "前端"
            },
            {
                "tag_id": 2,
                "tag_name": "后端"
            }
        ],
        "deleted": false,
        "sales": 0,
        "snapshot_id": 1,
        "content": "0000",
        "cover": "/media/20210903155523MvMZdsY824.jpg",
        "price": "10.10",
        "create_time": "2021-09-13 15:17:06"
    }
}
```

----

### 获取快照详情

**接口功能**

> 获取快照详情

**URL**

> /api/course/get_snapshot_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数        | 必选 | 类型 | 说明    |
> | :---------- | :--- | :--- | ------- |
> | snapshot_id | true | int  | 快照 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明                               |
> | ----------- | -------- | ---------------------------------- |
> | code        | int      | 状态码                             |
> | msg         | string   | 状态信息                           |
> | course_id   | int      | 快照对应的当前课程 id              |
> | title       | string   | 快照对应的当前课程课程名           |
> | seller_id   | int      | 卖家账户 id                        |
> | seller_name | string   | 卖家名                             |
> | published   | boolean  | 快照对应的当前课程是否上架         |
> | tags        | list     | 标签列表                           |
> | deleted     | boolean  | 是否被删除                         |
> | sales       | int      | 销量                               |
> | snapshot_id | int      | 当前快照 id                        |
> | content     | string   | 内容                               |
> | cover       | string   | 封面                               |
> | price       | string   | 价格 形式为 X···X.XX               |
> | create_time | string   | 创建时间 形式为 XXX-XX-XX XX:XX:XX |

**示例**

```json
// request 


// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "course_id": 1,
        "title": "1111",
        "seller_id": 1,
        "seller_name": "123",
        "published": false,
        "tags": [
            {
                "tag_id": 1,
                "tag_name": "前端"
            },
            {
                "tag_id": 2,
                "tag_name": "后端"
            }
        ],
        "deleted": false,
        "sales": 0,
        "snapshot_id": 1,
        "content": "0000",
        "cover": "/media/20210903155523MvMZdsY824.jpg",
        "price": "10.10",
        "create_time": "2021-09-13 15:17:06"
    }
}
```

----

### 修改课程

**接口功能**

> 修改课程

**URL**

> /api/course/edit_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型   | 说明     |
> | :-------- | :--- | :----- | -------- |
> | course_id | true | int    | 课程 id  |
> | title     | true | string | 标题     |
> | content   | true | string | 内容     |
> | cover     | true | string | 封面路径 |
> | price     | true | string | 价格     |
> | tags      | true | list   | 标签列表 |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明     |
> | ----------- | -------- | -------- |
> | code        | int      | 状态码   |
> | msg         | string   | 状态信息 |
> | course_id   | int      | 课程 id  |
> | snapshot_id | int      | 快照 id  |

**示例**

```json
// request 
{
    "course_id": "1",
    "title": "1111",
    "content": "0000",
    "cover": "/media/20210903155523MvMZdsY824.jpg",
    "price": "1000.00",
    "tags": [
        1,
        2
    ]
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "course_id": 1,
        "snapshot_id": 2
    }
}
```

----

### 删除课程

**接口功能**

> 删除课程

**URL**

> /api/course/delete_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 上架课程

**接口功能**

> 上架课程

**URL**

> /api/course/publish_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 下架课程

**接口功能**

> 下架课程

**URL**

> /api/course/unpublish_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 上架课程

**接口功能**

> 上架课程

**URL**

> /api/course/publish_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 获取课程列表

**接口功能**

> 获取课程列表
>
> （时间倒序）
>
> （销量倒序）
>
> （被置顶的课程）
>
> （我售卖的）（需卖家登录）

**URL**

> /api/course/get_latest_courses_list
>
> /api/course/get_hottest_courses_list
>
> /api/course/get_pinned_courses_list
>
> /api/course/get_my_courses_list

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明                               |
> | -------- | -------- | ---------------------------------- |
> | code     | int      | 状态码                             |
> | msg      | string   | 状态信息                           |
> | courses  | list     | 课程列表（内容字段解释见课程详情） |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "courses": [
            {
                "course_id": 3,
                "title": "1111",
                "seller_id": 1,
                "seller_name": "123",
                "published": true,
                "tags": [
                    {
                        "tag_id": 1,
                        "tag_name": "前端"
                    },
                    {
                        "tag_id": 2,
                        "tag_name": "后端"
                    }
                ],
                "deleted": false,
                "sales": 0,
                "snapshot_id": 4,
                "content": "0000",
                "cover": "/media/20210903155523MvMZdsY824.jpg",
                "price": "10.10",
                "create_time": "2021-09-13 15:35:29"
            },
            {
                "course_id": 2,
                "title": "1111",
                "seller_id": 1,
                "seller_name": "123",
                "published": true,
                "tags": [
                    {
                        "tag_id": 1,
                        "tag_name": "前端"
                    },
                    {
                        "tag_id": 2,
                        "tag_name": "后端"
                    }
                ],
                "deleted": false,
                "sales": 0,
                "snapshot_id": 3,
                "content": "0000",
                "cover": "/media/20210903155523MvMZdsY824.jpg",
                "price": "10.10",
                "create_time": "2021-09-13 15:34:28"
            }
        ]
    }
}
```

----

### 获取课程的快照列表

**接口功能**

> 获取课程的快照列表

**URL**

> /api/course/get_course_snapshot_list

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段  | 字段类型 | 说明         |
> | --------- | -------- | ------------ |
> | code      | int      | 状态码       |
> | msg       | string   | 状态信息     |
> | snapshots | list     | 快照 id 列表 |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "snapshots": [
            4,
            5
        ]
    }
}
```

----

### 获取全部标签

**接口功能**

> 获取全部标签

**URL**

> /api/course/get_all_tags

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段      | 字段类型 | 说明     |
> | ------------- | -------- | -------- |
> | code          | int      | 状态码   |
> | msg           | string   | 状态信息 |
> | tags          | list     | 标签列表 |
> | tags:tag_id   | int      | 标签 id  |
> | tags:tag_name | string   | 标签名   |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "tags": [
            {
                "tag_id": 3,
                "tag_name": "APP"
            },
            {
                "tag_id": 1,
                "tag_name": "前端"
            },
            {
                "tag_id": 2,
                "tag_name": "后端"
            }
        ]
    }
}
```

----

### 添加课程至购物车

**接口功能**

> 添加课程至购物车（需买家登录）

**URL**

> /api/cart/add_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 获取我的购物车

**接口功能**

> 获取我的购物车（需买家登录）

**URL**

> /api/cart/get_my_cart

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明        |
> | -------- | -------- | ----------- |
> | code     | int      | 状态码      |
> | msg      | string   | 状态信息    |
> | courses  | list     | 课程列表 id |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "courses": [
            3,
            2
        ]
    }
}
```

----

### 删除课程从购物车

**接口功能**

> 删除课程从购物车（需买家登录）

**URL**

> /api/cart/delete_course

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型 | 说明    |
> | :-------- | :--- | :--- | ------- |
> | course_id | true | int  | 课程 id |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 
{
    "course_id": 4
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 下单

**接口功能**

> 下单（需买家登录）

**URL**

> /api/order/place_order

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数       | 必选 | 类型 | 说明         |
> | :--------- | :--- | :--- | ------------ |
> | courses_id | true | int  | 课程 id 列表 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |
> | order_id | int      | 订单号   |

**示例**

```json
// request 
{
    "courses_id": [
        3
    ]
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "order_id": 1
    }
}
```

----

### 获取订单详情（买家）

**接口功能**

> 获取订单详情（买家）（需买家登录）

**URL**

> /order/get_order_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数     | 必选 | 类型 | 说明   |
> | :------- | :--- | :--- | ------ |
> | order_id | true | int  | 订单号 |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明                     |
> | ----------- | -------- | ------------------------ |
> | code        | int      | 状态码                   |
> | msg         | string   | 状态信息                 |
> | order_id    | int      | 订单号                   |
> | price       | string   | 总价格                   |
> | paid        | boolean  | 是否付款                 |
> | create_time | string   | 创建时间                 |
> | snapshots   | list     | 订单中课程的快照 id 列表 |

**示例**

```json
// request 


// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "order_id": "1",
        "price": "1000.0",
        "paid": false,
        "create_time": "2021-09-13 15:46:57",
        "snapshots": [
            1
        ]
    }
}
```

----

### 付款（模拟）

**接口功能**

> 付款（模拟）（无需登录）

**URL**

> /api/order/pay_order

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数     | 必选 | 类型 | 说明   |
> | :------- | :--- | :--- | ------ |
> | order_id | true | int  | 订单号 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | -------- | -------- | -------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**示例**

```json
// request 


// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

----

### 搜索

**接口功能**

> 搜索

**URL**

> /api/course/search

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数    | 必选  | 类型   | 说明     |
> | :------ | :---- | :----- | -------- |
> | content | true  | string | 搜索内容 |
> | tag_id  | false | int    | 标签id   |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明                                 |
> | -------- | -------- | ------------------------------------ |
> | code     | int      | 状态码                               |
> | msg      | string   | 状态信息                             |
> | courses  | list     | 符合条件的课程列表（字段同课程详情） |

**示例**

```json
// request 
{
    "content": "1",
    "tag_id": 1
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "courses": [
            {
                "course_id": 2,
                "title": "1111",
                "seller_id": 1,
                "seller_name": "123",
                "published": true,
                "tags": [
                    {
                        "tag_id": 1,
                        "tag_name": "前端"
                    },
                    {
                        "tag_id": 2,
                        "tag_name": "后端"
                    }
                ],
                "deleted": false,
                "sales": 0,
                "snapshot_id": 3,
                "content": "0000",
                "cover": "/media/20210903155523MvMZdsY824.jpg",
                "price": "10.10",
                "create_time": "2021-09-13 15:34:28"
            },
            {
                "course_id": 3,
                "title": "1111",
                "seller_id": 1,
                "seller_name": "123",
                "published": true,
                "tags": [
                    {
                        "tag_id": 1,
                        "tag_name": "前端"
                    },
                    {
                        "tag_id": 2,
                        "tag_name": "后端"
                    }
                ],
                "deleted": false,
                "sales": 0,
                "snapshot_id": 5,
                "content": "0000",
                "cover": "/media/20210903155523MvMZdsY824.jpg",
                "price": "1000.0",
                "create_time": "2021-09-13 15:39:41"
            },
            {
                "course_id": 5,
                "title": "1111",
                "seller_id": 1,
                "seller_name": "123",
                "published": true,
                "tags": [
                    {
                        "tag_id": 1,
                        "tag_name": "前端"
                    }
                ],
                "deleted": false,
                "sales": 0,
                "snapshot_id": 7,
                "content": "0000",
                "cover": "/media/20210903155523MvMZdsY824.jpg",
                "price": "10.10",
                "create_time": "2021-09-14 11:03:54"
            }
        ]
    }
}
```

----

### 获取我的订单（买家）

**接口功能**

> 获取我的订单（买家）（需要登录）

**URL**

> /api/order/get_my_orders

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段  | 字段类型 | 说明         |
> | --------- | -------- | ------------ |
> | code      | int      | 状态码       |
> | msg       | string   | 状态信息     |
> | orders_id | list     | 订单 id 列表 |

**示例**

```json
// request 

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "orders_id": [
            1
        ]
    }
}
```

----

