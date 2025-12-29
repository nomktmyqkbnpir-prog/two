<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>浦华曜ONE - 学院分院仪式</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;500;700&family=Noto+Serif+SC:wght@400;700&display=swap');

        :root {
            --bg-deep: #050507;
            --glass-bg: rgba(255, 255, 255, 0.02);
            --glass-border: rgba(255, 255, 255, 0.08);
            --accent-purple: #7b2cbf;
            --accent-blue: #3a86ff;
            --accent-gold: #ff9e00;
            --text-main: #ffffff;
            --text-muted: #9ca3af;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; user-select: none; }

        body {
            background-color: var(--bg-deep);
            font-family: 'Inter', 'Noto Serif SC', sans-serif;
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden; /* 禁止页面滚动 */
            position: relative;
        }

        /* --- 背景氛围光斑 --- */
        .ambient-light {
            position: fixed;
            border-radius: 50%;
            filter: blur(80px);
            z-index: 0;
            opacity: 0.5;
            animation: float 10s infinite ease-in-out;
        }
        .orb-1 { top: -10%; left: -10%; width: 50vw; height: 50vw; background: radial-gradient(circle, var(--accent-purple), transparent); }
        .orb-2 { bottom: -20%; right: -10%; width: 60vw; height: 60vw; background: radial-gradient(circle, #240046, transparent); animation-delay: -5s; }
        .orb-3 { top: 30%; left: 30%; width: 40vw; height: 40vw; background: radial-gradient(circle, rgba(58, 134, 255, 0.15), transparent); animation-delay: -2s; }

        @keyframes float {
            0%, 100% { transform: translate(0, 0); }
            50% { transform: translate(20px, 30px); }
        }

        /* --- 鼠标跟随光效 --- */
        .cursor-spotlight {
            position: fixed;
            top: 0; left: 0;
            width: 800px; height: 800px;
            background: radial-gradient(circle, rgba(255,255,255,0.04) 0%, transparent 60%);
            transform: translate(-50%, -50%);
            pointer-events: none;
            z-index: 1;
            mix-blend-mode: screen;
        }

        /* --- 主容器 --- */
        .app-container {
            width: 100%;
            max-width: 600px; /* 缩小容器宽度，更紧凑 */
            padding: 15px;
            text-align: center;
            position: relative;
            z-index: 10;
        }

        /* --- 玻璃拟态卡片 --- */
        .glass-card {
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            border-top: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 24px;
            padding: 40px 30px; /* 减小内边距 */
            box-shadow: 0 20px 50px rgba(0,0,0,0.6), inset 0 0 30px rgba(255,255,255,0.02);
            backdrop-filter: blur(30px);
            -webkit-backdrop-filter: blur(30px);
            position: relative;
            
            /* 关键修复：允许内容（Logo）溢出卡片边界 */
            overflow: visible !important; 
            
            transition: all 0.5s ease;
        }

        /* --- 首页排版优化 --- */
        .title-group h1 {
            font-size: 1.8rem; /* 字体改小 */
            font-weight: 700;
            line-height: 1.4;
            background: linear-gradient(135deg, #fff 0%, #aaa 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 15px;
            letter-spacing: -0.5px;
        }
        
        .subtitle {
            font-size: 0.8rem;
            color: var(--text-muted);
            letter-spacing: 2px;
            margin-bottom: 30px;
            text-transform: uppercase;
            opacity: 0.6;
        }

        .btn-gradient {
            background: linear-gradient(90deg, #6247aa, #9d4edd);
            color: #fff;
            border: none;
            padding: 14px 50px; /* 按钮缩小 */
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 8px 15px rgba(123, 44, 191, 0.3);
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .btn-gradient:hover { transform: translateY(-2px); box-shadow: 0 12px 25px rgba(123, 44, 191, 0.5); }

        /* --- 选项卡片 (更紧凑) --- */
        .options-grid { display: grid; gap: 10px; margin-top: 25px; }
        .option-card {
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(255,255,255,0.05);
            padding: 15px 20px; /* 减小选项内边距 */
            border-radius: 12px;
            cursor: pointer;
            text-align: left;
            display: flex; align-items: center;
            transition: 0.2s;
            font-size: 0.9rem; /* 字体缩小 */
        }
        .option-card:hover { background: rgba(255,255,255,0.08); border-color: var(--accent-blue); transform: translateX(5px); }
        .option-dot { width: 8px; height: 8px; border-radius: 50%; background: #555; margin-right: 15px; }
        .option-card:hover .option-dot { background: var(--accent-blue); box-shadow: 0 0 8px var(--accent-blue); }

        /* --- 结果页 Logo 修复 (关键) --- */
        .logo-wrapper {
            /* 1. 缩小尺寸 */
            width: 140px; 
            height: 140px;
            
            /* 2. 悬浮位置调整 */
            margin: -90px auto 20px; 
            
            /* 3. 样式 */
            background: #ffffff;
            border-radius: 50%;
            padding: 15px; /* 这里的 padding 确保图片不贴边 */
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
            border: 3px solid rgba(255,255,255,0.1); 
            
            /* 4. 确保层级在卡片之上 */
            position: relative;
            z-index: 20; 
            
            animation: popIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .logo-img {
            width: 100%;
            height: 100%;
            object-fit: contain; /* 确保完整显示，不裁剪 */
            display: block;
        }

        @keyframes popIn {
            from { transform: scale(0) translateY(30px); opacity: 0; }
            to { transform: scale(1) translateY(0); opacity: 1; }
        }

        /* --- 结果页内容紧凑化 --- */
        #res-name { font-size: 1.6rem; margin-bottom: 5px; color: #fff; }
        #res-motto { font-size: 0.75rem; color: var(--accent-gold); margin-bottom: 20px; letter-spacing: 2px; }
        #res-desc { 
            font-size: 0.85rem; 
            line-height: 1.6; 
            color: #ccc; 
            margin-bottom: 25px; 
            height: 60px; /* 固定高度防止跳动 */
            overflow: hidden;
        }
        
        /* 数据条 */
        .stat-box { background: rgba(0,0,0,0.25); padding: 15px 20px; border-radius: 12px; }
        .stat-row { display: flex; align-items: center; margin-bottom: 8px; }
        .stat-label { width: 40px; font-size: 0.7rem; color: var(--text-muted); text-align: right; margin-right: 10px; }
        .stat-track { flex: 1; height: 4px; background: rgba(255,255,255,0.1); border-radius: 2px; }
        .stat-fill { height: 100%; background: linear-gradient(90deg, var(--accent-blue), var(--accent-purple)); width: 0%; border-radius: 2px; transition: width 1s ease; }
        
        .section { display: none; opacity: 0; transition: opacity 0.4s ease; }
        .section.active { display: block; opacity: 1; animation: fadeUp 0.6s ease forwards; }
        @keyframes fadeUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

    </style>
</head>
<body>

<!-- 背景元素 -->
<div class="ambient-light orb-1"></div>
<div class="ambient-light orb-2"></div>
<div class="ambient-light orb-3"></div>
<div class="cursor-spotlight"></div>

<div class="app-container">
    
    <!-- 1. 首页 -->
    <div id="start-screen" class="section active">
        <div class="glass-card">
            <div class="subtitle">PUHUAYAO ONE · SORTER</div>
            
            <div class="title-group">
                <h1>你的学习风格<br>和精神特质<br>属于浦华曜ONE<br>哪个学院</h1>
            </div>
            
            <div style="width: 30px; height: 2px; background: var(--accent-gold); margin: 20px auto;"></div>
            
            <p style="color: var(--text-muted); margin-bottom: 30px; font-size: 0.85rem;">
                AI 精神图谱分析 · 探索灵魂归属
            </p>
            
            <button class="btn-gradient" onclick="startQuiz()">开启测试</button>
        </div>
    </div>

    <!-- 2. 题目页 -->
    <div id="quiz-screen" class="section">
        <div class="glass-card">
            <div style="display: flex; justify-content: space-between; color: var(--text-muted); margin-bottom: 15px; font-size: 0.75rem;">
                <span>ANALYSIS</span>
                <span id="progress">01 / 05</span>
            </div>
            
            <div style="width: 100%; height: 2px; background: rgba(255,255,255,0.1); margin-bottom: 25px;">
                <div id="progress-bar" style="width: 20%; height: 100%; background: var(--text-main); transition: width 0.3s;"></div>
            </div>

            <h2 id="q-text" style="font-size: 1.1rem; margin-bottom: 25px; font-weight: 500; line-height: 1.5; min-height: 50px;"></h2>
            <div id="opts" class="options-grid"></div>
        </div>
    </div>

    <!-- 3. 加载页 -->
    <div id="loading-screen" class="section">
        <div class="glass-card" style="padding: 60px 30px;">
            <div style="width: 50px; height: 50px; border: 3px solid rgba(255,255,255,0.1); border-top: 3px solid var(--accent-blue); border-radius: 50%; margin: 0 auto 20px; animation: spin 0.8s linear infinite;"></div>
            <p id="loading-txt" style="color: var(--text-muted); font-size: 0.8rem;">NEURAL LINKING...</p>
        </div>
    </div>

    <!-- 4. 结果页 (布局紧凑化) -->
    <div id="result-screen" class="section">
        <div class="glass-card" style="padding-top: 10px; margin-top: 50px;">
            
            <!-- Logo 容器 (已修复裁剪问题) -->
            <div class="logo-wrapper">
                <img id="final-logo" src="" class="logo-img" alt="House Logo">
            </div>

            <h1 id="res-name">House Name</h1>
            <p id="res-motto">MOTTO</p>
            
            <p id="res-desc"><!-- 描述 --></p>

            <!-- 数据条 -->
            <div class="stat-box">
                <div class="stat-row"><span class="stat-label">理性</span><div class="stat-track"><div class="stat-fill" id="fill-logos"></div></div></div>
                <div class="stat-row"><span class="stat-label">弹性</span><div class="stat-track"><div class="stat-fill" id="fill-kelvin"></div></div></div>
                <div class="stat-row"><span class="stat-label">热情</span><div class="stat-track"><div class="stat-fill" id="fill-meraki"></div></div></div>
                <div class="stat-row"><span class="stat-label">希望</span><div class="stat-track"><div class="stat-fill" id="fill-elpis"></div></div></div>
                <div class="stat-row"><span class="stat-label">协作</span><div class="stat-track"><div class="stat-fill" id="fill-vela"></div></div></div>
                
                <div style="margin-top: 15px; font-size: 0.7rem; color: var(--text-muted); text-align: left; border-top: 1px solid rgba(255,255,255,0.1); padding-top: 10px;">
                    <span style="color: var(--accent-blue);">AI:</span> <span id="ai-text"></span>
                </div>
            </div>

            <button class="btn-gradient" onclick="location.reload()" style="margin-top: 25px; padding: 10px 40px; font-size: 0.9rem; background: #333;">重新测试</button>
        </div>
    </div>

</div>

<script>
    document.addEventListener('mousemove', (e) => {
        const spot = document.querySelector('.cursor-spotlight');
        spot.style.left = e.clientX + 'px';
        spot.style.top = e.clientY + 'px';
    });

    const houseImages = {
        logos: "https://i.postimg.cc/Z9Z0cWHw/wei-xin-tu-pian-2025-12-26-104735-522.png",
        kelvin: "https://i.postimg.cc/KKF4N1f9/wei-xin-tu-pian-2025-12-26-104800-082.png",
        meraki: "https://i.postimg.cc/qt0gLNwb/wei-xin-tu-pian-2025-12-26-104805-777.png",
        elpis: "https://i.postimg.cc/VS15RJgZ/wei-xin-tu-pian-2025-12-26-104811-110.png",
        vela: "https://i.postimg.cc/t1y75skM/wei-xin-tu-pian-2025-12-26-104818-023.png"
    };

    const houses = {
        logos: { name: "Logos House", motto: "思辨 · 理性 · 真理", desc: "你如深蓝大海般深邃，崇尚逻辑，在真理的殿堂中，你是最严谨的求索者。", ai: "逻辑回路活跃度98%，结构化思维呈晶体状稳定。" },
        kelvin: { name: "Kelvin-R House", motto: "自由 · 弹性 · 独立", desc: "你拥有极强的适应力与弹性，像自由穿梭的风，在压力下依然能保持独立的自我。", ai: "适应性指数S级，心理韧性极佳，反脆弱性强。" },
        meraki: { name: "Meraki House", motto: "灵魂 · 热情 · 积极", desc: "你是一团燃烧的火焰，将灵魂倾注于热爱。你的热情极具感染力，照亮自己也温暖他人。", ai: "情感核心能量溢出，具备极强的团队感染力。" },
        elpis: { name: "Elpis House", motto: "信念 · 探索 · 成长", desc: "你是无畏的探路者，不畏惧未知与挫折。在你眼中，万物皆有裂痕，那正是光照进来的地方。", ai: "成长型思维模式显著，风险偏好正向，探索欲极高。" },
        vela: { name: "Vela House", motto: "启航 · 协作 · 领航", desc: "你是天生的领航员，善于协作与指引。愿你如帆借风，带领伙伴驶向未知的广阔海域。", ai: "领导力特征激活，善于构建连接与统筹全局。" }
    };

    const questions = [
        { q: "面对一个从未见过的复杂难题，你的第一反应是？", opts: [
            { t: "查阅文献，分析底层逻辑", h: "logos" },
            { t: "先试错，万一成功了呢？", h: "elpis" },
            { t: "召集大家头脑风暴", h: "vela" },
            { t: "全身心投入这个有趣的挑战", h: "meraki" },
            { t: "灵活应对，换个角度思考", h: "kelvin" }
        ]},
        { q: "远航时，你背包里最重要的东西是？", opts: [
            { t: "记载智慧的书", h: "logos" },
            { t: "指引方向的罗盘", h: "vela" },
            { t: "一颗未知的种子", h: "elpis" },
            { t: "爱人的照片", h: "meraki" },
            { t: "万能工具箱", h: "kelvin" }
        ]},
        { q: "朋友心情低落，你会怎么安慰？", opts: [
            { t: "帮他理智分析现状", h: "logos" },
            { t: "带他去透透气", h: "kelvin" },
            { t: "用心倾听他的烦恼", h: "meraki" },
            { t: "鼓励他向前看", h: "elpis" },
            { t: "叫上朋友们一起陪他", h: "vela" }
        ]},
        { q: "你觉得你更像哪种自然现象？", opts: [
            { t: "深邃有序的星空", h: "logos" },
            { t: "自由穿梭的风", h: "kelvin" },
            { t: "温暖热烈的火", h: "meraki" },
            { t: "破土而出的芽", h: "elpis" },
            { t: "鼓风前行的帆", h: "vela" }
        ]},
        { q: "理想中的学习环境是？", opts: [
            { t: "充满思辨的图书馆", h: "logos" },
            { t: "无拘无束的空间", h: "kelvin" },
            { t: "激情澎湃的工作室", h: "meraki" },
            { t: "鼓励试错的实验室", h: "elpis" },
            { t: "齐心协力的圆桌", h: "vela" }
        ]}
    ];

    let curr = 0;
    let scores = { logos:0, kelvin:0, meraki:0, elpis:0, vela:0 };

    function startQuiz() {
        switchSection('start-screen', 'quiz-screen');
        renderQ();
    }

    function renderQ() {
        let q = questions[curr];
        document.getElementById('q-text').innerText = q.q;
        document.getElementById('progress').innerText = `0${curr+1} / 05`;
        document.getElementById('progress-bar').style.width = ((curr+1)/5)*100 + "%";
        
        let div = document.getElementById('opts');
        div.innerHTML = "";
        
        [...q.opts].sort(()=>Math.random()-0.5).forEach((o, index) => {
            let btn = document.createElement('div');
            btn.className = 'option-card';
            btn.style.animation = `fadeUp 0.4s ease forwards ${index * 0.1}s`;
            btn.style.opacity = '0';
            btn.innerHTML = `<div class="option-dot"></div><span>${o.t}</span>`;
            btn.onclick = () => {
                scores[o.h] += 10;
                Object.keys(scores).forEach(k => { if(k!==o.h) scores[k]+=Math.random()*2; });
                curr++;
                if(curr < 5) renderQ();
                else showLoad();
            }
            div.appendChild(btn);
        });
    }

    function showLoad() {
        switchSection('quiz-screen', 'loading-screen');
        let txts = ["构建思维模型...", "分析性格偏好...", "连接学院数据库..."];
        let i=0;
        let timer = setInterval(()=> document.getElementById('loading-txt').innerText=txts[i++%3], 800);
        setTimeout(() => { clearInterval(timer); showRes(); }, 2000);
    }

    function showRes() {
        switchSection('loading-screen', 'result-screen');

        let max = 0, house = "logos";
        for(let k in scores) { if(scores[k]>max){ max=scores[k]; house=k; } }
        let data = houses[house];
        
        document.getElementById('res-name').innerText = data.name;
        document.getElementById('res-motto').innerText = data.motto;
        document.getElementById('res-desc').innerText = data.desc;
        document.getElementById('ai-text').innerText = data.ai;
        document.getElementById('final-logo').src = houseImages[house];

        let maxVal = Math.max(...Object.values(scores));
        ['logos','kelvin','meraki','elpis','vela'].forEach(k => {
            let bar = document.getElementById('fill-'+k);
            let pct = (scores[k]/maxVal)*80 + 10;
            bar.style.width = pct + '%';
        });
    }

    function switchSection(from, to) {
        document.getElementById(from).classList.remove('active');
        setTimeout(() => {
            document.getElementById(to).classList.add('active');
        }, 400);
    }
</script>

<style>
@keyframes spin { 100% { transform: rotate(360deg); } }
</style>

</body>
</html>
