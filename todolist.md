### 功能列表

- [x] 真实姓名：在 nameplate 上魔改
- [ ] 注册控制
- [ ] 图床
- [ ] 用标签重写用户组
- [ ] 更新 config default
- [ ] 更新 help

### 维护列表

- [x] 制定题目编号


---

Change log

- 在 config 中添加 "permission" 组，包括：
  - "disable_sign_up" , 设置为 true 时仅管理员可访问注册页面，设置为 false/undefined 时开放注册。
  - "enable_permission_control", 设置为 true 时启用用户组功能，设置为 false/undefined 时禁用。
- 拥有 manage_user 权限的账户可以修改所有用户的 nameplate 。
  - 在 permission.allow_edit_nameplate 开时，所有用户都可以修改自己的 nameplate ；否则，仅管理员可以查看并修改。

2019.11.06

- 加入字符串形式的用户组功能，控制题面查看，数据查看。

---

新 api

problem 加入 isAllowedUseBy ，判断用户是否有权查看题面
problem 加入 isAllowedViewDataBy ，判断用户是否有权查看数据
syzoj.utils 加入 isValidUserGroupList(s) ，传入当前需校验的用户组列表（字符串），
    返回 -1 表示用户组未启用， 0 表示无效， 1 表示有效

---

用户组功能简介：
- 使用前请在 config 文件中设置可用的用户组
- 用户具有 user_group 属性，可以以逗号分隔的形式指定用户组
  - 例如 `123,4,5` 表示该用户在 `123`, `4`, `5` 三个组中
- 题目可以设定 至少在指定用户组中的一个用户 才能查看题目，才能查看数据
  - 用户要能查看数据的前提是能查看题目
  - 例如，题目 A 设置能查看题目的用户组为 `1,2` ，能查看数据的用户组为 `1,3`
  - 则用户组 `1` 既能看题也能看数据， `2` 只能看题， `3` 不能看题也不能看数据