# 티스토리에 Github 커밋 그래프 적용하기

#### 적용할 곳을 클릭해주시면 설명으로 이동합니다.
1. [메인페이지](#1-메인페이지)
2. [사이드바](#2-사이드바)
3. [Reference](#reference)


[제 블로그에서 예시를 보실 수 있습니다](https://l4279625.tistory.com/)

---
<br>

## 1. 메인페이지
### 주의!!! 메인페이지에 들어갈 코드는 "**프라치노 공간**" 스킨에 최적화 되어있습니다.
### 해당 스킨이 아니라면 사전 작업 2번까지 진행하고 img 태그만 이용하여 요령껏 꾸며야 합니다 ㅠㅠ
![커밋 그래프 메인페이지](https://github.com/l4279625/Module_List/blob/main/images/Tistory-Commit-Graph-Mainpage.PNG?raw=true)



### 적용 방법
1. 티스토리 관리 페이지 진입
2. [꾸미기] - [스킨 편집] - [html 편집] 클릭 **(프라치노 공간 스킨이 아니라면 여기까지!)**
3. html 코드에서 [ctrl + F]로 "s_list" 검색
4. s_list 태그 내부 최상단에 아래 코드 삽입 **(깃허브닉네임, 티스토리주소 자기껄로 작성해줘야 한다!)**
5. 우측 상단의 [적용]버튼 클릭
6. :smiley: 메인 페이지를 확인해보면 잘 나올것이다!!! :smiley:

### Code

```html
<div id="home_jandi" style="position: relative; max-width:1100px; margin:auto; display:none;">
    <div style="margin:0 -10px; border-top:1px solid #E3E3E3;">
    </div>
    <!-- 링크 효과를 없애고 싶으면 a태그를 지워주세요!!!! -->
    <a href="https://github.com/깃허브닉네임" target="_blank">
        <!------------------ 제목 ------------------------->
        <h3 style="text-align: center;">
            잔디는 사랑입니다. 사랑으로 가꾸어 주세요^^
        </h3>
        <!------------------------------------------------->
        <!-- 프라치노 스킨이 아니라면 아래의 img태그를 기반으로 요령껏 꾸며주세요! -->
        <img src="https://ghchart.rshah.org/219138/깃허브닉네임" style="position: relative; width:100%;"/>
    </a>
</div>
<script>
    // 홈에서만 display="block" 처리해줌
    if (window.location.href === "본인 블로그 메인페이지 주소 복사하세요!") {
        document.getElementById('home_jandi').style.display="block";
    }
</script>
```

---
<br>

## 2. 사이드바
![커밋 그래프 사이드바](https://github.com/l4279625/Module_List/blob/main/images/Tistory-Commit-Graph-sidebar.PNG?raw=true)

### 적용 방법
1. 티스토리 관리 페이지 진입
2. [플러그인] 메뉴에서 "배너 출력" 플러그인을 활성화 해준다.
3. [꾸미기] - [사이드바] 로 들어가면 "[플러그인] HTML 배너출력"이 활성화 되었을것이다.
4. 기본 모듈 탭에 있는 해당 배너를 오른쪽의 사이드바로 드래그앤드랍 해주자 (자기가 원하는 위치에 놓으면 된다. 커스텀 잘해보자 \^ㅇ\^)
5. 해당 배너에 커서를 올리면 편집 버튼이 나오는데 클릭해주자
6. 조그만한 모달창이 뜰텐데 아래 코드를 복붙해주고 [확인] 클릭 후 변경사항 저장 **(깃허브 닉네임을 자기껄로 바꿔주는것을 잊지말자!)**
7. :star: 확인해보면 아주 잘 뜬다! :star:

### Code
```html
<!-- Include the library. -->
<script src="https://unpkg.com/github-calendar@latest/dist/github-calendar.min.js"></script>

<!-- Optionally, include the theme (if you don't want to struggle to write the CSS) -->
<link rel="stylesheet" href="https://unpkg.com/github-calendar@latest/dist/github-calendar-responsive.css" />

<div>
    <!-- Prepare a container for your calendar. -->
    <div style="text-align: center;">
        <strong>기원이의 잔디심기 대작전</strong>
    </div> 
    <div class="calendar">
        <!-- Loading stuff -->
        Loading data ...
    </div>
</div>

<script>
        GitHubCalendar(".calendar", "깃허브닉네임", { responsive: true, tooltips: false, global_stats: false}).then(function() {
            const div_calendar = document.getElementsByClassName('calendar')[0];
            div_calendar.style.minHeight = "50px";
            div_calendar.style.border = "0px";

            document.getElementsByClassName('js-calendar-graph')[0].childNodes[3].style.display = "none";
        });
</script>
```

## Reference
- [github-calendar API](https://github.com/Bloggify/github-calendar)  
- [githubchart API](https://github.com/akerl/githubchart)

<br><br><br><br>


# 감사합니다
![다운로드](https://user-images.githubusercontent.com/72638829/132350825-e6e555be-6efe-4029-94fd-26ed4b2d1182.gif)
