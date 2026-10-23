# 赛博鸡蛋 · 对外总入口页

替代飞书首页的对外入口。飞书仍是内容仓（12 篇文档一个字没动），这里是"路标"：
别人点这一个链接进来，再分流到飞书各篇。飞书哪篇被限，改这里一行链接重新部署即可，对外地址不变。

## 目录

```
site/
├── index.html          单页站点：九大板块 + 页内锚点导航 + 底部二维码
├── copy-draft.md       定稿文案，改内容先改这里再同步到 HTML
└── assets/
    ├── qr.jpg          微信二维码（已裁掉名片信息）
    └── og.jpg          分享卡片图 1200x630
```

页面结构：顶部品牌行 → 首屏大标题 → 九条锚点导航 → 01 蛋报（深色卡）+ 02~09（白卡）→ 质保与联系方式。所有按钮跳飞书单篇，不跳发卡页。

## 本地预览

```bash
cd site && python -m http.server 5500
# 打开 http://127.0.0.1:5500
```

## 上线（Cloudflare Pages，免费）

1. 域名注册并实名通过后，把域名的 NS 改成 Cloudflare 给的两个地址（在域名注册商后台改）。
2. Cloudflare 后台 → Workers & Pages → Create → Pages → Upload assets → 上传 `site/` 里全部文件。
3. 项目 → Custom domains → 添加你的域名（主域名 + www 各一次），HTTPS 自动签发。
4. 回 `index.html` 把 `og:image` 改成绝对地址：`https://你的域名/assets/og.jpg`。
5. 用手机 4G（不是 WiFi）打开一次，确认能通；再分别用微信内置浏览器、B 站 App 各点一次。

## 换链（飞书某篇被限时）

打开 `index.html`，搜那篇的 token（每个链接长这样：`https://my.feishu.cn/docx/<token>`），换成新文档 token，重新上传部署。约 1 分钟。

当前链接清单：

| 位置 | 标题 | Token |
| :--- | :--- | :--- |
| 主入口 | 今日蛋报 | `B4yCdmbASopMRrxSAr5cYsdNnGc` |
| 01 | ChatGPT Plus 进阶 | `Wt2adAHsQoZvNnxIo9NcSmvpnCd` |
| 02 | WorkBuddy 接入 | `Iwb9dafb2on4nIxSjrLc0HzRnjg` |
| 03 | 哈基米 Pro 进阶 | `T81Xdw1KoolDAoxCYT0c3I5hnZe` |
| 04 | 登录验证 | `VNoXdPNC0odrH7xk3PJc75yPnqf` |
| 05 | Notion 会员 | `JXGFdFeBkocsi1xI8OLcKB3knV3` |
| 06 | 克劳德 Pro 进阶 | `Uh8cdajFbobJCoxKLWTcu6X1nhh` |
| 07 | Meta Muse | `K0ztdFEdMoSGwlx9kDGchBImnae` |
| 08 | 大众点评副业 | `X6Sdd8Cqdo9C0NxiZo7cdybDnCc` |

## 刻意的取舍

- 页面只做路标：不写价格、成品号、接码、下单这些词，敏感描述全留在飞书单篇里。页面越干净，越不容易被举报。
- 不做站内搜索、不做统计脚本、不引外部字体和 CDN：一页纸，加载最快，也少一个被拦的点。
- 底部常驻一句"打不开就加我"：飞书真挂了，人还有地方去。
