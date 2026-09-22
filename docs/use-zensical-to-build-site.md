# 使用zensical搭建静态网站

## 准备

```shell
python -m pip install --upgrade pip
```

## 创建 Python 虚拟环境并初始化Git仓库

```shell
mkdir -p ~/Notes
cd ~/Notes
git init
# 避免将虚拟环境文件和最终生成的网页代码提交到 Git
echo ".venv/" > .gitignore
echo "site/" >> .gitignore
# 在 Python 虚拟环境中运行 Zensical 以避免依赖冲突
# 创建虚拟环境（文件夹名为 .venv）
python3 -m venv .venv
# 激活虚拟环境
source .venv/bin/activate
# 3. 升级 pip（推荐）
pip install --upgrade pip

# 4. 安装 Zensical
pip install zensical

# 5. 验证安装
zensical --version
```

## 配置项目

```shell
zensical new .
tree # 看项目结构
.
├── docs/
│   ├── index.md            # 网站首页
│   └── markdown.md         # Markdown 示例
└── zensical.toml           # 配置文件
```

配置项目：

```toml
[project]
site_url = "https://www.example.com/"
site_name = "我的个人知识库"
# site_description = "Your project description"
# site_author = "Your name"

# copyright = "Copyright &copy; 2026 Your name"

# repo_url = "https://github.com/user/repo"
# repo_name = "user/repo"
# edit_uri = "edit/main/docs/"

nav = [
  { "Get started" = "index.md" },
  { "Markdown in 5min" = "markdown.md" },
]

# extra_css = ["stylesheets/extra.css"]
# extra_javascript = ["javascripts/extra.js"]

[project.theme]
variant = "modern"
# custom_dir = "overrides"
# favicon = "images/favicon.png"
language = "zh"
features = [
  "announce.dismiss",
  # "content.action.edit",
  # "content.action.view",
  "content.code.annotate",
  "content.code.copy",
  "content.code.select",
  "content.footnote.tooltips",
  "content.tabs.link",
  "content.tooltips",
  # "navigation.expand",
  # "header.autohide",
  "navigation.footer",
  "navigation.indexes",
  "navigation.instant",
  "navigation.instant.prefetch",
  # "navigation.instant.progress",
  "navigation.path",
  # "navigation.prune",
  "navigation.sections",
  # "navigation.tabs",
  # "navigation.tabs.sticky",
  "navigation.top",
  "navigation.tracking",
  "search.highlight",
  # "toc.follow",
  # "toc.integrate",
]

# logo = "assets/logo.png"

# [project.theme.icon]
# logo = "lucide/smile"

# [project.theme.font]
# text = "Inter"
# code = "Jetbrains Mono"

[[project.theme.palette]]
media = "(prefers-color-scheme)"
toggle.icon = "lucide/sun-moon"
toggle.name = "Switch to light mode"

[[project.theme.palette]]
media = "(prefers-color-scheme: light)"
scheme = "default"
toggle.icon = "lucide/sun"
toggle.name = "Switch to dark mode"

[[project.theme.palette]]
media = "(prefers-color-scheme: dark)"
scheme = "slate"
toggle.icon = "lucide/moon"
toggle.name = "Switch to system preference"

# [[project.extra.social]]
# icon = "fontawesome/brands/github"
# link = "https://github.com/user/repo"

# [[project.extra.social]]
# icon = "fontawesome/brands/mastodon"
# link = "https://fosstodon.org/@user"

[project.markdown_extensions]
abbr = {}
admonition = {}
attr_list = {}
def_list = {}
footnotes = {}
md_in_html = {}
toc.permalink = true
pymdownx.arithmatex.generic = true
pymdownx.betterem = {}
pymdownx.caret = {}
pymdownx.details = {}
pymdownx.emoji.emoji_generator = "zensical.extensions.emoji.to_svg"
pymdownx.emoji.emoji_index = "zensical.extensions.emoji.twemoji"
pymdownx.highlight.anchor_linenums = true
pymdownx.highlight.line_spans = "__span"
pymdownx.highlight.pygments_lang_class = true
pymdownx.inlinehilite = {}
pymdownx.keys = {}
pymdownx.magiclink = {}
pymdownx.mark = {}
pymdownx.smartsymbols = {}
# pymdownx.snippets.base_path = "includes"
pymdownx.superfences.custom_fences = [
  { name = "mermaid", class = "mermaid", format = "pymdownx.superfences.fence_code_format" },
]
pymdownx.tabbed.alternate_style = true
pymdownx.tabbed.combine_header_slug = true
pymdownx.tasklist.custom_checkbox = true
pymdownx.tilde = {}

```

## 启动本地网站

```bash
$source .venv/bin/activate
$zensical serve
Serving /home/shachi/Notes/site on http://localhost:8000
Build started
No issues found

# 指定端口：
$zensical serve --dev-addr 192.168.31.199:8000
# 此时同一局域网内的设备可以通过 192.168.31.199:8000 访问网站了.
```

## 把 git 仓库放到 github

在 Github 创建 Notes 仓库，

```bash
git remote add origin git@github.com:chunni98/Notes.git
ssh-keygen -t ed25519 -C "shachi1758@outlook.com"
cat ~/.ssh/id_ed25519.pub
# 复制公钥，在 github 添加ssh密钥
```
