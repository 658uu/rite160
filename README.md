<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>复活祭 · Resurrect Rite</title>
    <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Crimson+Text:ital,wght@0,400;0,600;1,400&display=swap');
        :root{--blood:#dc143c;--void:#000}body{margin:0;height:100vh;background:var(--void);color:var(--blood);font-family:'Crimson Text',serif;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;overflow:hidden;letter-spacing:.08em;}
        h1{font-size:2.2rem;font-weight:600;text-shadow:0 0 10px var(--blood);}
        #clock{font-size:4.5rem;font-weight:400;margin:.5em 0;text-shadow:0 0 15px var(--blood);}
        #sub{margin-top:1rem;font-size:1.1rem;opacity:.8}
        .pulse{animation:pulse 1.8s infinite;}
        @keyframes pulse{0%,100%{transform:scale(1);text-shadow:0 0 10px var(--blood)}50%{transform:scale(1.03);text-shadow:0 0 25px var(--blood)}}
    </style>
</head>
<body>
    <h1>复活祭 · Resurrect Rite</h1>
    <div id="clock" class="pulse">160:00:00</div>
    <div id="sub">请在倒计时结束前完成献祭，否则后果将转移至推荐人。</div>

    <script>
        (function(){
            const storeKey = 'riteDeadline';
            const duration = 160;                       // 小时
            let deadline = localStorage.getItem(storeKey);
            if(!deadline){
                deadline = new Date(Date.now() + duration * 3600 * 1000).toISOString();
                localStorage.setItem(storeKey,deadline);
            }
            const pad = n => n<10 ? '0'+n : n;
            function tick(){
                const rem = Math.max(0, new Date(deadline) - Date.now());
                const h = Math.floor(rem / 3600000);
                const m = Math.floor((rem % 3600000) / 60000);
                const s = Math.floor((rem % 60000) / 1000);
                document.getElementById('clock').textContent = `${pad(h)}:${pad(m)}:${pad(s)}`;
                if(rem === 0){
                    document.getElementById('sub').textContent = '时间到，请查看门口。';
                    document.body.style.background = 'var(--blood)';
                    document.body.style.color = 'var(--void)';
                    return;
                }
                requestAnimationFrame(tick);
            }
            tick();
        })();
    </script>
</body>
</html>
