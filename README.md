# korean-wikipedia-corpus

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.

문장 단위로 분절한 한국어 위키피디아 코퍼스

## 사용법

Releases에서 직접 다운로드받은 후 사용하시거나, [tfds-korean 패키지](https://github.com/jeongukjae/tfds-korean)([카탈로그 페이지](https://jeongukjae.github.io/tfds-korean/datasets/korean_wikipedia_corpus.html))를 이용해 사용하세요.

## 텍스트 추출 방법

wikiextractor를 통해 한번 뽑아낸 다음, `<doc>`안에서 같은 섹션에 존재하는 문장을 전부 개행문자로 이어놓았습니다.
문장은 [kss](https://github.com/hyunwoongko/kss)를 사용하여 분리하였습니다.

문서와 문서 사이에는 개행문자 두개가 존재합니다.
문서의 첫 문장은 항상 제목입니다.
제목만을 담고 있을 경우에는 문서가 저장되지 않습니다.

즉, 아래와 같은 포맷입니다.

```text
문서1 제목
문서1 - 문장1
문서1 - 문장2
문서1 - 문장...
문서1 - 문장n

문서2 제목
문서2 - 문장1
문서2 - 문장2
문서2 - 문장...
문서2 - 문장m

문서3 제목
문서3 - 문장1
문서3 - 문장2
문서3 - 문장...
문서3 - 문장m

...
```

예시

```text
나성범
나성범(羅成範, 1989년 10월 3일 ~ )은 KBO 리그 NC 다이노스의 외야수이다.
그의 형은 KBO 리그 KIA 타이거즈의 잔류군 배터리코치인 나성용이다.

나성범 - 아마추어 시절.
2008년 신인 드래프트에서 2차 4라운드 8순위(전체 32순위)로 LG 트윈스의 지명을 받았으나 연세대학교 체육교육학과에 진학했다.
연세대학교 2학년 때인 2010년에 중앙대학교 투수 김명성과 함께 광저우 아시안 게임 예비 엔트리에 발탁됐으나 최종 엔트리에 선발되지 못했다.
그는 연고전에서 인상적인 활약을 펼쳤다.
연고전 등판 기록은 4경기에 등판해 34.2이닝동안 2승 1패, 평균자책점 2.34였다.
당시 고려대학교는 윤명준, 임치영, 문승원의 선발 트로이카와 김재율, 홍재호, 김준완 등이 이끄는 막강한 타선을 갖추고 있었고 연세대학교 체육교육학과는 그의 형인 나성용, 유민상, 최재원이 주축이 돼 상대적으로 전력이 약세였지만 그의 맹활약으로 2008년부터 2012년까지 고려대학교를 상대로 2승 1무 1패로 우위를 지켰다.

나성범 - 2012년 시즌.
신인 드래프트에서 2라운드 1순위(전체 10순위) 지명을 받아 창단 멤버로 입단했고, 뒤이어 2011년 야구 월드컵에 국가대표로 발탁됐다.
투수로 입단했으나, 당시 감독이었던 김경문의 권유로 2011년 가을 마무리 캠프를 통해 외야수로 전향했다.
2군 94경기에 출전해 타율 0.303, 16홈런, 67타점, 29도루, 33사구를 기록했다.
시즌 중에는 4할 타율을 기록했으나 손바닥 부상과 체력 저하로 인해 페이스가 떨어졌다.
남부 리그 최다 홈런, 최다 타점을 기록했고 팀 내에서 유일하게 3할 타율을 기록했다.
시즌 후 2012년 아시아 야구 선수권 대회 국가대표에 발탁됐으나 오른쪽 손등 부상으로 인해 박정준으로 교체됐다.

...
```

## 사용법

1. <https://ko.wikipedia.org/wiki/위키백과:데이터베이스_다운로드>에서 덤프파일 다운로드
2. 텍스트 파일로 변환

    ```sh
    docker run \
        --rm \
        -it \
        -w /app \
        -v `pwd`:/app \
        -v WIKI_FILE_PATH:/wiki.xml.bz2:ro \
        -e WIKI_FILE=/wiki.xml.bz2 \
        python:3.6 bash -c ./extract-text.sh
    ```

    이 단계 후에도 문서 제목과 `<doc></doc>` 태그가 남아있어 아래 스크립트를 추가했습니다.

3. 텍스트만 추출

    ```sh
    docker run \
        --rm \
        -it \
        -w /app \
        -v `pwd`:/app \
        python:3.6 bash -c ./preprocess-text.sh
    ```
