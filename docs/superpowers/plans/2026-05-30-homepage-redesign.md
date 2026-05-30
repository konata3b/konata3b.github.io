# 个人主页官方 1:1 复刻风格重塑 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将个人主页 `C:\Users\wxb\workspace\soft\python\konata3b.github.io\index.html` 替换为像素级 1:1 复刻的国科大教师主页样式，展示个人学术信息，支持中英文平滑淡入淡出切换，并引用目录下的 `logo.png` 和 `photo.jpg`。

**Architecture:** 
1. 部署从官方 MHTML 网页快照中成功解析出的三款核心样式表（`base.css`, `myzone.css`, `homePage.css`）到项目根目录。
2. 覆写主页入口文件 `index.html`，保留原装的 DOM 双栏布局骨架（`myzone3` 主题风格，侧边栏在右侧，内容区在左侧），替换图片及样式相对路径为根目录结构。
3. 植入高保真客户端多语言 JS 引擎，以声明式数据属性实现中英文的一键平滑过渡切换与状态缓存。

**Tech Stack:** 
HTML5, Vanilla CSS (官方原装提取), Vanilla Javascript.

---

### Task 1: 部署官方原装 CSS 样式表到根目录

**Files:**
- Create: `C:\Users\wxb\workspace\soft\python\konata3b.github.io\base.css`
- Create: `C:\Users\wxb\workspace\soft\python\konata3b.github.io\myzone.css`
- Create: `C:\Users\wxb\workspace\soft\python\konata3b.github.io\homePage.css`

- [ ] **Step 1: 复制 `base.css` 到根目录**
  
  运行：
  ```powershell
  Copy-Item -Force "C:\Users\wxb\workspace\soft\python\konata3b.github.io\.superpowers\brainstorm\session\content\base.css" "C:\Users\wxb\workspace\soft\python\konata3b.github.io\base.css"
  ```
  校验根目录下文件大小应约为 85,638 字节。

- [ ] **Step 2: 复制 `myzone.css` 到根目录**
  
  运行：
  ```powershell
  Copy-Item -Force "C:\Users\wxb\workspace\soft\python\konata3b.github.io\.superpowers\brainstorm\session\content\myzone.css" "C:\Users\wxb\workspace\soft\python\konata3b.github.io\myzone.css"
  ```
  校验根目录下文件大小应约为 5,879 字节。

- [ ] **Step 3: 复制 `homePage.css` 到根目录**
  
  运行：
  ```powershell
  Copy-Item -Force "C:\Users\wxb\workspace\soft\python\konata3b.github.io\.superpowers\brainstorm\session\content\homePage.css" "C:\Users\wxb\workspace\soft\python\konata3b.github.io\homePage.css"
  ```
  校验根目录下文件大小应约为 4,646 字节。

- [ ] **Step 4: 提交样式表文件到 Git**
  
  运行：
  ```powershell
  git add base.css myzone.css homePage.css
  git commit -m "style: deploy official UCAS style sheets to root"
  ```
  预期：Git 提示 3 个文件成功添加并提交。

---

### Task 2: 覆写 `index.html` 为 1:1 官方复刻学术主页

**Files:**
- Modify: `C:\Users\wxb\workspace\soft\python\konata3b.github.io\index.html`

- [ ] **Step 1: 覆写 `index.html` 源码**
  
  使用以下最新验证完毕的 1:1 结构覆盖 `index.html` 文件，包括将「关于我」移去、将「研究兴趣」移至最顶端、添加留白「近期工作」，并将「竞赛与活动」以代码注释形式保留在底部：
  
  写入 `C:\Users\wxb\workspace\soft\python\konata3b.github.io\index.html`：
  ```html
  <!DOCTYPE html>
  <html lang="zh-CN">
  <head>
      <meta charset="UTF-8">
      <title>Konata-中国科学院大学-UCAS</title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0">

      <!-- 加载国科大官方系统提取出的原装 CSS 样式表，实现 1:1 完美复刻 -->
      <link href="base.css" rel="stylesheet" type="text/css" />
      <link href="myzone.css" rel="stylesheet" type="text/css" />
      <link href="homePage.css" rel="stylesheet" type="text/css" />

      <style>
          /* 补充小部分自定义学术标签和双语淡入淡出动效 */
          .tag {
              display: inline-block;
              background-color: #eaf1f8;
              color: #075292;
              font-size: 13px;
              font-weight: 500;
              padding: 4px 12px;
              border: 1px solid #c8d6e3;
              border-radius: 20px;
              margin-right: 8px;
              margin-bottom: 8px;
              white-space: nowrap;
              transition: all 0.2s;
          }
          
          .tag:hover {
              background-color: #075292;
              color: #ffffff;
          }

          .publication-list {
              list-style-type: none;
              padding-left: 0;
              margin: 0;
          }

          .publication-item {
              margin-bottom: 12px;
              text-align: left;
          }

          .pub-number {
              font-weight: normal;
              margin-right: 8px;
          }

          .pub-content {
              display: inline;
          }

          /* 优化原版 logo 尺寸适应 */
          #logo img {
              width: auto;
              height: 100%;
              max-width: 486px;
              object-fit: contain;
              object-position: left center;
          }

          /* 语言切换按钮样式 */
          .b-topbar a {
              cursor: pointer;
              padding: 2px 6px;
              border-radius: 3px;
              transition: all 0.2s;
          }

          .b-topbar a.active {
              background-color: #075292;
              color: #ffffff !important;
              text-decoration: none;
          }

          [data-zh] {
              transition: opacity 0.15s ease;
          }

          /* 提升正文部分文字字号，使其在宽屏设备上更清晰好读 */
          body {
              font-size: 16px !important;
          }
          #myzone3 .m-itme .mi-box .mib-c {
              font-size: 15px !important;
              line-height: 1.8 !important;
          }
          #myzone3 .b-menu ul li {
              font-size: 15px !important;
          }
      </style>
  </head>
  <body id="myzone3">
      <!-- 顶部导航栏 -->
      <div id="header">
          <div class="container">
              <a id="logo" class="brand" href="#"> 
                  <img src="logo.png" alt="UCAS Logo" onerror="this.style.display='none'">
              </a>
              <div class="b-topbar">
                  <a id="btn-zh" class="active" onclick="setLanguage('zh')">[中文]</a>
                  <a id="btn-en" onclick="setLanguage('en')">[English]</a>
              </div>
          </div>
      </div>

      <!-- 主体内容 -->
      <div id="main-content">
          <div class="container">
              <!-- 右侧边栏菜单（myzone3 结构中，菜单在右侧 floated right） -->
              <div class="b-menu">
                  <ul style="list-style-type:disc">
                      <li><a href="#interests" data-zh="研究兴趣" data-en="Research Interests">研究兴趣</a></li>
                      <li><a href="#education" data-zh="教育背景" data-en="Education">教育背景</a></li>
                      <li><a href="#work" data-zh="近期工作" data-en="Recent Work">近期工作</a></li>
                      <!-- <li><a href="#activities" data-zh="竞赛与活动" data-en="Contests & Activities">竞赛与活动</a></li> -->
                  </ul>
              </div>
              <!--//b-menu:end-->

              <!-- 左侧个人名片卡（利用 float 流式排版，与 b-menu 同级） -->
              <div class="b-pinfo">
                  <div class="bp-title" id="basic-info" data-zh="基本信息" data-en="Basic Information">基本信息</div>
                  <img class="bp-photo" src="photo.jpg" alt="Photo" onerror="this.src='data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 100 100\' fill=\'%23a0b3c6\'><circle cx=\'50\' cy=\'40\' r=\'20\'/><path d=\'M20,90 C20,70 80,70 80,90\'/></svg>'">
                  <div class="bp-enty"> 
                      <p></p><p></p><p></p>
                      <p><b>Konata<br></b></p>
                      <p><b data-zh="即将入学 · 人工智能 硕士研究生 (2026 秋)" data-en="Incoming M.S. Student in Artificial Intelligence (Fall 2026)">即将入学 · 人工智能 硕士研究生 (2026 秋)<br></b></p>
                      <p><b data-zh="中国科学院大学" data-en="University of Chinese Academy of Sciences">中国科学院大学</b></p>
                      <p><br></p>
                      <p><span data-zh="电子邮件：" data-en="Email: ">电子邮件：</span> <a href="mailto:1571454955@qq.com">1571454955@qq.com</a><br></p>
                      <p><span>GitHub：</span> <a href="https://github.com" target="_blank">github.com</a><br></p>
                      <p><span data-zh="通信地址：" data-en="Address: ">通信地址：</span> <span data-zh="中国" data-en="China">中国</span><br></p>
                      <p></p><p></p><p></p>
                  </div>
              </div>

              <!-- 研究领域 / 兴趣 -->
              <div class="m-itme" id="interests">
                  <h3 class="mi-t">
                      <span data-zh="研究兴趣" data-en="Research Interests">研究兴趣</span>
                  </h3>
                  <div class="mi-box">
                      <div class="mib-c">
                          <span class="tag" data-zh="大语言模型" data-en="Large Language Models">大语言模型</span>
                          <span class="tag" data-zh="多模态模型" data-en="Multi-modal Models">多模态模型</span>
                          <span class="tag" data-zh="智能体" data-en="Intelligent Agents">智能体</span>
                      </div>
                  </div>
              </div>

              <!-- 教育背景 -->
              <div class="m-itme" id="education">
                  <h3 class="mi-t">
                      <span data-zh="教育背景" data-en="Education">教育背景</span>
                  </h3>
                  <div class="mi-box">
                      <div class="mib-c" data-zh="中国科学院大学 (2026–2029)" data-en="University of Chinese Academy of Sciences (2026–2029)">
                          中国科学院大学 (2026–2029)
                      </div>
                  </div>
              </div>

              <!-- 近期工作 -->
              <div class="m-itme" id="work">
                  <h3 class="mi-t">
                      <span data-zh="近期工作" data-en="Recent Work">近期工作</span>
                  </h3>
                  <div class="mi-box">
                      <div class="mib-c">
                          <ul class="publication-list">
                              <li class="publication-item">
                                  <font size="4">
                                      <span class="pub-number">1.</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
                                      <span class="pub-content" data-zh="" data-en=""></span>
                                  </font>
                              </li>
                          </ul>
                      </div>
                  </div>
              </div>

              <!-- 竞赛与活动（代码已注释保留，供以后使用） -->
              <!--
              <div class="m-itme" id="activities">
                  <h3 class="mi-t">
                      <span data-zh="竞赛与活动" data-en="Contests & Activities">竞赛与活动</span>
                  </h3>
                  <div class="mi-box">
                      <div class="mib-c">
                          <ul class="publication-list">
                              <li class="publication-item">
                                  <font size="4">
                                      <span class="pub-number">1.</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
                                      <span class="pub-content" data-zh="" data-en=""></span>
                                  </font>
                              </li>
                              <li class="publication-item">
                                  <font size="4">
                                      <span class="pub-number">2.</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
                                      <span class="pub-content" data-zh="" data-en=""></span>
                                  </font>
                              </li>
                          </ul>
                      </div>
                  </div>
              </div>
              -->

          </div>
      </div>

      <!-- 页脚 Footer -->
      <div id="footer">
          <div class="container">
              <span data-zh="声明：网页信息由学生个人维护，仅用于展示。教师系统风格由网络信息中心提供。" 
                    data-en="Disclaimer: This webpage is maintained by the student. Academic portal style templates are provided by the Network Information Center.">
                  声明：网页信息由学生个人维护，仅用于展示。教师系统风格由网络信息中心提供。
              </span><br>
              2013 &copy; <span data-zh="中国科学院大学，网络信息中心." data-en="University of Chinese Academy of Sciences, Network Information Center.">中国科学院大学，网络信息中心.</span>
              <br>
              <span style="color: #999; margin-top: 5px; display: inline-block;"
                    data-zh="声明：本页面用于学术身份验证，信息真实。最后更新：2026 年 5 月。"
                    data-en="Academic verification page. All information is accurate. Last updated: May 2026.">
                  声明：本页面用于学术身份验证，信息真实。最后更新：2026 年 5 月。
              </span>
          </div>
      </div>

      <script>
          // 语言切换 JavaScript
          function setLanguage(lang) {
              document.querySelectorAll('[data-zh]').forEach(el => {
                  const zhText = el.getAttribute('data-zh');
                  const enText = el.getAttribute('data-en');
                  
                  el.style.opacity = 0;
                  setTimeout(() => {
                      el.innerText = lang === 'zh' ? zhText : enText;
                      el.style.opacity = 1;
                  }, 150);
              });

              // 切换按钮样式
              if (lang === 'zh') {
                  document.getElementById('btn-zh').classList.add('active');
                  document.getElementById('btn-en').classList.remove('active');
                  document.documentElement.lang = 'zh-CN';
              } else {
                  document.getElementById('btn-en').classList.add('active');
                  document.getElementById('btn-zh').classList.remove('active');
                  document.documentElement.lang = 'en';
              }

              // 保存语言偏好
              localStorage.setItem('lang-preference', lang);
          }

          // 初始化加载
          window.addEventListener('DOMContentLoaded', () => {
              const savedLang = localStorage.getItem('lang-preference') || 'zh';
              setLanguage(savedLang);
          });
      </script>
  </body>
  </html>
  ```

- [ ] **Step 2: 提交代码更改到 Git**
  
  运行：
  ```powershell
  git add index.html
  git commit -m "feat: complete academic homepage 1:1 replica implementation"
  ```
  预期：git 提示 1 个文件发生更改，成功提交。

---

### Task 3: 最终部署验证

- [ ] **Step 1: 关闭原型测试服务器**
  
  运行：
  ```powershell
  Stop-Process -Id (Get-Content "C:\Users\wxb\workspace\soft\python\konata3b.github.io\.superpowers\brainstorm\session\state\server.pid") -Force
  ```
  或者通过 `manage_task` 工具手动终止对应的 Node.js 后台进程。

- [ ] **Step 2: 启动本地测试服务器预览最终的 `index.html`**
  
  在项目根目录下利用 python 或 http-server 快速校验：
  运行：
  ```powershell
  python -m http-server 8000
  ```
  在浏览器中打开 `http://localhost:8000`，测试中英文点击切换效果、证件照名片对齐、就读专业已被完全删除，Logo 和文字显示精美，大字号阅读自然。
