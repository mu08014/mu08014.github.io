---
layout: about
description: >
  지금까지 해온 일들
hide_description: true
redirect_from:
  - /download/
---

# Archives

<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        main { padding: 20px; }
        .timeline {
            position: relative;
            margin: 0 auto;
            padding: 40px 0;
            width: 100%;
            max-width: 800px;
        }
        .timeline::after {
            content: '';
            position: absolute;
            width: 3px;
            background-color: #333;
            top: 0;
            bottom: 0;
            left: 0;
            margin-left: -2px;
        }
        .timeline-entry {
            position: relative;
            width: 100%;
            padding: 20px 40px;
            box-sizing: border-box;
        }
        .timeline-entry.left {
            left: 0;
            padding-left: 60px;
        }
        .timeline-entry.right {
            left: 0;
            padding-left: 60px;
        }
        .timeline-entry::before {
            content: ' ';
            position: absolute;
            width: 25px;
            height: 25px;
            left: -12.5px;
            background-color: white;
            border: 4px solid #333;
            top: 30px;
            border-radius: 50%;
            z-index: 1;
        }
        .year {
            font-size: 1.5em;
            margin-bottom: 10px;
        }
        .month {
            font-size: 1.2em;
            margin-bottom: 10px;
            margin-top: 20px;
        }
        .project-list {
            list-style-type: none;
            padding: 0;
            margin: 15px;
        }
        .project-list li { margin-bottom: 10px; }
        .project-list a { text-decoration: none; color: #0066cc; }
        .project-list a:hover { text-decoration: underline; }
    </style>
</head>
<body>
    <main>
        <div class="timeline">
            <div class="timeline-entry left">
                <div class="year"><strong>2024</strong></div>
                <div class="month">June</div>
                <ul class="project-list">
                    <li>인공지능과게임프로그래밍 조별과제에서 ImageNet을 기반으로 사람의 손그림을 AI가 맞추고, 새로운 데이터를 바탕으로 지속적으로 모델이 개선되는 웹 프로그램 <A href = "https://sketchme.xyz">Sketch Me!</A> 제작 참여</li>
                </ul>
                <div class="month">Aprill</div>
                <ul class="project-list">
                    <li><A href = "https://www.quantumworkforce.kr">고려대학교 주관 양자대학원</A>에서 학부생 인턴십 프로그램 참가 및 Quantum Algorithm을 주제로 연구활동 참여(~2024.07)</li>
                </ul>
                <div class="month">Frebuary</div>
                <ul class="project-list">
                    <li><A href = "https://sites.google.com/view/khuqclab">Quantum Computing Lab</A>(지도교수님 : 김정산)에서 학부생 인턴 활동(~now)</li>
                </ul>
                <div class="month">January</div>
                <ul class="project-list">
                    <li><A href = "https://solved.ac/profile/mu08014">백준</A>플레티넘V 달성</li>
                </ul>
            </div>
            <div class="timeline-entry left">
                <div class="year"><strong>2023</strong></div>
                <div class="month">November</div>
                <ul class="project-list">
                    <li>NEW TEPS 339점 달성</li>
                </ul>
            </div>
            <div class="timeline-entry left">
                <div class="year"><strong>2022</strong></div>
                <div class="month">May</div>
                <ul class="project-list">
                    <li>육군 22사단 입대(~2023.11)</li>
                </ul>
            </div>
            <div class="timeline-entry left">
                <div class="year"><strong>2021</strong></div>
                <div class="month">September</div>
                <ul class="project-list">
                    <li>게임프로그래밍입문 텀프로젝트에서 cocos2D와 Pygame을 이용한 2D 슈팅게임 <A href = "https://github.com/mu08014/Ghost_Hunter">Ghost Hunter</A> 제작</li>
                </ul>
                <div class="month">August</div>
                <ul class="project-list">
                    <li>창업동아리 회기동막걸리에서 인터렉티브 픽션 게임 <A href = "https://github.com/SHT4196/Academia">Academia</A>개발팀 참여(~2022.05)</li>
                </ul>
                <div class="month">Aprill</div>
                <ul class="project-list">
                    <li>소프트웨어융합학과 복수전공 시작</li>
                </ul>
                <div class="month">Frebuary</div>
                <ul class="project-list">
                    <li>컴퓨터활용능력 1급 취득</li>
                </ul>
            </div>
        </div>
    </main>
</body>
</html>
