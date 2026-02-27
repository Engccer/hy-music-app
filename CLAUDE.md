# HY's Music App — 베이스 기타 연습 도구

## 개요

베이스 기타 연습을 위한 올인원 웹 애플리케이션. 메트로놈, 튜너, 코드 진행 플레이어 3가지 기능을 단일 HTML 파일로 제공한다.

- **배포**: GitHub Pages — https://engccer.github.io/hy-music-app/
- **기술 스택**: 바닐라 HTML/CSS/JavaScript, Web Audio API
- **파일 구조**: `index.html` 단일 파일 (CSS/JS 인라인)

## 주요 기능

### 1. 메트로놈 (Ctrl+1)
- BPM 20~300 조절 (슬라이더 + 직접 입력)
- 박자: 2/4, 3/4, 4/4, 6/8, 8/8
- 4종 클릭음 선택

### 2. 튜너 (Ctrl+2)
- 5현 베이스 기준음 재생: B0 / E1 / A1 / D2 / G2
- 배음 포함 사운드, +1 옥타브, 볼륨 조절

### 3. 코드 진행 플레이어 (Ctrl+3)
- 곡별 섹션(Intro, Verse, Chorus 등) 코드 진행 재생
- Space: 재생/정지, ←→: 마디 이동, ↑↓: 볼륨, Shift+↑↓: 곡 변경
- YouTube 참고 영상 링크 제공

## 수록곡 (SONGS 배열, index.html 620행~)

| # | 곡명 | 아티스트 | BPM | 박자 | 키 | 주요 코드 |
|---|------|----------|-----|------|----|-----------|
| 1 | Fake Plastic Trees | Radiohead | 75 | 4/4 | A장조 | A, E, F#m, D |
| 2 | Midnight Radio | Hedwig and the Angry Inch | 76 | 3/4 | C장조 | C, Am, F, G, Dm, Ab |
| 3 | 있지 | 자우림 | 84 | 4/4 | F#단조 | F#m, D, A, E |
| 4 | 좋지 아니한가 | 유다빈밴드 | 140 | 4/4 | Bb장조 | Bb, F, Gm, D |

## 곡 데이터 구조

```javascript
{
  title: string,      // 곡명
  artist: string,     // 아티스트
  bpm: number,        // 템포
  timeSig: number,    // 박자 (분자, 예: 4 = 4/4)
  key: string,        // 조성 (예: 'A장조', 'F#단조')
  chords: string[],   // 사용 코드 목록
  tuning: string,     // 튜닝 (현재 모두 'E Standard')
  ytUrl: string,      // YouTube 참고 영상 URL
  sections: [{        // 곡 구조
    name: string,     // 섹션명 (Intro, Verse 1, Chorus 등)
    bars: [{          // 마디 배열
      chord: string,  // 코드 심볼
      root: number    // 근음 주파수 (Hz, 베이스 옥타브)
    }]
  }]
}
```

## 접근성
- 키보드 전체 조작 지원
- ARIA live region으로 스크린 리더 알림 (BPM 변경, 재생 상태, 곡 변경)
- 고대비 다크 테마

## 곡 추가 방법
1. `SONGS` 배열 끝에 위 데이터 구조에 맞춰 객체 추가
2. 근음 주파수는 베이스 옥타브 기준 (예: A1=55.00, E1=41.20, Bb1=58.27)
3. 추가 후 별도 빌드 불필요 (정적 HTML)
