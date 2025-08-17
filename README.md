# 📕 SDU 自动绩点可视化 | SDU Auto GPA Visualizer

> 面向山东大学可信电子凭证 PDF 成绩单的本地解析与可视化（China Red 配色）。  
> Local, client‑side parsing & visualization for SDU verified PDF transcripts.

---

## 🎯 项目目标 (Project Aim)
- **中文**：构建一个在浏览器端运行的单页应用（Single‑Page Application / ˈsɪŋɡl peɪdʒ ˌæplɪˈkeɪʃn/），实现上传 PDF 成绩单后 **自动抽取** *学期 (semester / sɪˈmestə(r)/)、课程 (course / kɔːs/)、属性 (attribute / ˈætrɪˌbjuːt/)、学分 (credit / ˈkrɛdɪt/)、成绩 (grade / ɡreɪd/)* 等信息，并据此 **计算绩点 (GPA / dʒiː piː eɪ/)** 与 **可视化展示 (visualization / ˌvɪʒuələˈzeɪʃn/)**。\n- **English**: Build a client‑side SPA to **extract** key fields—*semester, course, attribute, credit, grade*—from SDU PDF transcripts and compute **GPA**, followed by **visual analytics**.

> **Methodological note**（方法学说明）: GPA is computed as a **credit‑weighted mean**. Let \( g_i \) be per‑course grade (converted to either score or 4.0 scale), \( w_i \) the credit. Then  
> \\[ \\text{GPA} = \\frac{\\sum_i w_i g_i}{\\sum_i w_i}. \\]  
> 不同院校/学院可能采用不同换算与规章，此处未能确认的部分以 *This information is not definitively established* 明示。

---

## 📦 文件结构 (Files)
- `auto-gpa-visualizer.html`：主页面（单文件，含样式与脚本）。
- （可选）将其与本 README 放在任意目录，使用浏览器直接打开 HTML 即可。

---

## 🛠️ 使用步骤 (How to Use)
1. **获取 PDF 成绩单**（山东大学信息化公共管理服务平台 → 可信电子凭证 → 成绩单 → 预览 → 填写邮箱 → 接收带公章 PDF）。*This information is not definitively established*（流程可能调整）。
2. 使用现代浏览器（Chrome/Edge/Firefox/Safari 最新版）。
3. 打开 `index.html`：将 PDF **拖拽**到上传区域或点击“选择文件”。
4. 解析完成后：
   - 顶部 KPI 显示 **课程数/学分**、**加权分或 4.0 GPA**、**属性学分结构**、**时间范围**。
   - 图表包含 **学期曲线**、**属性学分环图**、**成绩直方图**、**贡献度 Top10**（score×credit）。

---

## ⚙️ 计算设置 (Computation Settings)
- **GPA 方案 (Scale)**：
  - *加权平均分 (0–100)*：直接以百分制分数参与加权（常见于校内平均分统计）。
  - *线性 4.0*：\( \\text{GPA}=4\\times\\text{score}/100 \)。
  - *区间 4.0（常用档位）*：90–100→4.0；85–89→3.7；82–84→3.3；78–81→3.0；75–77→2.7；72–74→2.3；68–71→2.0；64–67→1.5；60–63→1.0；<60→0。*This information is not definitively established*（各单位可能不同）。\n  - *自定义*：在源码中扩展 `toGPA` 即可。
- **质化成绩映射 (Qualitative→Numeric)**：
  - 预设：优秀(Excellent / ɪkˈselənt/)→95/97/90；良好(Good / ɡʊd/)→85/88/80；合格(Pass / pɑːs/)→60；不合格(Fail / feɪl/)→0；缓考(Deferred / dɪˈfɜːd/)→0。*This information is not definitively established*。
- **零学分 (Zero‑credit) 计入**：默认 **不计入**（如 CET 成绩 0 学分、仅做合格性记录），可手动启用。*This information is not definitively established*。
- **重修 (Retake / ˈriːteɪk/)**：默认 **仅计最高分**（检测“*”标注），亦可关闭以逐条计入。*This information is not definitively established*。

---

## 📊 可视化 (Visualization)
- **Semester curve**（学期 GPA/加权分曲线）：按学分加权聚合每学期指标。\n- **Attribute donut**（属性学分环图）：必修/限选/任选学分占比。\n- **Score histogram**（成绩直方图）：默认区间 [50,60), …, [95,100]。\n- **Top10 contribution**：按 `score × credit` 排序的课程条形图。

---

## 🔒 隐私与安全 (Privacy & Security)
- **中文**：所有计算在浏览器本地完成，PDF 不会上传服务器。\n- **English**: Everything runs locally in your browser; your PDF is **not uploaded** anywhere.

---

## 🧠 精确性与局限 (Accuracy & Limitations)\n- 解析依赖 PDF 文本流顺序（PDF.js 提取）。若学校模板更改或 PDF 仅含位图，需更新解析规则。\n- SDU 成绩单上出现“平均学分绩点 85.54”等字段，更像**加权平均分**而非 4.0 GPA；官方折算口径未在本文档确认，*This information is not definitively established*。请以官方教务政策为准。\n- 建议手工抽样复核若干课程，以验证解析正确性。

---

## 🧩 技术栈 (Tech Stack)\n- **PDF.js** for parsing; **ECharts** for charts; plain **HTML/CSS/JS** in one file.\n- 可在 `toGPA` 和 `parseQualitative` 中进一步自定义分段与映射。

---

## 📬 反馈与扩展 (Feedback & Extension)\n- 支持导出 CSV/PNG、细化课程分类、引入置信区间可视化（Confidence Interval / ˈkɒnfɪdəns ˈɪntəvəl/）。\n- 可接入本地存储保存设置、增加“课程搜索/筛选”。
