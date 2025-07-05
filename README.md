# 蓝小豆笔记网 - 开发文档

## 📋 项目概述

**项目名称**: 蓝小豆笔记网
**主题名称**: 开心果
**作者**: 蓝小豆
**版权**: © 2025 蓝小豆
**口号**: 学习知识，连接世界！
**版本**: v1.0.0

## 🏗️ 项目架构

### 目录结构
```
蓝小豆笔记网/
├── admin/
│   ├── app/   # 应用核心代码│   
├── Controllers/        # 控制器
│   ├── Models/            # 数据模型
│   ├── Views/             # 视图模板
│   └── Core/              # 核心类库
├── config/                # 配置文件
│   ├── app.php           # 应用配置
│   ├── database.php      # 数据库配置
│   └── routes.php        # 路由配置
├── database/              # 数据库相关
│   └── migrations/       # 数据库迁移文件
├── public/                # 公共资源
│   ├── css/              # 样式文件
│   ├── js/               # JavaScript文件
│   ├── images/           # 图片资源
│   └── uploads/          # 上传文件
├── storage/               # 存储目录
│   ├── logs/             # 日志文件
│   └── cache/            # 缓存文件
├── install/               # 安装向导
│   ├── smart-installer.php  # 智能安装向导
│   ├── EnvironmentDetector.php  # 环境检测器
│   └── ...               # 其他安装文件
├── vendor/                # Composer依赖
├── index.php             # 入口文件
├── .htaccess             # Apache重写规则
└── README.md             # 项目说明
```

### MVC架构设计

#### 控制器 (Controllers)
- **HomeController.php**: 首页控制器
- **ArticleController.php**: 文章管理控制器
- **UserController.php**: 用户管理控制器
- **CommentController.php**: 评论管理控制器
- **PageController.php**: 页面控制器
- **ErrorController.php**: 错误处理控制器

#### 模型 (Models)
- **User.php**: 用户模型
- **Article.php**: 文章模型
- **Category.php**: 分类模型
- **Tag.php**: 标签模型
- **Comment.php**: 评论模型

#### 视图 (Views)
- **layouts/**: 布局模板
- **home/**: 首页模板
- **articles/**: 文章模板
- **users/**: 用户模板
- **errors/**: 错误页面模板

#### 核心类库 (Core)
- **Application.php**: 应用程序主类
- **Router.php**: 路由处理器
- **Controller.php**: 控制器基类
- **Model.php**: 模型基类
- **Database.php**: 数据库连接类
- **Autoloader.php**: 自动加载器

## 🎨 开心果主题设计

### 设计理念
- **清新活力**: 橙色主调 + 薄荷绿辅助
- **现代简约**: 圆角设计 + 渐变效果
- **用户友好**: 直观导航 + 响应式布局

### 色彩方案
```css
:root {
    --primary-color: #FF6B35;      /* 主色调 - 活力橙 */
    --secondary-color: #4ECDC4;    /* 辅助色 - 薄荷绿 */
    --accent-color: #FFE66D;       /* 强调色 - 明黄 */
    --text-color: #333333;         /* 文字色 - 深灰 */
    --bg-color: #FFFFFF;           /* 背景色 - 纯白 */
    --light-gray: #F8F9FA;         /* 浅灰色 */
    --border-color: #E9ECEF;       /* 边框色 */
}
```

### 响应式断点
- **桌面端**: ≥1200px
- **平板端**: 768px - 1199px
- **手机端**: <768px

## 🗄️ 数据库设计

### 核心数据表

#### 用户表 (lxd_users)
- id: 用户ID (主键)
- username: 用户名 (唯一)
- email: 邮箱 (唯一)
- password: 密码 (加密)
- nickname: 昵称
- avatar: 头像
- bio: 个人简介
- role: 角色 (admin/editor/user)
- status: 状态 (active/inactive/banned)
- email_verified_at: 邮箱验证时间
- last_login_at: 最后登录时间
- last_login_ip: 最后登录IP
- created_at: 创建时间
- updated_at: 更新时间

#### 文章表 (lxd_articles)
- id: 文章ID (主键)
- title: 标题
- slug: URL别名
- content: 内容
- excerpt: 摘要
- featured_image: 特色图片
- author_id: 作者ID (外键)
- category_id: 分类ID (外键)
- status: 状态 (draft/published/private)
- is_featured: 是否推荐
- view_count: 浏览次数
- like_count: 点赞次数
- comment_count: 评论次数
- meta_title: SEO标题
- meta_description: SEO描述
- meta_keywords: SEO关键词
- published_at: 发布时间
- created_at: 创建时间
- updated_at: 更新时间

#### 分类表 (lxd_categories)
- id: 分类ID (主键)
- name: 分类名称
- slug: 分类别名
- description: 分类描述
- parent_id: 父分类ID
- sort_order: 排序
- meta_title: SEO标题
- meta_description: SEO描述
- meta_keywords: SEO关键词
- created_at: 创建时间
- updated_at: 更新时间

#### 标签表 (lxd_tags)
- id: 标签ID (主键)
- name: 标签名称
- slug: 标签别名
- description: 标签描述
- color: 标签颜色
- created_at: 创建时间
- updated_at: 更新时间

#### 评论表 (lxd_comments)
- id: 评论ID (主键)
- article_id: 文章ID (外键)
- user_id: 用户ID (外键)
- parent_id: 父评论ID
- content: 评论内容
- status: 状态 (pending/approved/rejected)
- ip_address: IP地址
- user_agent: 用户代理
- created_at: 创建时间
- updated_at: 更新时间

#### 文章标签关联表 (lxd_article_tags)
- article_id: 文章ID (外键)
- tag_id: 标签ID (外键)
- created_at: 创建时间

## 🔧 开发规范

### PHP编码规范
- 遵循 **PSR-4** 自动加载标准
- 遵循 **PSR-12** 编码风格标准
- 使用 **驼峰命名法** (camelCase)
- 类名使用 **帕斯卡命名法** (PascalCase)
- 常量使用 **全大写下划线** (UPPER_SNAKE_CASE)

### 文件命名规范
- 控制器: `XxxController.php`
- 模型: `Xxx.php`
- 视图: `xxx.php`
- 配置: `xxx.php`

### 数据库规范
- 表名: `lxd_` 前缀 + 复数形式
- 字段名: 下划线命名法 (snake_case)
- 主键: `id`
- 外键: `xxx_id`
- 时间戳: `created_at`, `updated_at`

### 安全规范
- **SQL注入防护**: 使用预处理语句
- **XSS防护**: 输出转义
- **CSRF防护**: 令牌验证
- **文件上传安全**: 类型检查、大小限制
- **密码安全**: bcrypt加密

## 🚀 部署指南

### 环境要求
- **PHP**: 8.0+
- **MySQL**: 5.7+ / MariaDB 10.3+
- **Web服务器**: Apache 2.4+ / Nginx 1.18+ / IIS 10+
- **PHP扩展**: PDO、PDO_MySQL、mbstring、JSON、Session、OpenSSL、GD、cURL

### 智能安装系统
1. **环境检测**: 自动识别部署环境
2. **系统检查**: 验证PHP版本和扩展
3. **数据库配置**: 智能配置数据库连接
4. **管理员设置**: 创建管理员账户
5. **完成安装**: 系统初始化

### 支持的部署环境
- **本地开发**: XAMPP、WAMP、MAMP、LAMP
- **服务器面板**: 宝塔面板、cPanel、Plesk
- **云服务器**: 阿里云、腾讯云、AWS、Azure
- **虚拟主机**: 各种共享主机环境

## 📝 开发日志

### v1.0.0 (2025-01-26)
- ✅ 完成MVC架构设计
- ✅ 实现智能安装系统
- ✅ 完成开心果主题设计
- ✅ 实现用户管理系统
- ✅ 实现文章管理系统
- ✅ 实现评论系统
- ✅ 完成数据库设计
- ✅ 实现安全防护机制
- ✅ 完成响应式设计
- ✅ 实现SEO优化

## 🔮 后续规划

### v1.1.0 计划
- [ ] 多主题系统
- [ ] 插件系统
- [ ] 多语言支持
- [ ] 高级搜索功能
- [ ] 社交媒体集成

### v1.2.0 计划
- [ ] API接口开发
- [ ] 移动端APP
- [ ] 实时通知系统
- [ ] 高级统计分析
- [ ] 内容推荐算法

## 📞 技术支持

- **作者**: 蓝小豆
- **邮箱**: support@lanxiaodou.com
- **官网**: https://www.lanxiaodou.com
- **文档**: https://docs.lanxiaodou.com

## 🛠️ 开发工具和依赖

### 必需工具
- **PHP 8.0+**: 核心运行环境
- **Composer**: 依赖管理工具
- **MySQL/MariaDB**: 数据库系统
- **Web服务器**: Apache/Nginx/IIS

### 推荐工具
- **VS Code**: 代码编辑器
- **Git**: 版本控制
- **Postman**: API测试
- **phpMyAdmin**: 数据库管理

### 前端依赖
- **Bootstrap 5**: 响应式框架
- **Font Awesome 6**: 图标字体
- **jQuery**: JavaScript库

## 🔍 故障排除

### 常见问题
1. **安装失败**: 检查PHP版本和扩展
2. **数据库连接失败**: 检查数据库配置
3. **权限错误**: 检查目录写入权限
4. **页面404**: 检查URL重写配置
5. **编码问题**: 检查UTF-8设置

### 调试模式
在 `config/app.php` 中设置：
```php
define('DEBUG', true);
```

---

**© 2025 蓝小豆 | 开心果主题系统 | 学习知识，连接世界！**
