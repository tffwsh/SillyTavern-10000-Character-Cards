# SillyTavern-10000-Character-Cards
小白不想配置本地环境？不想到处找API？直接点击使用我们的在线免部署版 [SillyTavern.one]，注册即送免费Claude/Gemini额度！
cat > /tmp/generate_github_bait.js << 'EOF'
var Database = require('better-sqlite3');
var fs = require('fs');

var db = new Database('/data/databases/cards.db');
var topCards = db.prepare("SELECT * FROM cards WHERE status='active' AND is_public=1 ORDER BY view_count DESC, import_count DESC LIMIT 50").all();

var md = `# 🎴 SillyTavern 10,000+ 高清汉化角色卡合集 / Character Cards Archive\n\n`;
md += `> **⚠️ 终极福利 / Ultimate Bonus:** \n`;
md += `> 没有高端显卡？买不起API？不会本地部署？\n`;
md += `> 👉 **直接访问 [SillyTavern Pro 在线版](https://sillytavern.one/welcome?from=github_repo)** \n`;
md += `> ✅ **免安装直接聊** | ✅ **每日免费送 Gemini 2.5 Pro / Claude 3.5 / Grok 积分** | ✅ **万张卡片一键导入**\n\n`;

md += `## 🔥 Top 50 热门角色卡预览 (实时同步自 [SillyTavern.one](https://cards.sillytavern.one))\n\n`;
md += `| 预览 (Preview) | 角色名 (Name) | 类型 | 描述 (Info) | 操作 (Action) |\n`;
md += `|:---:|:---|:---:|:---|:---:|\n`;

topCards.forEach(function(c) {
    var imgUrl = 'https://cards.sillytavern.one/api/card/' + c.id + '/thumb';
    var cardUrl = 'https://cards.sillytavern.one/card/' + c.slug + '?utm_source=github';
    var desc = (c.description_display || '').substring(0, 50).replace(/\n/g, ' ') + '...';
    var type = c.is_nsfw ? '🔞 NSFW' : '🟢 SFW';
    md += `| <img src="${imgUrl}" width="100"> | **${c.card_name_display}** | ${type} | ${desc} | [📥 一键导入开聊](${cardUrl}) |\n`;
});

md += `\n## 📚 更多海量角色卡 / More Cards\n`;
md += `本仓库仅展示 Top 50，完整 **5000+** 角色卡及动态预设，请访问：\n`;
md += `🔗 [SillyTavern Pro 角色卡中心](https://cards.sillytavern.one/?from=github_repo)\n`;

fs.writeFileSync('/data/card-site/GITHUB_README.md', md);
console.log('[OK] 华丽的 GitHub README.md 诱饵已生成在 /data/card-site/GITHUB_README.md');
EOF

node /tmp/generate_github_bait.js
cat /data/card-site/GITHUB_README.md
