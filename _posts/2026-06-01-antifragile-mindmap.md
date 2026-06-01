---
layout: post
title: "《反脆弱》— 思维导图与交互脑图"
date: 2026-06-01
categories: [reading, philosophy]
tags: [antifragile, Taleb, 思维导图, 可视化]
---

<!-- Part A: 结构化思维导图 -->
<style>
  .af-hero {
    text-align: center;
    padding: 60px 20px 40px;
    background: linear-gradient(135deg, #FEF6E8 0%, #F5F2ED 50%, #FEF6E8 100%);
    position: relative;
    overflow: hidden;
  }

  .af-hero::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle at 30% 50%, rgba(192, 57, 43, 0.1) 0%, transparent 40%),
                radial-gradient(circle at 70% 50%, rgba(124, 185, 168, 0.1) 0%, transparent 40%);
    animation: af-pulse 8s ease-in-out infinite;
    opacity: 0.4;
  }

  @keyframes af-pulse {
    0%, 100% { transform: scale(1); opacity: 0.4; }
    50% { transform: scale(1.1); opacity: 0.6; }
  }

  .af-hero-content { position: relative; z-index: 1; }

  .af-hero h1 {
    font-size: clamp(2.5rem, 6vw, 4rem);
    font-weight: 900;
    background: linear-gradient(135deg, #c0392b, #E8A45C, #7CB9A8);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 10px;
    letter-spacing: 0.1em;
  }

  .af-hero .af-subtitle {
    font-size: clamp(1rem, 2.5vw, 1.4rem);
    color: #718096;
    font-weight: 300;
    margin-bottom: 20px;
  }

  .af-hero .af-quote {
    font-size: clamp(1rem, 2vw, 1.2rem);
    color: #E8A45C;
    font-style: italic;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px 30px;
    border-left: 3px solid #E8A45C;
    background: rgba(232, 164, 92, 0.05);
    border-radius: 0 8px 8px 0;
  }

  .af-legend {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin-top: 30px;
    flex-wrap: wrap;
  }

  .af-legend-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 0.9rem;
    color: #718096;
  }

  .af-legend-dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
  }

  .af-legend-dot.af-fragile { background: #c0392b; box-shadow: 0 0 8px rgba(192, 57, 43, 0.1); }
  .af-legend-dot.af-robust { background: #5A9A8A; box-shadow: 0 0 8px rgba(90, 154, 138, 0.1); }
  .af-legend-dot.af-antifragile { background: #7CB9A8; box-shadow: 0 0 8px rgba(124, 185, 168, 0.1); }

  /* Triad Section */
  .af-triad {
    padding: 40px 20px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .af-triad h2 {
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 30px;
    color: #4A5568;
  }

  .af-triad-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-bottom: 40px;
  }

  .af-triad-card {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 28px;
    border: 1px solid #E8E4DE;
    transition: transform 0.3s, box-shadow 0.3s;
    position: relative;
    overflow: hidden;
  }

  .af-triad-card:hover {
    transform: translateY(-4px);
  }

  .af-triad-card.af-fragile {
    border-top: 3px solid #c0392b;
    box-shadow: 0 4px 20px rgba(192, 57, 43, 0.1);
  }

  .af-triad-card.af-robust {
    border-top: 3px solid #5A9A8A;
    box-shadow: 0 4px 20px rgba(90, 154, 138, 0.1);
  }

  .af-triad-card.af-antifragile {
    border-top: 3px solid #7CB9A8;
    box-shadow: 0 4px 20px rgba(124, 185, 168, 0.1);
  }

  .af-triad-card .af-icon {
    font-size: 2.5rem;
    margin-bottom: 12px;
  }

  .af-triad-card h3 {
    font-size: 1.4rem;
    margin-bottom: 8px;
  }

  .af-triad-card.af-fragile h3 { color: #c0392b; }
  .af-triad-card.af-robust h3 { color: #5A9A8A; }
  .af-triad-card.af-antifragile h3 { color: #7CB9A8; }

  .af-triad-card .af-myth {
    font-size: 0.85rem;
    color: #718096;
    margin-bottom: 12px;
    padding: 6px 12px;
    background: rgba(0,0,0,0.02);
    border-radius: 6px;
    display: inline-block;
  }

  .af-triad-card p {
    font-size: 0.95rem;
    color: #718096;
    line-height: 1.8;
  }

  .af-triad-card .af-trait-list {
    list-style: none;
    margin-top: 12px;
  }

  .af-triad-card .af-trait-list li {
    padding: 4px 0;
    font-size: 0.9rem;
    color: #718096;
    position: relative;
    padding-left: 20px;
  }

  .af-triad-card .af-trait-list li::before {
    content: '\25B8';
    position: absolute;
    left: 0;
  }

  .af-triad-card.af-fragile .af-trait-list li::before { color: #c0392b; }
  .af-triad-card.af-robust .af-trait-list li::before { color: #5A9A8A; }
  .af-triad-card.af-antifragile .af-trait-list li::before { color: #7CB9A8; }

  /* Book Structure */
  .af-book-structure {
    padding: 40px 20px;
    max-width: 1400px;
    margin: 0 auto;
  }

  .af-book-structure h2 {
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 10px;
    color: #4A5568;
  }

  .af-book-structure .af-subtitle-text {
    text-align: center;
    color: #718096;
    margin-bottom: 40px;
    font-size: 0.95rem;
  }

  .af-volume {
    margin-bottom: 30px;
    border-radius: 16px;
    background: #FFFFFF;
    border: 1px solid #E8E4DE;
    overflow: hidden;
    transition: box-shadow 0.3s;
  }

  .af-volume:hover {
    box-shadow: 0 0 30px rgba(0,0,0,0.03);
  }

  .af-volume summary {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 20px 28px;
    cursor: pointer;
    transition: background 0.3s;
    user-select: none;
    list-style: none;
  }

  .af-volume summary::-webkit-details-marker { display: none; }
  .af-volume summary::marker { display: none; content: ''; }

  .af-volume summary:hover {
    background: rgba(0,0,0,0.02);
  }

  .af-volume-num {
    font-size: 2rem;
    font-weight: 900;
    min-width: 50px;
  }

  .af-volume.af-v1 .af-volume-num { color: #c0392b; }
  .af-volume.af-v2 .af-volume-num { color: #E8A45C; }
  .af-volume.af-v3 .af-volume-num { color: #8e44ad; }
  .af-volume.af-v4 .af-volume-num { color: #2980b9; }
  .af-volume.af-v5 .af-volume-num { color: #16a085; }
  .af-volume.af-v6 .af-volume-num { color: #7CB9A8; }
  .af-volume.af-v7 .af-volume-num { color: #f39c12; }

  .af-volume-title {
    flex: 1;
  }

  .af-volume-title h3 {
    font-size: 1.2rem;
    color: #4A5568;
  }

  .af-volume-title .af-vol-insight {
    font-size: 0.85rem;
    color: #E8A45C;
    margin-top: 4px;
  }

  .af-volume-toggle {
    font-size: 1.2rem;
    color: #718096;
    transition: transform 0.3s;
    display: inline-block;
  }

  .af-volume[open] > summary .af-volume-toggle {
    transform: rotate(90deg);
  }

  .af-volume-content {
    padding: 0 28px 28px;
    border-top: 1px solid #E8E4DE;
  }

  .af-chapter {
    margin-top: 20px;
    padding: 20px;
    background: rgba(0,0,0,0.01);
    border-radius: 12px;
  }

  .af-chapter summary {
    cursor: pointer;
    list-style: none;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 12px;
    margin-bottom: 0;
  }

  .af-chapter summary::-webkit-details-marker { display: none; }
  .af-chapter summary::marker { display: none; content: ''; }

  .af-chapter[open] > summary {
    margin-bottom: 12px;
  }

  .af-volume.af-v1 .af-chapter { border-left: 3px solid #c0392b; }
  .af-volume.af-v2 .af-chapter { border-left: 3px solid #E8A45C; }
  .af-volume.af-v3 .af-chapter { border-left: 3px solid #8e44ad; }
  .af-volume.af-v4 .af-chapter { border-left: 3px solid #2980b9; }
  .af-volume.af-v5 .af-chapter { border-left: 3px solid #16a085; }
  .af-volume.af-v6 .af-chapter { border-left: 3px solid #7CB9A8; }
  .af-volume.af-v7 .af-chapter { border-left: 3px solid #f39c12; }

  .af-chapter h4 {
    font-size: 1.05rem;
    color: #4A5568;
    font-weight: 700;
  }

  .af-chapter .af-ch-num {
    font-size: 0.75rem;
    color: #718096;
    background: rgba(0,0,0,0.03);
    padding: 2px 8px;
    border-radius: 10px;
    white-space: nowrap;
  }

  .af-chapter .af-core-idea {
    font-size: 0.9rem;
    color: #E8A45C;
    margin-bottom: 10px;
    font-weight: 500;
  }

  .af-chapter .af-details {
    font-size: 0.88rem;
    color: #718096;
    line-height: 1.8;
  }

  .af-chapter .af-details strong {
    color: #4A5568;
    font-weight: 500;
  }

  .af-insight-box {
    margin-top: 12px;
    padding: 12px 16px;
    background: rgba(124, 185, 168, 0.08);
    border: 1px solid rgba(124, 185, 168, 0.08);
    border-radius: 8px;
    font-size: 0.85rem;
    color: #7CB9A8;
    line-height: 1.7;
  }

  .af-insight-box .af-label {
    font-weight: 700;
    margin-right: 4px;
  }

  /* Philosophy Deep Dive */
  .af-philosophy {
    padding: 40px 20px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .af-philosophy h2 {
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 40px;
    color: #4A5568;
  }

  .af-philosophy-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 20px;
  }

  .af-philo-card {
    background: #FFFFFF;
    border-radius: 16px;
    padding: 24px;
    border: 1px solid #E8E4DE;
    transition: transform 0.3s;
  }

  .af-philo-card:hover { transform: translateY(-3px); }

  .af-philo-card h4 {
    font-size: 1.1rem;
    color: #7CB9A8;
    margin-bottom: 10px;
  }

  .af-philo-card p {
    font-size: 0.9rem;
    color: #718096;
    line-height: 1.8;
  }

  .af-philo-card .af-vs {
    display: flex;
    gap: 10px;
    margin: 10px 0;
    align-items: center;
  }

  .af-philo-card .af-vs span {
    padding: 4px 12px;
    border-radius: 6px;
    font-size: 0.82rem;
    font-weight: 500;
  }

  .af-philo-card .af-vs .af-left { background: rgba(192,57,43,0.08); color: #c0392b; }
  .af-philo-card .af-vs .af-right { background: rgba(124,185,168,0.08); color: #7CB9A8; }
  .af-philo-card .af-vs .af-mid { color: #718096; font-size: 0.8rem; }

  /* Actionable Principles */
  .af-principles {
    padding: 40px 20px;
    max-width: 1000px;
    margin: 0 auto;
  }

  .af-principles h2 {
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 40px;
    color: #4A5568;
  }

  .af-principle-item {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
    padding: 20px;
    background: #FFFFFF;
    border-radius: 12px;
    border: 1px solid #E8E4DE;
    align-items: flex-start;
  }

  .af-principle-num {
    font-size: 2rem;
    font-weight: 900;
    color: #7CB9A8;
    min-width: 40px;
  }

  .af-principle-item h4 {
    font-size: 1rem;
    color: #4A5568;
    margin-bottom: 6px;
  }

  .af-principle-item p {
    font-size: 0.88rem;
    color: #718096;
    line-height: 1.7;
  }

  /* Footer */
  .af-footer {
    text-align: center;
    padding: 40px 20px;
    color: #718096;
    font-size: 0.85rem;
    border-top: 1px solid #E8E4DE;
  }

  .af-footer .af-final-quote {
    font-size: 1.1rem;
    color: #E8A45C;
    margin-bottom: 16px;
    font-style: italic;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .af-hero h1 { font-size: 2rem; }
    .af-triad-grid { grid-template-columns: 1fr; }
    .af-philosophy-grid { grid-template-columns: 1fr; }
    .af-volume summary { padding: 16px 20px; }
    .af-volume-content { padding: 0 16px 16px; }
    .af-chapter { padding: 14px; }
    .af-principle-item { flex-direction: column; }
  }
</style>

<!-- ==================== HERO ==================== -->
<section class="af-hero">
  <div class="af-hero-content">
    <h1>反 脆 弱</h1>
    <div class="af-subtitle">Antifragile: Things That Gain from Disorder</div>
    <div class="af-subtitle">纳西姆·尼古拉斯·塔勒布 — 思想全景思维导图</div>
    <div class="af-quote">
      "风会熄灭蜡烛，却能使火越烧越旺。<br>对随机性、不确定性和混沌也是一样：你要利用它们，而不是躲避它们。<br>你要成为火，渴望得到风的吹拂。"
    </div>
    <div class="af-legend">
      <div class="af-legend-item"><div class="af-legend-dot af-fragile"></div>脆弱类 — 压力下受损</div>
      <div class="af-legend-item"><div class="af-legend-dot af-robust"></div>强韧类 — 压力下不变</div>
      <div class="af-legend-item"><div class="af-legend-dot af-antifragile"></div>反脆弱类 — 压力下获益</div>
    </div>
  </div>
</section>

<!-- ==================== 核心三元结构 ==================== -->
<section class="af-triad">
  <h2>核心三元结构：脆弱 — 强韧 — 反脆弱</h2>

  <div class="af-triad-grid">
    <div class="af-triad-card af-fragile">
      <div class="af-icon">&#x1F5E1;&#xFE0F;</div>
      <h3>脆弱</h3>
      <div class="af-myth">隐喻：达摩克利斯之剑</div>
      <p>权力越大，悬剑越险。一根马鬃即可毁掉一切。</p>
      <ul class="af-trait-list">
        <li>厌恶波动性、随机性和压力</li>
        <li>暴露于负面"黑天鹅"中</li>
        <li>优化与效率导向（效率=无冗余=脆弱）</li>
        <li>厌恶错误，错误不可逆且致命</li>
        <li>集权、大规模、单一模式</li>
        <li>自上而下的设计与控制</li>
        <li>约翰博士：稳定收入但一裁即溃</li>
      </ul>
    </div>

    <div class="af-triad-card af-robust">
      <div class="af-icon">&#x1F525;</div>
      <h3>强韧</h3>
      <div class="af-myth">隐喻：凤凰</div>
      <p>从灰烬中重生，恢复原状——但不会变得更好。</p>
      <ul class="af-trait-list">
        <li>抵抗冲击，保持原状</li>
        <li>冗余提供缓冲，但无成长</li>
        <li>错误只是信息，不会致命</li>
        <li>贝鲁特7次被毁7次重建——但仍是贝鲁特</li>
        <li>经验主义、习惯法、启发法</li>
        <li>城邦制、分权式</li>
        <li>尼罗·图利普：观察但不参与</li>
      </ul>
    </div>

    <div class="af-triad-card af-antifragile">
      <div class="af-icon">&#x1F409;</div>
      <h3>反脆弱</h3>
      <div class="af-myth">隐喻：九头蛇怪</div>
      <p>砍掉一个头，长出两个头。伤害成为成长的燃料。</p>
      <ul class="af-trait-list">
        <li>从波动性、压力、混乱中茁壮成长</li>
        <li>暴露于正面"黑天鹅"之中</li>
        <li>喜欢错误（微小的），从中进化</li>
        <li>毒物兴奋效应、过度补偿、创伤后成长</li>
        <li>自下而上的自由探索与试错</li>
        <li>杠铃策略、可选择性、凸性效应</li>
        <li>胖子托尼：直觉嗅出脆弱，揩脆弱推手的油</li>
      </ul>
    </div>
  </div>

  <div class="af-insight-box" style="max-width:900px;margin:0 auto;">
    <span class="af-label">深层洞察：</span>塔勒布的核心发现是，我们语言和思维中缺少"反脆弱"这个词，导致我们只看到脆弱与强韧，却忽略了从混乱中获益的整个维度。这不仅是概念缺失，而是文明层面的盲点——现代性系统性否定反脆弱性，试图消除一切波动，结果制造了更大的系统性脆弱。反脆弱性不是一个词，而是一整套世界观。
  </div>
</section>

<!-- ==================== 七卷思想脉络 ==================== -->
<section class="af-book-structure">
  <h2>七卷思想脉络：从概念到伦理</h2>
  <div class="af-subtitle-text">点击各卷展开详细思想导图</div>

  <!-- 第一卷 -->
  <details class="af-volume af-v1" open>
    <summary>
      <div class="af-volume-num">I</div>
      <div class="af-volume-title">
        <h3>反脆弱性：介绍</h3>
        <div class="af-vol-insight">核心命题：什么是反脆弱性？为何它被系统性忽略？</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第1章 达摩克利斯之剑和九头蛇怪</h4>
          <span class="af-ch-num">核心概念章</span>
        </summary>
        <div class="af-core-idea">脆弱-强韧-反脆弱三元结构的建立</div>
        <div class="af-details">
          <strong>达摩克利斯之剑</strong>：权力的副作用是持续危险，成功越辉煌剑越危险。一根马鬃断裂，一切化为乌有。<br>
          <strong>凤凰</strong>：从灰烬中重生，但只是恢复原状，并非变得更强。<br>
          <strong>九头蛇怪</strong>：砍掉一个头长出两个，伤害反而成为成长的燃料。<br><br>
          <strong>领域依赖性</strong>：人们在一个领域理解毒物兴奋效应（医疗），却无法将其迁移到经济、社会等其他领域。这是反脆弱性被忽略的认知根源。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>语言中没有"反脆弱"这个词，本身就是认知盲点的证据。我们谈论"强韧"、"复原力"，却无法描述那些从混乱中获益的事物——而恰恰是这些事物驱动了进化、创新和文化繁荣。缺少词汇=缺少思维框架=缺少行动指南。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第2章 随处可见的过度补偿和过度反应</h4>
          <span class="af-ch-num">机制章</span>
        </summary>
        <div class="af-core-idea">反脆弱性的初级机制：过度补偿</div>
        <div class="af-details">
          <strong>毒物兴奋效应（Hormesis）</strong>：小剂量有害物质反而有益——受到15毫克毒物后，机体能承受20毫克甚至更多。<br>
          <strong>米特拉达梯式解毒法</strong>：逐渐增加毒物剂量，最终获得免疫力。<br>
          <strong>创伤后成长</strong>：与创伤后应激障碍相对，许多人在伤害后超越自我。<br>
          <strong>冗余</strong>：反脆弱性表现为某种形式的冗余（两个肾脏、九头蛇怪多出的头）。<br><br>
          缺乏压力源反而有害——航空自动化降低飞行员挑战，导致技能钝化和事故。现代试图在舒适环境中创新是谬论——"必要性是发明之母"。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>过度补偿的本质是非线性响应：系统的反应超过刺激本身。这是反脆弱性的物理基础——不是"刚好恢复"，而是"过度恢复"，从而实现进化性超越。对某事的痴迷是最具反脆弱性的状态，因为痴迷者从每一次挫折中汲取更多能量。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第3章 猫与洗衣机</h4>
          <span class="af-ch-num">本体论章</span>
        </summary>
        <div class="af-core-idea">有机体需要压力源，机械体需要减少压力</div>
        <div class="af-details">
          <strong>猫</strong>：有机体——有反脆弱性，能自我修复，从压力中变得更强。<br>
          <strong>洗衣机</strong>：机械体——会损耗、破败，无法自我修复，压力只会加速退化。<br><br>
          <strong>沃尔夫定律</strong>：骨骼在压力下骨密度上升。<br>
          <strong>两种压力源</strong>：急性刺激+恢复（有益）vs 慢性低水平压力（有害，如房贷、通勤）。<br>
          <strong>观光化</strong>：将不确定性从生活中清除出去的企图——相当于给有机体施加洗衣机的逻辑。<br><br>
          衰老不是自然老化，而是功能失调——个体功能与环境随机性结构的错配。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>"猫与洗衣机"揭示了反脆弱性的本体论基础：不是所有事物都能从压力中获益，只有具有内在修复和超越机制的复杂系统才能。将有机体当作机械体管理（现代医疗、教育、企业管理的通病），就是剥夺其反脆弱性。赫拉克勒斯灼烧九头蛇伤口——阻止其恢复——恰恰是干扰反脆弱性最形象的行为隐喻。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第4章 杀死我的东西却让其他人更强壮</h4>
          <span class="af-ch-num">层级章</span>
        </summary>
        <div class="af-core-idea">整体的反脆弱性建立在个体的脆弱性之上</div>
        <div class="af-details">
          <strong>餐馆集群</strong>：个别餐馆脆弱易倒闭，但餐饮业整体具有反脆弱性。<br>
          <strong>进化逻辑</strong>：个体必须死亡，基因库才能改进。不死的有机体需完美预测未来（不可能），有限生命只需模糊方向。<br>
          <strong>反脆弱性层级</strong>：毒物兴奋效应（个体从危害中受益）< 进化（个体死亡，集体受益）。<br>
          <strong>抗生素耐药性</strong>：越努力杀灭细菌，幸存细菌越顽强。<br><br>
          向创业者和冒险者致敬——他们的失败为集体提供了反脆弱性。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>这一章的思想内核极其深刻：死亡是生命反脆弱性的必要条件。没有个体的终结，就没有进化的空间。现代社会的"让所有人都活得长久"的冲动，实际上是在消除系统层面的反脆弱性。火鸡悖论——为保护火鸡而阻止波动性——结果导致更大的系统性崩溃。
        </div>
      </details>
    </div>
  </details>

  <!-- 第二卷 -->
  <details class="af-volume af-v2">
    <summary>
      <div class="af-volume-num">II</div>
      <div class="af-volume-title">
        <h3>现代化与对反脆弱性的否定</h3>
        <div class="af-vol-insight">核心命题：现代性如何系统性地破坏反脆弱性？</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第5章 露天市场与办公楼</h4>
          <span class="af-ch-num">对比章</span>
        </summary>
        <div class="af-core-idea">表面稳定的系统实则脆弱，表面波动的系统实则反脆弱</div>
        <div class="af-details">
          <strong>约翰（银行员工）vs 乔治（出租车司机）</strong>：约翰收入稳定但隐性风险巨大（裁员即崩溃）；乔治收入波动但反脆弱（持续压力保持竞争力）。<br>
          <strong>瑞士城邦制</strong>：无中央政府、自下而上治理，最具反脆弱性。讽刺的是列宁在苏黎世——集权蓝图设计师栖息在最反脆弱的地方。<br>
          <strong>隐性风险 vs 显性风险</strong>：雇员风险隐性（看不见），自雇人士风险显性（持续感知并调整）。<br><br>
          波动性传递信息：技术工人不断从环境中学习调整；集权制消除波动=消除信息=积累隐性风险。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>"稳定即脆弱"是全书最反直觉的命题。表面的稳定往往是风险积累的遮羞布——波动被压制不代表风险被消除，而是被转化为更致命的隐性风险。市场创下"两年新低"比"一年新低"导致更多损失——平静期越长，崩溃越惨烈。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第6章 告诉他们我爱随机性</h4>
          <span class="af-ch-num">机制章</span>
        </summary>
        <div class="af-core-idea">随机性是反脆弱性系统的必需燃料</div>
        <div class="af-details">
          <strong>布里丹之驴</strong>：饥渴的驴在等距的食物和水间犹豫至死，一阵随机微风即可解救。<br>
          <strong>森林火灾</strong>：定期小火灾清洗易燃物，系统预防火灾反而导致更大灾难。<br>
          <strong>随机共振</strong>：添加背景噪声让微弱信号被听见。<br>
          <strong>模拟退火</strong>：原子随机漫游后冷却找到更优结构。<br>
          <strong>麦克斯韦调节器</strong>：严密控制蒸汽机速度反而导致不稳定。<br><br>
          古代雅典议会成员抽签决定，旨在保护系统免于退化。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>随机性不是噪声，而是信号的营养。系统需要"洗牌"来防止僵化和退化——市场需要波动来淘汰弱者，生物需要变异来适应环境，思想需要挑战来保持活力。消除随机性=消除进化压力=积累脆弱性。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第7章 天真的干预</h4>
          <span class="af-ch-num">批判章</span>
        </summary>
        <div class="af-core-idea">天真的干预导致医源性损伤——治疗比疾病更危险</div>
        <div class="af-details">
          <strong>医源性损伤</strong>：净损失超过治疗益处的损害，通常被隐藏或延迟。<br>
          <strong>扁桃体手术</strong>：389名儿童中325名被建议手术，实际发病率仅2-4%，每15000名手术患者1人死亡。<br>
          <strong>乔治·华盛顿之死</strong>：放血5-9磅加速死亡。<br>
          <strong>塞梅尔维斯</strong>：发现医院死亡率高于家中分娩，被同行迫害致死。<br><br>
          医疗失误死亡率是车祸的3-10倍。希波克拉底誓言"以不伤害为前提"花了24个世纪才执行。其他领域（政治、经济、教育）对医源性损伤仍一无所知。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>"天真的干预"是现代性最隐蔽的暴力形式。其逻辑是"必须做些什么"——但什么都不做往往更好。干预的收益是可见的、即时的，而伤害是隐蔽的、延迟的。这种信息不对称使得医源性损伤在所有领域持续蔓延。否认反脆弱性导致伤害——因为系统本可自愈，干预反而破坏了自愈机制。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第8章 预测是现代化的产物</h4>
          <span class="af-ch-num">认识论章</span>
        </summary>
        <div class="af-core-idea">预测带来医源性损伤，反脆弱系统不需要精确预测</div>
        <div class="af-details">
          <strong>第四象限</strong>："黑天鹅"领域——罕见而不可预测的高风险领域。<br>
          <strong>两类领域</strong>：可预测的物理世界 vs 不可预测的社会经济世界。<br>
          <strong>给人预测数据</strong>：即使知道预测不准确，仍会增加承担风险的行为。<br><br>
          福岛事故后，正确做法不是改进预测，而是建立更小、更深的反应堆。消除人类贪婪的努力几千年来毫无效果——正确做法是让世界抵御贪婪的影响，甚至从贪婪中获益。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>洞察反脆弱性比预测事件容易得多。脆弱性是可以衡量的（当前属性），但风险是不可衡量的（未来概率）。这是一个根本性的认识论转向：从"预测未来"转向"识别脆弱"。不需要知道暴风雨何时来，只需确保你的房子不是纸做的。
        </div>
      </details>
    </div>
  </details>

  <!-- 第三卷 -->
  <details class="af-volume af-v3">
    <summary>
      <div class="af-volume-num">III</div>
      <div class="af-volume-title">
        <h3>非预测性的世界观</h3>
        <div class="af-vol-insight">核心命题：不预测未来，如何从不确定性中获益？</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第9章 胖子托尼与脆弱推手</h4>
          <span class="af-ch-num">人物章</span>
        </summary>
        <div class="af-core-idea">实用主义智慧直觉性地识别脆弱性</div>
        <div class="af-details">
          <strong>胖子托尼</strong>：代表实践智慧——不需要理论就能嗅出脆弱，通过"揩脆弱推手的油水"获利。<br>
          <strong>脆弱推手</strong>：制造系统性脆弱性的人（银行家、经济学家），自己却远离风险，将后果转嫁给他人。<br>
          <strong>尼罗的长午餐</strong>：通过长期观察理解随机性，而非依赖理论。<br><br>
          脆弱推手的核心特征：西装革履、开会、坐在桌前——他们看不到自己不理解的东西，将未知误认为不存在。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第10章 塞内加的不利因素和有利因素</h4>
          <span class="af-ch-num">哲学章</span>
        </summary>
        <div class="af-core-idea">反脆弱性的核心：有利因素永远大于不利因素</div>
        <div class="af-details">
          <strong>斯多葛学派的智慧</strong>：专注于可控的事物（内在态度），而非不可控的外部事件。<br>
          <strong>不对称性原理</strong>：反脆弱系统的损失有限、收益无限——这是反脆弱的数学本质。<br>
          <strong>塞内加的实践</strong>：定期在心理上"失去"一切，从而对真正的损失免疫——在波动中保持有利地位。<br><br>
          特法特教授拒绝服用自己开的药——理论家不实践自己的理论，这是脆弱推手的原型。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>塞内加的智慧不仅是心理策略，更是反脆弱性的结构设计：通过改变自己对不利因素的暴露方式，将"不利因素>有利因素"翻转为"有利因素>不利因素"。这是杠铃策略的哲学原型——在精神层面实现不对称性。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第11章 千万别嫁给摇滚明星</h4>
          <span class="af-ch-num">策略章</span>
        </summary>
        <div class="af-core-idea">杠铃策略：极端保守 + 极端冒险，避开中间地带</div>
        <div class="af-details">
          <strong>杠铃策略</strong>：90%极度保守（确保生存）+ 10%极度冒险（获取巨大收益），避免"中庸"的脆弱性。<br>
          <strong>什么可以混合，什么不可以</strong>：不是所有东西都能安全混合——杠铃策略就是在不可混合的领域保持分离。<br>
          <strong>从脆弱到反脆弱</strong>：杠铃策略可以将任何脆弱系统转变为反脆弱系统。<br><br>
          职业杠铃：稳定的主业+高风险高回报的副业。投资杠铃：大部分安全资产+小部分极端投机。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>杠铃策略的深刻之处在于它是对"中庸之道"的否定。"中庸"看似安全实则最脆弱——中等风险既无法确保生存，又无法获得超额收益。真正的安全来自一端确保底线，另一端无限向上。这颠覆了传统风险管理中"分散风险到中间地带"的教条。
        </div>
      </details>
    </div>
  </details>

  <!-- 第四卷 -->
  <details class="af-volume af-v4">
    <summary>
      <div class="af-volume-num">IV</div>
      <div class="af-volume-title">
        <h3>可选择性、技术与反脆弱性的智慧</h3>
        <div class="af-vol-insight">核心命题：创新从何而来？自由探索为何优于顶层设计？</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第12章 泰勒斯的甜葡萄</h4>
          <span class="af-ch-num">核心章</span>
        </summary>
        <div class="af-core-idea">可选择性：有限风险 + 无限收益的选择权</div>
        <div class="af-details">
          <strong>泰勒斯的期权</strong>：古代哲学家通过购买压榨机的期权（而非机器本身），以有限成本获得无限收益——这是可选择性最古老的案例。<br>
          <strong>可选择性的本质</strong>：不需要知道具体会发生什么，只需拥有选择权——在任何可能性中都能获益。<br>
          <strong>亚里士多德的盲点</strong>：他将泰勒斯的成功归结为天文知识，而忽略了可选择性的逻辑——这个概念混淆持续了两千年。<br><br>
          在什么条件下自由探索优于设计？——当不确定性极高、试错成本有限时。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>可选择性是反脆弱性的操作化形式。它允许你"不知道"——恰恰因为你不需要预测。拥有选择权意味着你对未来的任何走向都有有利位置。这与传统"先规划后执行"的思维完全相反——不是消除不确定性，而是在不确定性中保持有利的选择权。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第13章 教鸟儿如何飞行</h4>
          <span class="af-ch-num">批判章</span>
        </summary>
        <div class="af-core-idea">苏联-哈佛派谬见：自上而下的设计无法创造真正的创新</div>
        <div class="af-details">
          <strong>苏联-哈佛谬见</strong>：认为可以通过规划、研究和教育来"生产"创新——就像教鸟儿如何飞行。<br>
          <strong>副现象</strong>：学术研究看起来推动了创新，实际上创新来自实践者的试错，学术研究只是事后标注了路径。<br>
          <strong>增长背后的不对称回报</strong>：真正的增长来自无数失败的探索中极少数成功者的超额回报。<br><br>
          哈佛商学院等机构陷入了苏联式思维误区——认为可以通过教授来培养企业家。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第14章 当两件事不是"同一回事"时</h4>
          <span class="af-ch-num">认识论章</span>
        </summary>
        <div class="af-core-idea">绿色木材谬误："知道为什么" &#x2260; "知道怎么做"</div>
        <div class="af-details">
          <strong>绿色木材谬误</strong>：木材商并不知道木材为什么是绿色的，他只需要知道如何做木材生意。<br>
          <strong>理论与实践的鸿沟</strong>：成功往往不需要理解底层理论——实践者的智慧来自经验，而非理论理解。<br>
          <strong>试错 vs 理论设计</strong>：试错允许失败、从错误中学习、适应性强；理论设计完美但脆弱、无法适应变化。<br><br>
          知识是否能创造财富？如果是，那么是哪些知识？——"知道怎么做"的知识远比"知道为什么"的知识更有价值。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第15章 失败者撰写的历史</h4>
          <span class="af-ch-num">历史章</span>
        </summary>
        <div class="af-core-idea">技术发展史是事后合理化的，不是真实路径</div>
        <div class="af-details">
          <strong>幸存者偏差</strong>：我们只看到成功的技术，无数失败的尝试被遗忘。<br>
          <strong>历史被改写</strong>：历史书上的技术路径是事后构建的线性叙事，真实过程充满偶然和混乱。<br>
          <strong>副现象的扩散</strong>：学术研究看似推动了技术进步，实际是技术进步后的理论包装。<br><br>
          生物学知识是否伤害了医疗技术发展？——对理论的过度信任可能阻碍试错驱动的实践进步。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第16章 混乱中的秩序</h4>
          <span class="af-ch-num">教育章</span>
        </summary>
        <div class="af-core-idea">漫游者的教育优于观光客的教育</div>
        <div class="af-details">
          <strong>漫游者</strong>：通过自由探索和试错获得知识，路径不可预测但充满发现。<br>
          <strong>观光客</strong>：按计划行动，看似高效实则错过了所有意外之喜。<br>
          <strong>足球妈妈的危害</strong>：过度安排孩子的时间，剥夺了自由探索和无聊（创造力的温床）。<br><br>
          偏爱秩序的教育与偏爱无序的创新之间存在根本矛盾——教育系统站在了错误的一边。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第17章 胖子托尼与苏格拉底辩论</h4>
          <span class="af-ch-num">哲学高潮章</span>
        </summary>
        <div class="af-core-idea">酒神式思维 vs 日神式思维——实践智慧胜过理论理性</div>
        <div class="af-details">
          <strong>苏格拉底的错误</strong>：要求一切行为都能被逻辑解释——但"我们不能做我们无法解释的事"是荒谬的。<br>
          <strong>酒神式思维（狄奥尼索斯）</strong>：拥抱混乱、直觉、实践经验、生命力。<br>
          <strong>日神式思维（阿波罗）</strong>：追求理性、逻辑、理论、秩序、抽象。<br>
          <strong>胖子托尼的胜利</strong>：实用主义智慧最终胜过空洞的理论辩论。<br><br>
          尼采的洞见：现代文化越来越倾向于选择无视酒神式的事物——而这恰恰是反脆弱性的源泉。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>整部书的思想在此达到高潮。苏格拉底式的"理性暴政"要求一切都能被解释——但这等于是给反脆弱性判了死刑。实践智慧（胖子托尼）不需要理论辩护就能行动，而理论理性（苏格拉底）却无法行动因为它需要先解释一切。在一个本质上不透明的世界里，等待解释再行动=永远的脆弱。
        </div>
      </details>
    </div>
  </details>

  <!-- 第五卷 -->
  <details class="af-volume af-v5">
    <summary>
      <div class="af-volume-num">V</div>
      <div class="af-volume-title">
        <h3>非线性与非线性</h3>
        <div class="af-vol-insight">核心命题：反脆弱性的数学本质是什么？如何识别脆弱？</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第18章 一块大石头与一千颗小石子的区别</h4>
          <span class="af-ch-num">数学章</span>
        </summary>
        <div class="af-core-idea">凸性=反脆弱性，凹性=脆弱性</div>
        <div class="af-details">
          <strong>凸性效应</strong>：小冲击损失有限，大冲击收益无限——这是反脆弱性的数学表述。<br>
          <strong>凹性效应</strong>：小冲击收益有限，大冲击损失无限——这是脆弱性的数学表述。<br>
          <strong>一块大石头 vs 一千颗小石子</strong>：集中=脆弱，分散=反脆弱。<br>
          <strong>规模带来脆弱性</strong>：大型组织、项目往往具有凹性特征。<br>
          <strong>非线性现实</strong>：9万辆车+11万辆车&#x2260;两个10万辆车（交通拥堵）。<br><br>
          交通、项目成本超支、金融危机——都是非线性凹性效应的体现。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>反脆弱性可以用凸性来精确定义：f(x+&#x394;) + f(x-&#x394;) &gt; 2f(x)。这意味着波动本身就能带来净收益。脆弱性则相反：波动带来净损失。这不是比喻，而是数学——凸性偏见和詹森不等式证明了在不确定环境下，凸性函数的期望值高于期望值处的函数值。波动性本身就成了收益来源。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第19章 炼金石与反炼金石</h4>
          <span class="af-ch-num">方法章</span>
        </summary>
        <div class="af-core-idea">炼金石：将脆弱系统转化为反脆弱系统的方法</div>
        <div class="af-details">
          <strong>炼金石</strong>：通过理解和利用非线性关系，将脆弱转化为反脆弱——就像将铅变成黄金。<br>
          <strong>反炼金石</strong>：将反脆弱系统误操作为脆弱——房利美的破产案例。<br>
          <strong>詹森不等式</strong>：凸性函数中，E[f(x)] &#x2265; f(E[x])——不确定性的期望收益超过确定性的期望。<br>
          <strong>识别脆弱性的启发法</strong>：<br>
          &#x00B7; 凸性偏见测试：事物是否从波动中获益？<br>
          &#x00B7; 不对称性测试：潜在收益是否大于潜在损失？<br>
          &#x00B7; 可观察性原则：脆弱性可衡量，风险不可衡量。<br><br>
          人类直觉倾向于低估非线性效应——这是决策错误的深层根源。
        </div>
      </details>
    </div>
  </details>

  <!-- 第六卷 -->
  <details class="af-volume af-v6">
    <summary>
      <div class="af-volume-num">VI</div>
      <div class="af-volume-title">
        <h3>否定法</h3>
        <div class="af-vol-insight">核心命题：减法优于加法，古老优于新奇</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第20章 时间与脆弱性</h4>
          <span class="af-ch-num">时间章</span>
        </summary>
        <div class="af-core-idea">林迪效应：存在越久的事物，未来预期寿命越长</div>
        <div class="af-details">
          <strong>林迪效应</strong>：旧事物的预期剩余寿命与其已存活时间成正比。一本存活了100年的书，预计还能再存活100年。<br>
          <strong>新事物狂热症</strong>：过度迷恋新技术、新方法——新事物未经过时间检验，存在未知风险。<br>
          <strong>否定法</strong>：通过去除错误（减法）来进步，而非增加正确答案（加法）。<br>
          <strong>时间作为过滤器</strong>：时间是最好的风险测试器——淘汰脆弱事物，留下反脆弱事物。<br><br>
          骆驼取代轮子、传统医学的持续应用——古老的方法往往更可靠。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>否定法是全书最深刻的哲学立场：知道什么是错的比知道什么是对的更容易、更可靠。减法优于加法——去除有害的比添加有益的更有效。这不仅是方法论，更是一种认识论谦逊：我们无法确定什么是好的，但可以确定什么是坏的。消除坏的东西，好的自然会浮现。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第21章 医疗、凸性和不透明</h4>
          <span class="af-ch-num">应用章</span>
        </summary>
        <div class="af-core-idea">病重者有凸性回报（值得冒险），健康者有凹性风险（不值得干预）</div>
        <div class="af-details">
          <strong>病重者</strong>：干预的潜在收益巨大，潜在损失相对较小——值得冒险。<br>
          <strong>健康者</strong>：干预的潜在收益微不足道，潜在损失可能很大——不值得冒险。<br>
          <strong>医源性损伤</strong>：药物副作用、过度诊断、不必要手术——对健康人的干预是医源性损伤的重灾区。<br>
          <strong>不透明</strong>：信息不对称——副作用和并发症被低估，成功案例被放大。<br><br>
          医疗决策规则：基于风险/收益的不对称性分析，而非"一刀切"的干预标准。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第22章 活得长寿，但不要太长</h4>
          <span class="af-ch-num">生命章</span>
        </summary>
        <div class="af-core-idea">减法医疗：去除不健康因素，而非增加药物</div>
        <div class="af-details">
          <strong>减法医疗</strong>：减少加工食品、不必要药物、过度医疗——让身体自然恢复。<br>
          <strong>个体与环境的匹配</strong>：人类适应了随机性和压力源，过度保护削弱了适应性。<br>
          <strong>为什么不想永生</strong>：反脆弱性需要死亡——个体的死亡为群体进化提供空间。长寿&#x2260;生命质量。<br><br>
          自然的智慧（数百万年进化）vs 技术的局限（人为干预往往破坏自然平衡）。
        </div>
      </details>
    </div>
  </details>

  <!-- 第七卷 -->
  <details class="af-volume af-v7">
    <summary>
      <div class="af-volume-num">VII</div>
      <div class="af-volume-title">
        <h3>脆弱性与反脆弱性的伦理</h3>
        <div class="af-vol-insight">核心命题：以他人脆弱为代价的反脆弱性是不道德的</div>
      </div>
      <div class="af-volume-toggle">&#x25B6;</div>
    </summary>
    <div class="af-volume-content">

      <details class="af-chapter">
        <summary>
          <h4>第23章 切身利害</h4>
          <span class="af-ch-num">伦理核心章</span>
        </summary>
        <div class="af-core-idea">决策者必须承担决策后果——没有风险承担的决策是不道德的</div>
        <div class="af-details">
          <strong>代理问题</strong>：代理人获得收益，委托人承担风险——脆弱性转移。<br>
          <strong>切身利害（Skin in the Game）</strong>：决策者必须承担决策后果——这是反脆弱系统运行的伦理基础。<br>
          <strong>牺牲他人的可选择性</strong>：决策者拥有选择权，将负面结果转移给他人，保留正面结果给自己。<br>
          <strong>历史对比</strong>：古代工程师为失败付出生命代价；现代官员只享受权力不承担风险。<br><br>
          罗伯特·鲁宾问题、斯蒂格利茨问题、布林德问题——都关乎代理问题与过滤性选择。
        </div>
        <div class="af-insight-box">
          <span class="af-label">洞察：</span>"你不应该为了获得反脆弱性，而牺牲别人的脆弱"——这是全书最核心的伦理法则。现代社会的根本危机不是经济危机，而是风险承担与决策权的分离。银行家获奖金，纳税人承担损失；官员发号施令，百姓承担后果。这种伦理倒置使得整个系统失去了反脆弱性的进化机制——犯错的人不承担后果，就无法从错误中学习。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第24章 给职业戴上伦理光环</h4>
          <span class="af-ch-num">批判章</span>
        </summary>
        <div class="af-core-idea">职业光环成为伦理失败的遮羞布</div>
        <div class="af-details">
          <strong>伦理倒置</strong>：群体犯错误，个人可能知道真相但不敢说——职业规范和光环效应压制了异见。<br>
          <strong>职业 vs 技能</strong>：职业=规范、标准、保护、垄断；技能=能力、结果、风险承担、持续改进。<br>
          <strong>如何获得自由</strong>：打破光环、建立风险共担、开放竞争、历史检验。<br><br>
          医生沉默、经济学家集体失误、政治家维护糟糕政策——职业光环让人不敢质疑。
        </div>
      </details>

      <details class="af-chapter">
        <summary>
          <h4>第25章 结语</h4>
          <span class="af-ch-num">终章</span>
        </summary>
        <div class="af-core-idea">反脆弱性是复杂系统的关键属性，也是繁荣的秘诀</div>
        <div class="af-details">
          <strong>实践建议</strong>：<br>
          &#x00B7; 个人：采用杠铃策略，暴露于适量随机性，从错误中学习，拥有切身利害<br>
          &#x00B7; 社会：减少自上而下干预，鼓励自下而上创新，建立风险共担机制<br><br>
          <strong>哲学立场</strong>：<br>
          &#x00B7; 认识论谦逊：承认无知比假装理解更有价值<br>
          &#x00B7; 非线性思维：世界不是线性的，不要过度模型化<br>
          &#x00B7; 时间检验：古老方法往往比新方法更可靠<br>
          &#x00B7; 实践导向：行动比理论更重要<br><br>
          反脆弱性不是简单的"坚韧"，而是从冲击中变得更强。
        </div>
      </details>
    </div>
  </details>
</section>

<!-- ==================== 核心对偶结构 ==================== -->
<section class="af-philosophy">
  <h2>思想对偶：贯穿全书的二元张力</h2>

  <div class="af-philosophy-grid">
    <div class="af-philo-card">
      <h4>有机体 vs 机械体</h4>
      <div class="af-vs">
        <span class="af-left">猫：需要压力，从压力中进化</span>
        <span class="af-mid">vs</span>
        <span class="af-right">洗衣机：压力即损耗，最终报废</span>
      </div>
      <p>将有机体当作机械体管理是现代性的根本错误——医疗、教育、企业管理都犯了这个错误。有机体的反脆弱性来自内在修复和超越机制，而机械体只能损耗和衰退。</p>
    </div>

    <div class="af-philo-card">
      <h4>自下而上 vs 自上而下</h4>
      <div class="af-vs">
        <span class="af-left">集权设计：蓝图、规划、控制</span>
        <span class="af-mid">vs</span>
        <span class="af-right">自由演化：试错、探索、涌现</span>
      </div>
      <p>瑞士（无中央政府）vs 列宁式的集权蓝图。硅谷（快速失败）vs 纽约银行体系（系统性崩溃）。创新从来不是被设计出来的，而是从无数失败中涌现的。</p>
    </div>

    <div class="af-philo-card">
      <h4>酒神 vs 日神</h4>
      <div class="af-vs">
        <span class="af-left">苏格拉底：解释一切才能行动</span>
        <span class="af-mid">vs</span>
        <span class="af-right">胖子托尼：无需解释就能获益</span>
      </div>
      <p>尼采的酒神式思维拥抱混乱、直觉和实践——这是反脆弱性的认识论基础。日神式思维追求逻辑和解释，但等待解释再行动等于永远的脆弱。真正的智慧是知道什么时候不需要解释。</p>
    </div>

    <div class="af-philo-card">
      <h4>加法 vs 减法（否定法）</h4>
      <div class="af-vs">
        <span class="af-left">添加：更多药物、更多规则、更多干预</span>
        <span class="af-mid">vs</span>
        <span class="af-right">去除：减少有害因素，让好的自然浮现</span>
      </div>
      <p>知道什么是错的比知道什么是对的更容易、更可靠。减法医疗（减少药物）优于加法医疗（增加药物）。否定法不仅是方法论，更是认识论谦逊——我们无法确定什么是好的，但可以确定什么是坏的。</p>
    </div>

    <div class="af-philo-card">
      <h4>凸性 vs 凹性</h4>
      <div class="af-vs">
        <span class="af-left">凹性：大冲击=无限损失（脆弱）</span>
        <span class="af-mid">vs</span>
        <span class="af-right">凸性：大冲击=无限收益（反脆弱）</span>
      </div>
      <p>凸性是反脆弱性的数学本质：f(x+&#x394;)+f(x-&#x394;)&gt;2f(x)，波动本身带来净收益。詹森不等式证明在不确定环境下，凸性函数的期望值高于期望处的函数值。波动性=收益来源。</p>
    </div>

    <div class="af-philo-card">
      <h4>切身利害 vs 代理问题</h4>
      <div class="af-vs">
        <span class="af-left">代理者：收益私有，风险转嫁</span>
        <span class="af-mid">vs</span>
        <span class="af-right">切身利害：权力与风险匹配</span>
      </div>
      <p>现代社会的根本危机：决策权与风险承担分离。银行家获奖金纳税人承担损失——这不仅是经济问题，更是伦理问题。"你不应该为了获得反脆弱性，而牺牲别人的脆弱。"</p>
    </div>
  </div>
</section>

<!-- ==================== 行动原则 ==================== -->
<section class="af-principles">
  <h2>从思想到行动：反脆弱性实践法则</h2>

  <div class="af-principle-item">
    <div class="af-principle-num">1</div>
    <div>
      <h4>杠铃策略</h4>
      <p>在90%的领域极度保守（确保生存底线），在10%的领域极度冒险（追逐无限收益）。永远不要停留在"中庸"的中间地带——中间地带既不安全也无超额收益。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">2</div>
    <div>
      <h4>保留可选择性</h4>
      <p>不要把自己锁定在单一路径中。拥有选择权意味着在任何未来场景中都有有利位置。你不需要预测未来，只需要确保自己有选择。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">3</div>
    <div>
      <h4>拥抱微小错误</h4>
      <p>让错误小到可逆、频繁到能学习。避免"一个大错"——那会毁灭你。微小错误的累积是进化的燃料，正如餐馆倒闭成就了餐饮业的活力。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">4</div>
    <div>
      <h4>用否定法做减法</h4>
      <p>不要问"我应该添加什么"，而是问"我应该去除什么"。减少加工食品、减少不必要的药物、减少无意义的干预。减法永远比加法更可靠。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">5</div>
    <div>
      <h4>尊重时间检验</h4>
      <p>林迪效应告诉我们：存在越久的事物越可能继续存在。在技术、方法、制度的选择上，偏好经过时间考验的旧事物，而非未经验证的新事物。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">6</div>
    <div>
      <h4>确保切身利害</h4>
      <p>决策者必须承担决策后果。如果你不会为失败买单，你就不应该拥有决策权。这是反脆弱系统的伦理底线——也是防止系统级崩溃的最后一道防线。</p>
    </div>
  </div>

  <div class="af-principle-item">
    <div class="af-principle-num">7</div>
    <div>
      <h4>识别脆弱性而非预测风险</h4>
      <p>不要试图预测黑天鹅何时到来，而要识别哪些系统在黑天鹅来临时会崩溃。脆弱性可以衡量，风险不可衡量。确保你的房子不是纸做的——这比预测暴风雨何时来重要得多。</p>
    </div>
  </div>
</section>

<!-- ==================== FOOTER ==================== -->
<section class="af-footer">
  <div class="af-final-quote">"当你寻求秩序，你得到的不过是表面的秩序；<br>而当你拥抱随机性，你却能把握秩序、掌控局面。"</div>
  <div>《反脆弱：从无序中受益》— 纳西姆·尼古拉斯·塔勒布</div>
  <div style="margin-top:8px; font-size:0.8rem;">思维导图基于原书内容深度提炼 · 七卷完整思想脉络</div>
</section>


<!-- Part B: 交互式树状脑图 -->
<h2 style="text-align:center;margin:60px 0 20px;font-family:Georgia,serif;color:#2D3748;">交互式树状脑图</h2>
<p style="text-align:center;color:#718096;margin-bottom:20px;">点击节点展开/折叠 · 滚轮缩放 · 拖拽平移 · 悬停查看详情</p>
<style>
  .af-tree-container {
    font-family: 'Microsoft YaHei', 'PingFang SC', sans-serif;
    color: #4A5568;
  }

  #af-tree-toolbar {
    position: absolute;
    top: 16px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 100;
    display: flex;
    gap: 8px;
    align-items: center;
    background: rgba(255,255,255,0.95);
    border: 1px solid #E8E4DE;
    border-radius: 12px;
    padding: 8px 16px;
    backdrop-filter: blur(10px);
  }

  #af-tree-toolbar button {
    background: rgba(0,0,0,0.04);
    border: 1px solid #E8E4DE;
    color: #718096;
    padding: 6px 14px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 13px;
    font-family: inherit;
    transition: all 0.2s;
  }

  #af-tree-toolbar button:hover {
    background: rgba(0,0,0,0.08);
    color: #4A5568;
  }

  #af-tree-toolbar .sep {
    width: 1px;
    height: 20px;
    background: #E8E4DE;
    margin: 0 4px;
  }

  #af-tree-toolbar .zoom-info {
    font-size: 12px;
    color: #718096;
    min-width: 40px;
    text-align: center;
  }

  #af-tree-search-box {
    background: rgba(0,0,0,0.04);
    border: 1px solid #E8E4DE;
    color: #4A5568;
    padding: 6px 12px;
    border-radius: 8px;
    font-size: 13px;
    font-family: inherit;
    width: 160px;
    outline: none;
  }

  #af-tree-search-box::placeholder { color: #A0AEC0; }
  #af-tree-search-box:focus { border-color: #E8A45C; }

  #af-tree-svg {
    width: 100%;
    height: 100%;
    cursor: grab;
  }

  #af-tree-svg:active { cursor: grabbing; }

  .af-tree-link {
    fill: none;
    stroke: #D4CFC6;
    stroke-width: 1.5;
    opacity: 0.6;
    transition: stroke 0.3s, opacity 0.3s;
  }

  .af-tree-link.af-tree-highlight {
    stroke: #E8A45C;
    stroke-width: 2.5;
    opacity: 1;
  }

  .af-tree-node circle {
    stroke-width: 2.5;
    cursor: pointer;
    transition: r 0.3s, fill 0.3s, stroke 0.3s;
  }

  .af-tree-node:hover circle {
    filter: brightness(0.95);
  }

  .af-tree-node text {
    font-size: 12px;
    fill: #4A5568;
    pointer-events: none;
    text-shadow: 0 1px 4px rgba(0,0,0,0.1);
  }

  .af-tree-node text.af-tree-highlight {
    fill: #E8A45C;
    font-weight: 700;
  }

  /* Depth styles */
  .af-tree-node.af-tree-depth-0 circle { fill: #F5F2ED; stroke: #E8A45C; r: 18; }
  .af-tree-node.af-tree-depth-0 text { font-size: 16px; font-weight: 700; fill: #E8A45C; }

  .af-tree-node.af-tree-depth-1 circle { fill: #F5F2ED; stroke: #5A9A8A; r: 12; }
  .af-tree-node.af-tree-depth-1 text { font-size: 13px; font-weight: 600; fill: #5A9A8A; }

  .af-tree-node.af-tree-depth-2 circle { fill: #F5F2ED; r: 7; }
  .af-tree-node.af-tree-depth-2 text { font-size: 11px; fill: #718096; }

  .af-tree-node.af-tree-depth-3 circle { fill: #F5F2ED; r: 5; }
  .af-tree-node.af-tree-depth-3 text { font-size: 10px; fill: #A0AEC0; }

  /* Color per volume */
  .af-tree-node[data-v="1"] circle { stroke: #c0392b; }
  .af-tree-node[data-v="1"] text { fill: #c0392b; }
  .af-tree-node[data-v="2"] circle { stroke: #E8A45C; }
  .af-tree-node[data-v="2"] text { fill: #D4893A; }
  .af-tree-node[data-v="3"] circle { stroke: #8e44ad; }
  .af-tree-node[data-v="3"] text { fill: #a78bfa; }
  .af-tree-node[data-v="4"] circle { stroke: #2980b9; }
  .af-tree-node[data-v="4"] text { fill: #60a5fa; }
  .af-tree-node[data-v="5"] circle { stroke: #16a085; }
  .af-tree-node[data-v="5"] text { fill: #34d399; }
  .af-tree-node[data-v="6"] circle { stroke: #7CB9A8; }
  .af-tree-node[data-v="6"] text { fill: #5A9A8A; }
  .af-tree-node[data-v="7"] circle { stroke: #f39c12; }
  .af-tree-node[data-v="7"] text { fill: #fbbf24; }

  .af-tree-node[data-v="core"] circle { stroke: #E8A45C; }
  .af-tree-node[data-v="core"] text { fill: #D4893A; }
  .af-tree-node[data-v="dual"] circle { stroke: #ec4899; }
  .af-tree-node[data-v="dual"] text { fill: #f472b6; }
  .af-tree-node[data-v="act"] circle { stroke: #06b6d4; }
  .af-tree-node[data-v="act"] text { fill: #22d3ee; }

  .af-tree-tooltip {
    position: absolute;
    background: rgba(255,255,255,0.98);
    border: 1px solid #E8A45C;
    border-radius: 10px;
    padding: 14px 18px;
    max-width: 340px;
    font-size: 13px;
    line-height: 1.7;
    color: #4A5568;
    pointer-events: none;
    opacity: 0;
    transition: opacity 0.2s;
    z-index: 200;
    backdrop-filter: blur(8px);
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
  }

  .af-tree-tooltip.af-tree-show { opacity: 1; }

  .af-tree-tooltip .tt-title {
    font-weight: 700;
    font-size: 14px;
    margin-bottom: 6px;
    color: #E8A45C;
  }

  .af-tree-tooltip .tt-tag {
    display: inline-block;
    font-size: 11px;
    padding: 2px 8px;
    border-radius: 6px;
    background: rgba(232,164,92,0.15);
    color: #D4893A;
    margin-bottom: 6px;
  }

  .af-tree-tooltip .tt-body {
    color: #718096;
  }

  #af-tree-legend {
    position: absolute;
    bottom: 20px;
    right: 20px;
    background: rgba(255,255,255,0.95);
    border: 1px solid #E8E4DE;
    border-radius: 12px;
    padding: 14px 18px;
    font-size: 12px;
    backdrop-filter: blur(10px);
    z-index: 100;
  }

  #af-tree-legend h4 {
    font-size: 12px;
    color: #718096;
    margin-bottom: 8px;
    font-weight: 400;
  }

  .af-tree-legend-row {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 4px;
    color: #718096;
  }

  .af-tree-legend-dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    flex-shrink: 0;
  }
</style>

<div class="af-tree-container" style="position:relative;height:70vh;border:1px solid #E8E4DE;border-radius:12px;overflow:hidden;margin:40px 0;">

  <div id="af-tree-toolbar">
    <button onclick="afTreeZoomFit()" title="适配视图">适配</button>
    <button onclick="afTreeExpandAll()">全部展开</button>
    <button onclick="afTreeCollapseAll()">折叠</button>
    <div class="sep"></div>
    <button onclick="afTreeZoomBy(1.3)">+</button>
    <span class="zoom-info" id="af-tree-zoom-level">100%</span>
    <button onclick="afTreeZoomBy(0.77)">-</button>
    <div class="sep"></div>
    <input type="text" id="af-tree-search-box" placeholder="搜索节点..." oninput="afTreeSearchNode(this.value)">
  </div>

  <div class="af-tree-tooltip" id="af-tree-tooltip">
    <div class="tt-title"></div>
    <div class="tt-tag"></div>
    <div class="tt-body"></div>
  </div>

  <div id="af-tree-legend">
    <h4>卷次图例</h4>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#c0392b"></div>I 反脆弱性：介绍</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#E8A45C"></div>II 现代化与否定</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#8e44ad"></div>III 非预测性世界观</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#2980b9"></div>IV 可选择性与智慧</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#16a085"></div>V 非线性</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#7CB9A8"></div>VI 否定法</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#f39c12"></div>VII 伦理</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#ec4899"></div>核心对偶</div>
    <div class="af-tree-legend-row"><div class="af-tree-legend-dot" style="background:#06b6d4"></div>实践法则</div>
  </div>

  <svg id="af-tree-svg"></svg>

</div>

<script src="https://d3js.org/d3.v7.min.js"></script>
<script>
(function() {
  const treeData = {
    name: "反脆弱",
    tag: "核心理念",
    tip: "风会熄灭蜡烛，却能使火越烧越旺。你要成为火，渴望得到风的吹拂。",
    vol: "core",
    children: [
      {
        name: "三元结构",
        tag: "第一卷 · 概念",
        vol: "1",
        tip: "脆弱-强韧-反脆弱，对应达摩克利斯之剑-凤凰-九头蛇怪",
        children: [
          { name: "脆弱", vol: "1", tip: "达摩克利斯之剑：厌恶波动，负面黑天鹅，优化即脆弱", children: [
            { name: "效率=无冗余", vol: "1", tip: "效率导向消除冗余，而冗余是反脆弱的基础" },
            { name: "错误不可逆", vol: "1", tip: "脆弱系统面对错误时崩溃，无法恢复" },
            { name: "集权·大规模", vol: "1", tip: "集中化、单一模式、自上而下的控制" }
          ]},
          { name: "强韧", vol: "1", tip: "凤凰：抵抗冲击，恢复原状，但不会变得更好", children: [
            { name: "冗余缓冲", vol: "1", tip: "有缓冲但无成长，只是原地恢复" },
            { name: "经验主义", vol: "1", tip: "习惯法、启发法、城邦制、分权" }
          ]},
          { name: "反脆弱", vol: "1", tip: "九头蛇怪：从伤害中成长，砍掉一个头长出两个", children: [
            { name: "毒物兴奋效应", vol: "1", tip: "小剂量有害物质反而有益，过度补偿机制" },
            { name: "创伤后成长", vol: "1", tip: "超越复原，从创伤中变得更强" },
            { name: "自由探索·试错", vol: "1", tip: "自下而上、杠铃策略、可选择性、凸性效应" }
          ]},
          { name: "领域依赖性", vol: "1", tip: "人们在医疗中理解毒物兴奋效应，却无法迁移到经济领域" }
        ]
      },
      {
        name: "有机体vs机械体",
        tag: "第一卷 · 本体论",
        vol: "1",
        tip: "猫需要压力源变得更强，洗衣机在压力下只会损耗",
        children: [
          { name: "猫·有机体", vol: "1", tip: "自我修复、从压力中进化、沃尔夫定律(骨密度↑)", children: [
            { name: "急性压力+恢复", vol: "1", tip: "有益：面对毒蛇后的应激反应" },
            { name: "毒物兴奋效应", vol: "1", tip: "小剂量毒物触发过度补偿" }
          ]},
          { name: "洗衣机·机械体", vol: "1", tip: "损耗、破败、无法自我修复", children: [
            { name: "慢性低压", vol: "1", tip: "有害：房贷、邮件、通勤——磨损而非强化" }
          ]},
          { name: "观光化", vol: "1", tip: "将不确定性从生活中清除=给有机体施加机械体逻辑" },
          { name: "衰老=功能失调", vol: "1", tip: "不是自然老化，而是与环境随机性的错配" }
        ]
      },
      {
        name: "个体脆弱→集体反脆弱",
        tag: "第一卷 · 层级",
        vol: "1",
        tip: "餐馆倒闭成就餐饮业活力，个体死亡促进基因进化",
        children: [
          { name: "餐馆集群效应", vol: "1", tip: "个别餐馆脆弱易倒闭，但行业整体具反脆弱性" },
          { name: "死亡是进化必要条件", vol: "1", tip: "不死的有机体需完美预测未来(不可能)，有限生命只需模糊方向" },
          { name: "抗生素耐药性", vol: "1", tip: "越努力杀灭细菌，幸存细菌越顽强" },
          { name: "向冒险者致敬", vol: "1", tip: "创业者的失败为集体提供反脆弱性" }
        ]
      },
      {
        name: "现代化否定反脆弱",
        tag: "第二卷",
        vol: "2",
        tip: "现代性系统性否定反脆弱性：消除随机性、集权控制、天真的干预",
        children: [
          { name: "稳定即脆弱", vol: "2", tip: "约翰(银行)vs乔治(出租车)：表面稳定实则隐性风险巨大", children: [
            { name: "瑞士城邦制", vol: "2", tip: "无中央政府、自下而上，最具反脆弱性" },
            { name: "隐性风险vs显性风险", vol: "2", tip: "波动被压制≠风险被消除，而是转化为更致命的隐性风险" }
          ]},
          { name: "随机性是燃料", vol: "2", tip: "消除随机性=消除进化压力=积累脆弱性", children: [
            { name: "布里丹之驴", vol: "2", tip: "等距犹豫至死，一阵微风即可解救" },
            { name: "森林火灾", vol: "2", tip: "预防小火→积累易燃物→更大灾难" },
            { name: "随机共振", vol: "2", tip: "添加噪声让微弱信号被听见" },
            { name: "模拟退火", vol: "2", tip: "随机漫游后冷却找到更优结构" }
          ]},
          { name: "天真的干预", vol: "2", tip: "治疗比疾病更危险：医源性损伤", children: [
            { name: "扁桃体手术", vol: "2", tip: "325/389被建议手术，实际发病率仅2-4%" },
            { name: "华盛顿之死", vol: "2", tip: "放血5-9磅加速死亡" },
            { name: "塞梅尔维斯", vol: "2", tip: "发现医院死亡率高于家中分娩，被同行迫害" }
          ]},
          { name: "预测的谬误", vol: "2", tip: "脆弱性可衡量，风险不可衡量", children: [
            { name: "第四象限", vol: "2", tip: "黑天鹅领域：罕见而不可预测的高风险" },
            { name: "认识论转向", vol: "2", tip: "从预测未来→识别脆弱，确保房子不是纸做的" }
          ]}
        ]
      },
      {
        name: "非预测性世界观",
        tag: "第三卷",
        vol: "3",
        tip: "不预测未来，如何从不确定性中获益？",
        children: [
          { name: "胖子托尼", vol: "3", tip: "直觉嗅出脆弱，揩脆弱推手的油水——实践智慧", children: [
            { name: "脆弱推手", vol: "3", tip: "制造系统性脆弱，自己却远离风险——将未知误认为不存在" }
          ]},
          { name: "塞内加·不对称性", vol: "3", tip: "反脆弱核心：有利因素永远大于不利因素", children: [
            { name: "斯多葛学派", vol: "3", tip: "专注于可控事物，对不可控事件保持有利地位" },
            { name: "损失有限·收益无限", vol: "3", tip: "反脆弱的数学本质：不对称性" }
          ]},
          { name: "杠铃策略", vol: "3", tip: "90%极度保守+10%极度冒险，避开中间地带", children: [
            { name: "否定中庸", vol: "3", tip: "中间地带既不安全也无超额收益——最脆弱" },
            { name: "一端保底·一端无限", vol: "3", tip: "颠覆传统风险管理'分散到中间'的教条" },
            { name: "职业杠铃", vol: "3", tip: "稳定主业+高风险高回报副业" }
          ]}
        ]
      },
      {
        name: "可选择性·智慧",
        tag: "第四卷",
        vol: "4",
        tip: "创新从何而来？自由探索为何优于顶层设计？",
        children: [
          { name: "泰勒斯·可选择性", vol: "4", tip: "有限风险+无限收益的选择权，无需预测即可获益", children: [
            { name: "亚里士多德盲点", vol: "4", tip: "将成功归结为知识而非可选择性，概念混淆两千年" }
          ]},
          { name: "教鸟儿飞行", vol: "4", tip: "苏联-哈佛谬见：自上而下无法创造创新", children: [
            { name: "副现象", vol: "4", tip: "学术研究看似推动创新，实际是事后标注路径" },
            { name: "不对称回报", vol: "4", tip: "增长来自无数失败中极少数成功者的超额回报" }
          ]},
          { name: "绿色木材谬误", vol: "4", tip: "'知道为什么'≠'知道怎么做'", children: [
            { name: "实践>理论", vol: "4", tip: "木材商不需要知道木材为何绿色，只需知道如何做生意" }
          ]},
          { name: "失败者写历史", vol: "4", tip: "技术史是事后合理化的线性叙事，非真实路径" },
          { name: "漫游者教育", vol: "4", tip: "漫游者(自由探索)>观光客(按计划)——足球妈妈剥夺创造力温床" },
          { name: "酒神vs日神", vol: "4", tip: "苏格拉底式理性暴政 vs 胖子托尼式实践智慧", children: [
            { name: "等待解释=脆弱", vol: "4", tip: "在不透明世界里，等待解释再行动=永远脆弱" }
          ]}
        ]
      },
      {
        name: "非线性·凸性",
        tag: "第五卷",
        vol: "5",
        tip: "反脆弱性的数学本质：凸性效应",
        children: [
          { name: "凸性=反脆弱", vol: "5", tip: "f(x+Δ)+f(x-Δ)>2f(x)，波动带来净收益", children: [
            { name: "詹森不等式", vol: "5", tip: "E[f(x)]≥f(E[x])，不确定性的期望收益超过确定性的期望" }
          ]},
          { name: "凹性=脆弱", vol: "5", tip: "大冲击=无限损失，规模带来脆弱性" },
          { name: "大石头vs小石子", vol: "5", tip: "集中=脆弱，分散=反脆弱", children: [
            { name: "9万+11万≠2×10万", vol: "5", tip: "交通拥堵的非线性现实" }
          ]},
          { name: "炼金石", vol: "5", tip: "将脆弱系统转化为反脆弱的方法", children: [
            { name: "凸性偏见测试", vol: "5", tip: "事物是否从波动中获益？" },
            { name: "不对称性测试", vol: "5", tip: "潜在收益>潜在损失？" },
            { name: "可观察性原则", vol: "5", tip: "脆弱性可衡量，风险不可衡量" }
          ]}
        ]
      },
      {
        name: "否定法",
        tag: "第六卷",
        vol: "6",
        tip: "减法优于加法，古老优于新奇",
        children: [
          { name: "林迪效应", vol: "6", tip: "存在越久的事物，未来预期寿命越长", children: [
            { name: "100年寿命→再活100年", vol: "6", tip: "旧事物的预期剩余寿命与已存活时间成正比" }
          ]},
          { name: "新事物狂热症", vol: "6", tip: "未经过时间检验=未知风险" },
          { name: "减法>加法", vol: "6", tip: "知道什么是错的比知道什么对的更容易更可靠", children: [
            { name: "减法医疗", vol: "6", tip: "去除有害因素而非添加药物" },
            { name: "认识论谦逊", vol: "6", tip: "无法确定什么是好的，但可确定什么是坏的" }
          ]},
          { name: "医疗不对称性", vol: "6", tip: "病重者有凸性回报(值得冒险)，健康者有凹性风险(不值得干预)", children: [
            { name: "医源性损伤重灾区", vol: "6", tip: "对健康人的干预：潜在收益微不足道，潜在损失可能很大" }
          ]},
          { name: "长寿≠永生", vol: "6", tip: "反脆弱性需要死亡——个体死亡为群体进化提供空间" }
        ]
      },
      {
        name: "伦理·切身利害",
        tag: "第七卷",
        vol: "7",
        tip: "以他人脆弱为代价的反脆弱性是不道德的",
        children: [
          { name: "Skin in the Game", vol: "7", tip: "决策者必须承担决策后果——反脆弱系统的伦理基础", children: [
            { name: "古代工程师", vol: "7", tip: "为失败付出生命代价——权力与风险匹配" },
            { name: "现代代理问题", vol: "7", tip: "收益私有、风险转嫁——鲁宾问题、斯蒂格利茨问题" }
          ]},
          { name: "核心伦理法则", vol: "7", tip: "你不应该为了获得反脆弱性，而牺牲别人的脆弱" },
          { name: "职业光环", vol: "7", tip: "职业规范压制异见，成为伦理失败的遮羞布", children: [
            { name: "职业vs技能", vol: "7", tip: "职业=规范·保护·垄断；技能=能力·结果·风险承担" }
          ]},
          { name: "风险共担", vol: "7", tip: "犯错者不承担后果→无法从错误中学习→系统失去进化机制" }
        ]
      },
      {
        name: "核心对偶",
        tag: "思想张力",
        vol: "dual",
        tip: "贯穿全书的二元张力结构",
        children: [
          { name: "有机体vs机械体", vol: "dual", tip: "需要压力进化 vs 压力即损耗" },
          { name: "自下而上vs自上而下", vol: "dual", tip: "自由涌现 vs 集权设计" },
          { name: "酒神vs日神", vol: "dual", tip: "实践智慧 vs 理性暴政" },
          { name: "减法vs加法", vol: "dual", tip: "去除有害 vs 添加有益" },
          { name: "凸性vs凹性", vol: "dual", tip: "波动=收益 vs 波动=损失" },
          { name: "切身利害vs代理", vol: "dual", tip: "权力与风险匹配 vs 收益私有风险转嫁" }
        ]
      },
      {
        name: "实践法则",
        tag: "行动指南",
        vol: "act",
        tip: "从思想到行动：七条反脆弱实践法则",
        children: [
          { name: "1 杠铃策略", vol: "act", tip: "90%保守+10%冒险，永远不要停留在中庸" },
          { name: "2 保留可选择性", vol: "act", tip: "不锁定单一路径，确保自己有选择权" },
          { name: "3 拥抱微小错误", vol: "act", tip: "小到可逆、频繁到能学习，避免一个大错" },
          { name: "4 否定法做减法", vol: "act", tip: "问'应该去除什么'而非'应该添加什么'" },
          { name: "5 尊重时间检验", vol: "act", tip: "林迪效应：存在越久越可能继续存在" },
          { name: "6 确保切身利害", vol: "act", tip: "不为失败买单就不该拥有决策权" },
          { name: "7 识别脆弱而非预测风险", vol: "act", tip: "确保房子不是纸做的，比预测暴风雨更重要" }
        ]
      }
    ]
  };

  // =================== D3 Tree ===================
  const afContainer = document.querySelector('.af-tree-container');
  const width = afContainer.clientWidth;
  const height = afContainer.clientHeight;
  const svg = d3.select("#af-tree-svg");
  const g = svg.append("g");

  let currentTransform = d3.zoomIdentity;
  const zoom = d3.zoom()
    .scaleExtent([0.15, 4])
    .on("zoom", (event) => {
      currentTransform = event.transform;
      g.attr("transform", event.transform);
      document.getElementById("af-tree-zoom-level").textContent = Math.round(event.transform.k * 100) + "%";
    });

  svg.call(zoom);

  // Assign IDs and collapse initially
  let idCounter = 0;
  function assignIds(node, depth) {
    if (depth === undefined) depth = 0;
    node.id = idCounter++;
    node.depth = depth;
    if (node.children) {
      node._children = node.children;
      // Only expand first two levels initially
      if (depth >= 1) {
        node.children = null;
      } else {
        node.children.forEach(function(c) { assignIds(c, depth + 1); });
      }
    }
  }
  assignIds(treeData);

  // Re-assign for depth-1 children (they were already expanded)
  function reAssignDepth(node, depth) {
    if (depth === undefined) depth = 0;
    node.depth = depth;
    if (node.children) {
      node.children.forEach(function(c) { reAssignDepth(c, depth + 1); });
    }
    if (node._children) {
      node._children.forEach(function(c) { reAssignDepth(c, depth + 1); });
    }
  }

  const treeLayout = d3.tree().nodeSize([22, 220]);
  const diagonal = d3.linkHorizontal().x(function(d) { return d.y; }).y(function(d) { return d.x; });

  function update(source) {
    const root = d3.hierarchy(treeData);
    root.x0 = source.x0 || 0;
    root.y0 = source.y0 || 0;

    const treeNodes = treeLayout(root);
    const nodes = treeNodes.descendants();
    const links = treeNodes.links();

    // Normalize depths
    nodes.forEach(function(d) {
      d.y = d.depth * 260;
    });

    // ---- Links ----
    const link = g.selectAll("path.af-tree-link")
      .data(links, function(d) { return d.target.data.id; });

    const linkEnter = link.enter().append("path")
      .attr("class", "af-tree-link")
      .attr("d", function(d) {
        const o = { x: source.x0 || 0, y: source.y0 || 0 };
        return diagonal({ source: o, target: o });
      });

    linkEnter.merge(link)
      .transition().duration(400)
      .attr("d", diagonal);

    link.exit()
      .transition().duration(400)
      .attr("d", function(d) {
        const o = { x: source.x, y: source.y };
        return diagonal({ source: o, target: o });
      })
      .remove();

    // ---- Nodes ----
    const node = g.selectAll("g.af-tree-node")
      .data(nodes, function(d) { return d.data.id; });

    const nodeEnter = node.enter().append("g")
      .attr("class", function(d) { return "af-tree-node af-tree-depth-" + d.depth; })
      .attr("data-v", function(d) { return d.data.vol || ""; })
      .attr("transform", "translate(" + (source.y0 || 0) + "," + (source.x0 || 0) + ")")
      .on("click", function(event, d) {
        event.stopPropagation();
        toggleNode(d);
      })
      .on("mouseenter", function(event, d) { showTooltip(event, d); })
      .on("mousemove", function(event) { moveTooltip(event); })
      .on("mouseleave", hideTooltip);

    // Circle
    nodeEnter.append("circle")
      .attr("r", 0);

    // Has-children indicator
    nodeEnter.append("text")
      .attr("class", "indicator")
      .attr("dy", "0.35em")
      .attr("text-anchor", "middle")
      .style("font-size", "9px")
      .style("fill", "#F5F2ED")
      .style("pointer-events", "none")
      .text(function(d) { return (d.data._children || d.data.children) ? (d.data._children ? "+" : "−") : ""; });

    // Label
    nodeEnter.append("text")
      .attr("dy", function(d) { return d.children || d._children ? "-1.2em" : "0.35em"; })
      .attr("x", function(d) { return (d.children || d._children) ? 0 : 12; })
      .attr("text-anchor", function(d) { return (d.children || d._children) ? "middle" : "start"; })
      .text(function(d) { return d.data.name; });

    // Merge
    const nodeUpdate = nodeEnter.merge(node);

    nodeUpdate.transition().duration(400)
      .attr("transform", function(d) { return "translate(" + d.y + "," + d.x + ")"; });

    nodeUpdate.select("circle")
      .transition().duration(400)
      .attr("r", function(d) {
        if (d.depth === 0) return 18;
        if (d.depth === 1) return 12;
        if (d.depth === 2) return 7;
        return 5;
      });

    nodeUpdate.select(".indicator")
      .text(function(d) { return (d.data._children || d.data.children) ? (d.data._children ? "+" : "−") : ""; })
      .style("font-size", function(d) {
        if (d.depth === 0) return "14px";
        if (d.depth === 1) return "11px";
        return "8px";
      });

    // Exit
    const nodeExit = node.exit()
      .transition().duration(400)
      .attr("transform", "translate(" + source.y + "," + source.x + ")")
      .remove();

    nodeExit.select("circle").attr("r", 0);

    // Save positions
    nodes.forEach(function(d) {
      d.data.x0 = d.x;
      d.data.y0 = d.y;
    });
  }

  function toggleNode(d) {
    if (d.data._children) {
      d.data.children = d.data._children;
      d.data.children.forEach(function(c) { assignIds(c, d.depth + 1); });
      d.data._children = null;
    } else if (d.data.children) {
      d.data._children = d.data.children;
      d.data.children = null;
    }
    update(d.data);
  }

  function expandNode(node) {
    if (node._children) {
      node.children = node._children;
      node.children.forEach(function(c) {
        c.depth = (node.depth || 0) + 1;
        assignIds(c, c.depth);
      });
      node._children = null;
    }
    if (node.children) {
      node.children.forEach(expandNode);
    }
  }

  function collapseNode(node) {
    if (node.children) {
      node.children.forEach(collapseNode);
      if (node.depth > 0) {
        node._children = node.children;
        node.children = null;
      }
    }
  }

  // Expose global functions for toolbar buttons
  window.afTreeExpandAll = function() {
    expandNode(treeData);
    update(treeData);
    setTimeout(afTreeZoomFit, 500);
  };

  window.afTreeCollapseAll = function() {
    if (treeData.children) {
      treeData.children.forEach(collapseNode);
    }
    update(treeData);
    setTimeout(afTreeZoomFit, 500);
  };

  window.afTreeZoomFit = function() {
    const bounds = g.node().getBBox();
    if (bounds.width === 0) return;
    const container = document.querySelector('.af-tree-container');
    const fullWidth = container.clientWidth;
    const fullHeight = container.clientHeight;
    const midX = bounds.x + bounds.width / 2;
    const midY = bounds.y + bounds.height / 2;
    const scale = 0.85 / Math.max(bounds.width / fullWidth, bounds.height / fullHeight);
    const translate = [fullWidth / 2 - scale * midX, fullHeight / 2 - scale * midY];
    svg.transition().duration(600).call(
      zoom.transform,
      d3.zoomIdentity.translate(translate[0], translate[1]).scale(scale)
    );
  };

  window.afTreeZoomBy = function(factor) {
    svg.transition().duration(300).call(zoom.scaleBy, factor);
  };

  // Tooltip
  const tooltip = document.getElementById("af-tree-tooltip");

  function showTooltip(event, d) {
    const data = d.data;
    if (!data.tip && !data.tag) return;
    tooltip.querySelector(".tt-title").textContent = data.name;
    tooltip.querySelector(".tt-tag").textContent = data.tag || "";
    tooltip.querySelector(".tt-body").textContent = data.tip || "";
    tooltip.classList.add("af-tree-show");
    moveTooltip(event);
  }

  function moveTooltip(event) {
    const container = document.querySelector('.af-tree-container');
    const containerRect = container.getBoundingClientRect();
    let x = event.clientX - containerRect.left + 16;
    let y = event.clientY - containerRect.top - 10;
    if (x + 340 > containerRect.width) x = event.clientX - containerRect.left - 356;
    if (y + 150 > containerRect.height) y = containerRect.height - 160;
    if (x < 0) x = 4;
    if (y < 0) y = 4;
    tooltip.style.left = x + "px";
    tooltip.style.top = y + "px";
  }

  function hideTooltip() {
    tooltip.classList.remove("af-tree-show");
  }

  // Search
  window.afTreeSearchNode = function(query) {
    const q = query.trim().toLowerCase();
    g.selectAll("g.af-tree-node text:not(.indicator)").classed("af-tree-highlight", false);
    g.selectAll("path.af-tree-link").classed("af-tree-highlight", false);

    if (!q) return;

    const searchRoot = d3.hierarchy(treeData);
    treeLayout(searchRoot);
    const allNodes = searchRoot.descendants();
    const matched = allNodes.filter(function(d) { return d.data.name.toLowerCase().includes(q) || (d.data.tip && d.data.tip.toLowerCase().includes(q)); });

    if (matched.length === 0) return;

    // Highlight matched nodes
    const matchedIds = new Set(matched.map(function(d) { return d.data.id; }));
    g.selectAll("g.af-tree-node").each(function(d) {
      if (matchedIds.has(d.data.id)) {
        d3.select(this).select("text:not(.indicator)").classed("af-tree-highlight", true);
      }
    });

    // Pan to first match
    const first = matched[0];
    if (first) {
      const targetX = first.y;
      const targetY = first.x;
      const container = document.querySelector('.af-tree-container');
      const cw = container.clientWidth;
      const ch = container.clientHeight;
      svg.transition().duration(500).call(
        zoom.transform,
        d3.zoomIdentity
          .translate(cw / 2 - 0.8 * targetX, ch / 2 - 0.8 * targetY)
          .scale(0.8)
      );
    }
  };

  // Initial render
  update(treeData);
  setTimeout(afTreeZoomFit, 600);

  // Resize handler - use container dimensions
  window.addEventListener("resize", function() {
    afTreeZoomFit();
  });
})();
</script>
