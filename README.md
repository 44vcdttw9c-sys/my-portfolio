
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>认识我</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Noto+Sans+SC:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #08080c;
            --text-primary: #f5f5f5;
            --text-secondary: #a0a0a0;
            --text-tertiary: #5a5a5a;
            --accent-purple: #6366f1;
            --accent-pink: #ec4899;
            --accent-teal: #14b8a6;
            --transition: 0.5s cubic-bezier(0.16, 1, 0.3, 1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        html { scroll-behavior: smooth; }

        body {
            font-family: 'Inter', 'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg);
            color: var(--text-primary);
            line-height: 1.6;
            -webkit-font-smoothing: antialiased;
            overflow-x: hidden;
        }

        /* ===== Ambient Background ===== */
        .bg-ambient {
            position: fixed; inset: 0; pointer-events: none; z-index: 0;
        }
        .bg-orb {
            position: absolute; border-radius: 50%; filter: blur(120px); opacity: 0.10;
            animation: orbFloat 20s ease-in-out infinite;
        }
        .bg-orb:nth-child(1) { width: 600px; height: 600px; background: var(--accent-purple); top: -10%; left: -5%; animation-delay: 0s; }
        .bg-orb:nth-child(2) { width: 500px; height: 500px; background: var(--accent-pink); top: 50%; right: -10%; animation-delay: -7s; }
        .bg-orb:nth-child(3) { width: 400px; height: 400px; background: var(--accent-teal); bottom: -10%; left: 30%; animation-delay: -14s; }

        @keyframes orbFloat {
            0%, 100% { transform: translate(0, 0) scale(1); }
            25% { transform: translate(40px, -30px) scale(1.1); }
            50% { transform: translate(-20px, 20px) scale(0.95); }
            75% { transform: translate(-30px, -20px) scale(1.05); }
        }

        /* Grid overlay */
        .grid-overlay {
            position: fixed; inset: 0; pointer-events: none; z-index: 0;
            background-image:
                linear-gradient(rgba(255,255,255,0.012) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255,255,255,0.012) 1px, transparent 1px);
            background-size: 64px 64px;
            mask-image: radial-gradient(ellipse 80% 60% at 50% 40%, black 25%, transparent 70%);
        }

        /* ===== Container ===== */
        .container {
            position: relative; z-index: 1; max-width: 1100px; margin: 0 auto; padding: 0 32px;
        }

        /* ===== Hero ===== */
        .hero {
            min-height: 100vh;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            text-align: center; padding: 120px 0 80px; position: relative;
        }
        .hero-eyebrow {
            font-size: 13px; font-weight: 600; letter-spacing: 0.35em; text-transform: uppercase;
            color: var(--text-tertiary); margin-bottom: 48px;
            opacity: 0; animation: fadeUp 0.8s ease-out 0.2s forwards;
        }
        .hero-quote {
            font-size: clamp(2.2rem, 5.5vw, 4rem);
            font-weight: 650; line-height: 1.22; letter-spacing: -0.025em;
            max-width: 860px; margin-bottom: 36px;
            opacity: 0; animation: fadeUp 0.8s ease-out 0.4s forwards;
        }
        .hero-quote .hl-purple {
            background: linear-gradient(135deg, #818cf8, #a78bfa);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
        }
        .hero-quote .hl-pink {
            background: linear-gradient(135deg, #f472b6, #fb923c);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
        }
        .hero-sub {
            font-size: 1.05rem; color: var(--text-secondary); font-weight: 400;
            max-width: 580px; margin-bottom: 56px;
            opacity: 0; animation: fadeUp 0.8s ease-out 0.6s forwards;
        }

        /* ===== Hero Nav Buttons ===== */
        .hero-nav {
            display: flex; gap: 16px; flex-wrap: wrap; justify-content: center;
            opacity: 0; animation: fadeUp 0.8s ease-out 0.8s forwards;
        }
        .hero-nav-btn {
            padding: 16px 36px; border-radius: 100px;
            font-size: 1rem; font-weight: 550; letter-spacing: 0.02em;
            text-decoration: none; cursor: pointer;
            border: 1px solid rgba(255,255,255,0.08);
            background: rgba(255,255,255,0.03);
            color: var(--text-primary);
            backdrop-filter: blur(12px);
            transition: all var(--transition);
            position: relative; overflow: hidden;
        }
        .hero-nav-btn::before {
            content: ''; position: absolute; inset: 0;
            border-radius: 100px; opacity: 0; transition: opacity 0.5s;
        }
        .hero-nav-btn.nav-purple::before { background: radial-gradient(circle at center, rgba(99,102,241,0.2), transparent); }
        .hero-nav-btn.nav-pink::before   { background: radial-gradient(circle at center, rgba(236,72,153,0.2), transparent); }
        .hero-nav-btn.nav-teal::before   { background: radial-gradient(circle at center, rgba(20,184,166,0.2), transparent); }
        .hero-nav-btn:hover::before { opacity: 1; }
        .hero-nav-btn:hover {
            border-color: rgba(255,255,255,0.18);
            transform: translateY(-3px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.4);
        }
        .hero-nav-btn .btn-arrow {
            display: inline-block; margin-left: 6px; transition: transform 0.3s;
        }
        .hero-nav-btn:hover .btn-arrow { transform: translateX(3px); }

        /* Scroll indicator */
        .scroll-indicator {
            position: absolute; bottom: 40px; left: 50%; transform: translateX(-50%);
            opacity: 0; animation: fadeUp 0.8s ease-out 1.2s forwards;
        }
        .scroll-mouse {
            width: 26px; height: 42px; border: 2px solid var(--text-tertiary);
            border-radius: 13px; position: relative;
        }
        .scroll-mouse::after {
            content: ''; position: absolute; top: 8px; left: 50%; transform: translateX(-50%);
            width: 3px; height: 8px; background: var(--text-tertiary);
            border-radius: 2px; animation: scrollWheel 1.5s ease-in-out infinite;
        }
        @keyframes scrollWheel {
            0% { opacity: 1; transform: translateX(-50%) translateY(0); }
            100% { opacity: 0; transform: translateX(-50%) translateY(12px); }
        }
        @keyframes fadeUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ===== Content Sections ===== */
        .content-section {
            position: relative;
            padding: 100px 0;
            min-height: 100vh;
            display: flex; align-items: center;
        }

        /* Section diffused background image */
        .section-bg {
            position: absolute; inset: 0; z-index: 0; overflow: hidden;
        }
        .section-bg-img {
            width: 100%; height: 100%; object-fit: cover;
            filter: blur(80px) saturate(1.3);
            opacity: 0.25;
            transform: scale(1.2);
        }
        .section-bg::after {
            content: ''; position: absolute; inset: 0;
            background: radial-gradient(ellipse at center, transparent 40%, var(--bg) 85%);
        }
        .section-bg-gradient {
            position: absolute; inset: 0;
            background: linear-gradient(180deg, var(--bg) 0%, transparent 30%, transparent 70%, var(--bg) 100%);
            z-index: 1;
        }

        /* Section inner content */
        .section-inner {
            position: relative; z-index: 2; width: 100%;
        }

        .section-label {
            font-size: 0.8rem; font-weight: 600; letter-spacing: 0.25em; text-transform: uppercase;
            margin-bottom: 12px; opacity: 0;
            transform: translateY(20px); transition: all 0.6s var(--transition);
        }
        .section-label.visible { opacity: 1; transform: translateY(0); }

        .section-label.l-purple { color: #a5b4fc; }
        .section-label.l-pink   { color: #f9a8d4; }
        .section-label.l-teal   { color: #5eead4; }

        .section-heading {
            font-size: clamp(2rem, 4vw, 3rem);
            font-weight: 700; letter-spacing: -0.025em;
            margin-bottom: 12px; opacity: 0;
            transform: translateY(20px); transition: all 0.6s var(--transition) 0.1s;
        }
        .section-heading.visible { opacity: 1; transform: translateY(0); }

        .section-desc {
            font-size: 1.05rem; color: var(--text-secondary);
            max-width: 500px; margin-bottom: 56px; opacity: 0;
            transform: translateY(20px); transition: all 0.6s var(--transition) 0.2s;
        }
        .section-desc.visible { opacity: 1; transform: translateY(0); }

        /* ===== Feature Cards (weakened card feel) ===== */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 24px;
        }

        .feature-item {
            padding: 36px 32px;
            border-radius: 24px;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all var(--transition);
            opacity: 0; transform: translateY(30px);
            background: rgba(255,255,255,0.015);
            border: 1px solid rgba(255,255,255,0.04);
        }
        .feature-item.visible { opacity: 1; transform: translateY(0); }

        .feature-item:hover {
            background: rgba(255,255,255,0.035);
            border-color: rgba(255,255,255,0.1);
            transform: translateY(-2px);
        }

        /* Diffused glow on hover */
        .feature-item::after {
            content: ''; position: absolute; inset: -1px; border-radius: 24px;
            opacity: 0; transition: opacity 0.6s;
            z-index: -1;
        }
        .feature-item.purple::after { background: radial-gradient(400px circle at var(--mx,50%) var(--my,50%), rgba(99,102,241,0.12), transparent 70%); }
        .feature-item.pink::after   { background: radial-gradient(400px circle at var(--mx,50%) var(--my,50%), rgba(236,72,153,0.12), transparent 70%); }
        .feature-item.teal::after   { background: radial-gradient(400px circle at var(--mx,50%) var(--my,50%), rgba(20,184,166,0.12), transparent 70%); }
        .feature-item:hover::after { opacity: 1; }

        .feature-icon {
            font-size: 2rem; margin-bottom: 20px; display: block;
            filter: grayscale(0.3); transition: filter 0.3s;
        }
        .feature-item:hover .feature-icon { filter: grayscale(0); }

        .feature-title {
            font-size: 1.1rem; font-weight: 600; letter-spacing: -0.01em;
            margin-bottom: 8px; line-height: 1.4;
        }
        .feature-subtitle {
            font-size: 0.88rem; color: var(--text-secondary); line-height: 1.6;
        }

        /* Hover reveal line */
        .feature-hover-line {
            font-size: 0.84rem; color: var(--text-tertiary); margin-top: 14px;
            line-height: 1.5; opacity: 0; transform: translateY(6px);
            transition: all var(--transition); font-style: italic;
        }
        .feature-item:hover .feature-hover-line {
            opacity: 1; transform: translateY(0); color: var(--text-secondary);
        }

        /* Expand area */
        .feature-expand {
            max-height: 0; opacity: 0; overflow: hidden;
            transition: all 0.55s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .feature-item.expanded .feature-expand {
            max-height: 600px; opacity: 1;
            margin-top: 22px; padding-top: 22px;
            border-top: 1px solid rgba(255,255,255,0.06);
        }
        .feature-expand ul { list-style: none; padding: 0; }
        .feature-expand li {
            padding: 9px 0; font-size: 0.88rem; color: var(--text-secondary);
            line-height: 1.6; position: relative; padding-left: 18px;
        }
        .feature-expand li::before {
            content: ''; position: absolute; left: 0; top: 17px;
            width: 5px; height: 5px; border-radius: 50%; opacity: 0.5;
        }
        .feature-item.purple .feature-expand li::before { background: var(--accent-purple); }
        .feature-item.pink   .feature-expand li::before { background: var(--accent-pink); }
        .feature-item.teal   .feature-expand li::before { background: var(--accent-teal); }

        /* Expand indicator */
        .expand-dot {
            position: absolute; top: 32px; right: 32px;
            width: 28px; height: 28px; border-radius: 50%;
            background: rgba(255,255,255,0.03);
            display: flex; align-items: center; justify-content: center;
            font-size: 0.65rem; color: var(--text-tertiary);
            transition: all var(--transition);
        }
        .feature-item:hover .expand-dot { background: rgba(255,255,255,0.06); }
        .feature-item.expanded .expand-dot { transform: rotate(45deg); }

        /* ===== Footer ===== */
        .footer {
            text-align: center; padding: 100px 0 40px; position: relative; z-index: 1;
        }
        .footer-line { width: 40px; height: 1px; background: rgba(255,255,255,0.08); margin: 0 auto 24px; }
        .footer-text { font-size: 0.8rem; color: var(--text-tertiary); letter-spacing: 0.05em; }

        /* ===== Back to top ===== */
        .back-top {
            position: fixed; bottom: 32px; right: 32px; z-index: 100;
            width: 44px; height: 44px; border-radius: 50%;
            background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08);
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; opacity: 0; pointer-events: none;
            transition: all 0.3s; font-size: 1.1rem; color: var(--text-secondary);
            backdrop-filter: blur(10px);
        }
        .back-top.show { opacity: 1; pointer-events: auto; }
        .back-top:hover { background: rgba(255,255,255,0.08); border-color: rgba(255,255,255,0.15); }

        /* ===== Responsive ===== */
        @media (max-width: 768px) {
            .container { padding: 0 20px; }
            .hero { padding: 80px 0 60px; min-height: auto; }
            .hero-quote { font-size: 1.6rem; }
            .hero-sub { font-size: 0.9rem; }
            .hero-nav { flex-direction: column; align-items: center; }
            .hero-nav-btn { width: 220px; text-align: center; }
            .features-grid { grid-template-columns: 1fr; }
            .feature-item { padding: 28px 24px; }
            .feature-hover-line { opacity: 1; transform: none; color: var(--text-secondary); }
            .content-section { padding: 60px 0; min-height: auto; }
        }

        ::selection { background: rgba(99,102,241,0.3); color: #fff; }
    </style>
</head>
<body>

    <!-- Ambient BG -->
    <div class="bg-ambient">
        <div class="bg-orb"></div>
        <div class="bg-orb"></div>
        <div class="bg-orb"></div>
    </div>
    <div class="grid-overlay"></div>

    <!-- ========== HERO ========== -->
    <section class="hero">
        <div class="container" style="display:flex;flex-direction:column;align-items:center;">
            <p class="hero-eyebrow">ABOUT ME</p>
            <h1 class="hero-quote">
                「我不是写公文的行政生——<br>
                我用<span class="hl-purple">小红书数据</span>帮品牌卖爆单品，<br>
                用<span class="hl-pink">公关思维</span>拆解每一篇爆文。」
            </h1>
            <p class="hero-sub">
                广东外语外贸大学 · 行政管理（公共关系方向）· 27届 · 求职产品营销/运营/市场/销售
            </p>
            <nav class="hero-nav">
                <a href="#section-wanggan" class="hero-nav-btn nav-purple">
                    有网感 <span class="btn-arrow">↓</span>
                </a>
                <a href="#section-chuangyi" class="hero-nav-btn nav-pink">
                    有创意 <span class="btn-arrow">↓</span>
                </a>
                <a href="#section-luoji" class="hero-nav-btn nav-teal">
                    逻辑总结能力强 <span class="btn-arrow">↓</span>
                </a>
            </nav>
        </div>
        <div class="scroll-indicator"><div class="scroll-mouse"></div></div>
    </section>

    <!-- ========== SECTION 1: 有网感 ========== -->
    <section class="content-section" id="section-wanggan">
        <div class="section-bg">
            <img class="section-bg-img" src="images/abstract_gradient_mesh__smooth_2026-06-11T03-27-07.png" alt="">
            <div class="section-bg-gradient"></div>
        </div>
        <div class="container section-inner">
            <p class="section-label l-purple">01 · 有网感</p>
            <h2 class="section-heading">数据嗅觉，<br>从评论区长出来。</h2>
            <p class="section-desc">用AI提效、用数据挖痛点、用持续拆解保持网感——不是天赋，是习惯。</p>

            <div class="features-grid">
                <!-- Feature 1 -->
                <div class="feature-item purple" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">🤖</span>
                    <h3 class="feature-title">评论区运维SOP + AI话术指令卡</h3>
                    <p class="feature-subtitle">把评论分5类，用DeepSeek批量生成"路人感"话术</p>
                    <p class="feature-hover-line">制定24h监控规则，自研指令卡（角色分配+动态槽+人工筛选），被机构复用</p>
                    <div class="feature-expand">
                        <ul>
                            <li>分类运维：提问向重点维护，新笔记24h内完成监控</li>
                            <li>指令卡设计：细节控40%+感性派30%+质疑者30%，植入随机语气词</li>
                            <li>人工筛选2-3分钟，剔除硬广词、重复句式</li>
                            <li>效果：评论区围绕核心卖点讨论，外溢数据稳定</li>
                        </ul>
                    </div>
                </div>

                <!-- Feature 2 -->
                <div class="feature-item purple" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">🌧️</span>
                    <h3 class="feature-title">"暴雨场景"怎么变成产品痛点</h3>
                    <p class="feature-subtitle">从400+条评论里挖出"下雨天翻车"高频词</p>
                    <p class="feature-hover-line">归类"淋雨""出汗""口罩闷"三大场景，建议达人植入后外溢超2000</p>
                    <div class="feature-expand">
                        <ul>
                            <li>扫描400+条评论，天气/出汗相关抱怨占27%</li>
                            <li>归类为：暴雨通勤、健身房暴汗、口罩闷妆</li>
                            <li>达人"存了个存"暴雨笔记外溢2500+</li>
                            <li>形成"天气痛点"选题模板，被产品团队采纳</li>
                        </ul>
                    </div>
                </div>

                <!-- Feature 3 -->
                <div class="feature-item purple" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">📝</span>
                    <h3 class="feature-title">爆文拆解周记</h3>
                    <p class="feature-subtitle">每两周拆3篇低粉爆文，非工作需求</p>
                    <p class="feature-hover-line">分析标题结构、封面套路、评论区高频词，整理成飞书表格</p>
                    <div class="feature-expand">
                        <ul>
                            <li>示例拆解："素人宿舍改造"爆文核心是"前后对比+预算清单"</li>
                            <li>可复用方法：痛点场景前置、数据可视化、评论区埋"帮选型"</li>
                            <li>持续更新，证明网感来自持续输入</li>
                            <li>拆解文档可随时分享</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ========== SECTION 2: 有创意 ========== -->
    <section class="content-section" id="section-chuangyi">
        <div class="section-bg">
            <img class="section-bg-img" src="images/abstract_gradient_mesh__smooth_2026-06-11T03-27-08.png" alt="">
            <div class="section-bg-gradient"></div>
        </div>
        <div class="container section-inner">
            <p class="section-label l-pink">02 · 有创意</p>
            <h2 class="section-heading">内容逻辑，<br>比堆卖点更重要。</h2>
            <p class="section-desc">从0到爆文、从秋冬到春夏——创意是给同一件产品，找到新的语言。</p>

            <div class="features-grid">
                <!-- Feature 4 -->
                <div class="feature-item pink" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">✏️</span>
                    <h3 class="feature-title">一篇稿件修改前后</h3>
                    <p class="feature-subtitle">外溢从0到超1500</p>
                    <p class="feature-hover-line">初稿痛点模糊、卖点混乱、硬广感强；3条修改方向后成为爆文</p>
                    <div class="feature-expand">
                        <ul>
                            <li>原稿问题：痛点头不具体、先讲技术后讲质地、结尾像品牌喊话</li>
                            <li>修改：开头"换季起皮+卡粉"，卖点顺序"质地→感受→技术"，结尾"我终于悟了"</li>
                            <li>达人"去班味义工"因这篇获后续合作</li>
                            <li>经验：内容逻辑比堆卖点更重要</li>
                        </ul>
                    </div>
                </div>

                <!-- Feature 5 -->
                <div class="feature-item pink" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">🔄</span>
                    <h3 class="feature-title">换季，给同一款产品换张"脸"</h3>
                    <p class="feature-subtitle">贴贴霜从"秋冬滋润"转"春夏清爽"</p>
                    <p class="feature-hover-line">对比评论区高频词，推动卖点转向"水润不油腻+持妆完整+精简妆前三合一"</p>
                    <div class="feature-expand">
                        <ul>
                            <li>数据支撑：5月21篇笔记中"水润不油腻"出现30+次</li>
                            <li>动作：Brief增加"空调房""通勤""户外"场景关键词</li>
                            <li>验证："暴雨"笔记外溢2500+，证明场景切换有效</li>
                            <li>思路被产品团队采纳用于后续合作方向</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ========== SECTION 3: 逻辑总结能力强 ========== -->
    <section class="content-section" id="section-luoji">
        <div class="section-bg">
            <img class="section-bg-img" src="images/abstract_gradient_mesh__smooth_2026-06-11T03-27-11.png" alt="">
            <div class="section-bg-gradient"></div>
        </div>
        <div class="container section-inner">
            <p class="section-label l-teal">03 · 逻辑总结能力强</p>
            <h2 class="section-heading">把感觉，<br>变成可复用的系统。</h2>
            <p class="section-desc">审稿能打分、流程能压缩80%——逻辑不是纸上谈兵，是真实提效。</p>

            <div class="features-grid">
                <!-- Feature 7 -->
                <div class="feature-item teal" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">📋</span>
                    <h3 class="feature-title">审稿SOP：从"感觉"到"打分表"</h3>
                    <p class="feature-subtitle">5个维度 + 4级痛点，可量化审核</p>
                    <p class="feature-hover-line">拆出痛点命中、核心卖点、形容词语等维度；干皮痛点按严重程度分4级</p>
                    <div class="feature-expand">
                        <ul>
                            <li>审核维度：痛点命中(≥1)、核心卖点(≥2)、形容词语(≥2)、字数200-300、禁止堆砌技术词</li>
                            <li>痛点等级：1上妆卡纹→2越补越脏→3混干尴尬→4搓泥</li>
                            <li>效果：审稿效率提升，被带教认可并复用</li>
                            <li>可迁移：这套方法可用于任何产品的内容审核</li>
                        </ul>
                    </div>
                </div>

                <!-- Feature 9 -->
                <div class="feature-item teal" onclick="toggleFeature(this)">
                    <div class="expand-dot">+</div>
                    <span class="feature-icon">⚡</span>
                    <h3 class="feature-title">把300人次的团员事务处理时间压缩80%</h3>
                    <p class="feature-subtitle">标准化Checklist + 线上预填问卷</p>
                    <p class="feature-hover-line">发现线下填表错误率90%来自材料缺漏，用工具和流程改造解决问题</p>
                    <div class="feature-expand">
                        <ul>
                            <li>问题诊断：90%跑腿因材料缺漏或格式错误</li>
                            <li>方案：① Checklist发给支书 ② 问卷星预填校验 ③ 集中办理时段</li>
                            <li>结果：错误率降80%，单人次15分钟→3分钟</li>
                            <li>模式被其他学生组织借鉴，可迁移到运营岗位</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <div class="footer-line"></div>
            <p class="footer-text">© 2026</p>
        </div>
    </footer>

    <!-- Back to top -->
    <div class="back-top" id="backTop" onclick="window.scrollTo({top:0,behavior:'smooth'})">↑</div>

    <script>
        // ===== Feature toggle =====
        function toggleFeature(el) {
            const was = el.classList.contains('expanded');
            document.querySelectorAll('.feature-item.expanded').forEach(f => f.classList.remove('expanded'));
            if (!was) el.classList.add('expanded');
        }

        // Mouse glow tracking
        document.querySelectorAll('.feature-item').forEach(el => {
            el.addEventListener('mousemove', e => {
                const r = el.getBoundingClientRect();
                el.style.setProperty('--mx', ((e.clientX - r.left) / r.width * 100) + '%');
                el.style.setProperty('--my', ((e.clientY - r.top) / r.height * 100) + '%');
            });
        });

        // Close expanded on Escape
        document.addEventListener('keydown', e => {
            if (e.key === 'Escape') {
                document.querySelectorAll('.feature-item.expanded').forEach(f => f.classList.remove('expanded'));
            }
        });

        // Close expanded on outside click
        document.addEventListener('click', e => {
            if (!e.target.closest('.feature-item')) {
                document.querySelectorAll('.feature-item.expanded').forEach(f => f.classList.remove('expanded'));
            }
        });

        // ===== Scroll animations =====
        const obs = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, { threshold: 0.08, rootMargin: '0px 0px -40px 0px' });

        document.querySelectorAll('.section-label, .section-heading, .section-desc, .feature-item').forEach(el => {
            obs.observe(el);
        });

        // ===== Back to top =====
        const backTop = document.getElementById('backTop');
        window.addEventListener('scroll', () => {
            backTop.classList.toggle('show', window.scrollY > 600);
        });
    </script>
</body>
</html>
