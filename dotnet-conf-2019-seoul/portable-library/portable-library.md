---
marp: true
style: |
  em { font-style: normal; }
  em:before { content: '\2018'; }
  em:after { content: '\2019'; }
  th { text-align: left; }
  section.image
    { position: absolute; left: 0; top: 0; width: 100%; height: 100%; padding: 0; line-height: 0; }
  section.image > p > img,
  section.image > p > a { display: block; margin: auto; }
  section.image.zoom img { width: 100%; }
  section.table { font-size: 1.4em; }
  section.cover em:before,
  section.cover em:after { content: ''; }
  section.cover em {
    position: absolute;
    color: maroon;
    margin-top: -1.7em; margin-left: -4.5em;
    transform: rotate(20deg);
    border-bottom: .1em solid maroon;
    border-right: .1em solid maroon;
    padding-right: .2em;
  }
  section.hiring img { width: 500px; }
---

<!-- _class: cover -->

여러 .NET 구현과 플랫폼을 두루 지원하는 라이브러리 *오픈 소스로* 만들기
=========================================================

플라네타리움 <planetariumhq.com>
홍민희 <hongminhee.org>

---

<!-- _class: image -->

[![github.com/dahlia](github.png)](https://github.com/dahlia)

<!-- 연사 소개. -->

---

[![](github-languages.png)](http://ionicabizau.github.io/github-profile-languages/?user=dahlia)

<!-- 여태 파이썬을 주로 써왔는데 왜 .NET을 썼는지? -->

---

2018년 여름
===========

 *  고전 게임은 30년이 지나도 어떻게든 즐길 수 있는데,  
    온라인 멀티플레이어 게임도 그럴 수 있을까?

 *  고전 게임은 세이브 파일만 잘 백업하면 나중에라도 이어서 할 수 있는데,
    온라인 멀티플레이어 게임은?

---

<!-- _class: image -->

![구글에서 “섭종” 검색: “섭종 환불”, “섭종 게임”, “섭종 게임 하는 법”, “섭종 온라인 게임”, “섭종 온라인”, “하오스 섭종”, “소울워커 섭종”…](google-shutdown.png)

<!-- 실제로 섭종을 아쉬워 하는 사람은 많다. -->

---

(세간에서의 뜻과는 다르지만)
서버리스 온라인 멀티플레이어 게임 만들기
========================================

---

<!-- _class: image zoom -->

[![Nine Chronicles](9c.jpg)](https://nine-chronicles.com/)

<!-- 현재 팀에서 만들고 있는 탈중앙 P2P 멀티플레이어 게임, 《나인 크로니클》. -->

---

Libplanet
=========

https://libplanet.io/

 *  게임에서 갖다 쓸 수 있는 네트워크 및 스토리지 라이브러리.
 *  중앙에서 누군가(≅ 게임사)가 서버를 운영하는 대신, 비트토렌트처럼 게이머의 기기끼리 통신.
 *  다음을 위해 블록체인 기술을 구현:
     * 모든 플레이어가 일관된 상태를 볼 수 있도록 (BFT 합의).
     * 중앙의 관계형 데이터베이스 등을 쓰지 않고도 영속성을 구현할 수 있도록.
     * 잠재적 악의적 플레이어(핵 유저, 치터)가 있어도 합의된 세계가 변조되지 않도록.

---

왜 .NET으로? 사고의 흐름
============================

 *  가장 많이 써본 언어는 파이썬이지만, 서버를 만드려는 게 아니다.
 *  기본적으로 게임 (소위) “클라이언트”끼리 알아서 모든 것을 다 해야 한다.
 *  즉, 게임 엔진과 더불어 살며 돌 라이브러리를 만들어야 한다.
 *  요즘 게임은 어떤 엔진이나 언어로 많이 만들지?
 *  역시 C++이 답인가?
     *  솔직히 달갑지 않다.
     *  게임 엔진처럼 프레임워크·엔진도 아닌, 라이브러리를 C++로 만들 자신도 없다.

---

<!-- _class: image -->

[![](techcrunch-unity.png)](https://tcrn.ch/2ClQTGr)

<!-- 새로 나오는 게임의 반 정도는 Unity로 만들어진다고 한다. -->

---

왜 Unity 플러그인이 아닌 .NET 라이브러리로?
===========================================

 *  Unity 외에도 C# 스크립팅을 지원하거나 .NET 기반의 게임 엔진은 많다.
 *  블록 익스플로러 같은 주변 도구들을 만들 때 도움이 된다.

---

다양한 .NET 구현들
==================

 -  .NET Framework
 -  Mono ← Unity가 내부적으로 쓰는 VM
 -  UWP
 -  Xamarin (iOS, macOS, Android)
 -  .NET Core

---

[.NET Standard](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)
===============

<!-- _class: table -->

| .NET Standard     | 1.0    | 1.1    | 1.2    | 1.3    | 1.4    | 1.5        | 1.6        | 2.0        |
|-------------------|--------|--------|--------|--------|--------|------------|------------|------------|
| .NET Core         | 1.0    | 1.0    | 1.0    | 1.0    | 1.0    | 1.0        | 1.0        | 2.0        |
| .NET Framework    | 4.5    | 4.5    | 4.5.1  | 4.6    | 4.6.1  | 4.6.1 2    | 4.6.1 2    | 4.6.1 2    |
| Mono              | 4.6    | 4.6    | 4.6    | 4.6    | 4.6    | 4.6        | 4.6        | 5.4        |
| Xamarin (iOS)     | 10.0   | 10.0   | 10.0   | 10.0   | 10.0   | 10.0       | 10.0       | 10.14      |
| Xamarin (macOS)   | 3.0    | 3.0    | 3.0    | 3.0    | 3.0    | 3.0        | 3.0        | 3.8        |
| Xamarin (Android) | 7.0    | 7.0    | 7.0    | 7.0    | 7.0    | 7.0        | 7.0        | 8.0        |
| UWP               | 10.0   | 10.0   | 10.0   | 10.0   | 10.0   | 10.0.16299 | 10.0.16299 | 10.0.16299 |
| Unity             | 2018.1 | 2018.1 | 2018.1 | 2018.1 | 2018.1 | 2018.1     | 2018.1     | 2018.1     |

---

<!-- _class: image -->

[![Libplanet targets .NET Standard 2.0](nuget-netstandard.png)](https://www.nuget.org/packages/Libplanet/)

<!-- Libplanet도 .NET Standard 2.0을 타깃한다. 아쉽게도 Unity는 아직 .NET Standard 2.1 지원 안 하고 있음. -->

---

다양한 OS
=========

 -  Linux
 -  macOS
 -  Windows

모바일도 합치면:

 -  Android
 -  iOS 및 iPadOS

<!-- 하지만 아직은 모바일까지 테스트하고 있지는 못하다. 추후 추가 예정 있음. -->

---

<!-- _class: image -->

[![Libplanet 테스트가 세 OS에서 통과한 모습](travis-matrix.png)](https://travis-ci.com/planetarium/libplanet/builds/117367234)

---

(Linux, macOS, Windows) × (.NET Core, Mono)
\+ .NET Framework
===========================================

<!-- .NET Framework는 Windows에서밖에 안 되니까 별도로 추가. -->

---

<!-- _class: image -->

[![Libplanet 테스트가 세 OS 및 세 .NET 구현에서 통과한 모습](azure-matrix.png)](https://github.com/planetarium/libplanet/pull/245)

---

Unity
=====

 *  한동안 CI의 빽빽한 초록불에 심리적 안정을 찾았으나…
 *  실제로 만드는 게임에서만 나타나는 현상들이 자꾸 보고된다.
 *  분명 Mono에서는 괜찮은데 Unity에서 왜 문제가? 좀 옛날 버전의 Mono를 쓰는 걸까?

---

<!-- _class: image -->

[![Unity의 다운스트림 Mono](github-unity-mono.png)](https://github.com/mono/mono/compare/master...Unity-Technologies:unity-master)

<!-- 실제로 Unity는 공식 GitHub 계정에서 자신들의 Mono 포크를 공개하고 있다. -->

---

<!-- _class: image -->

[![Unity의 깊은 다운스트림](github-unity-mono-downstream.png)](https://github.com/mono/mono/compare/master...Unity-Technologies:unity-master)

<!-- 그리고 이미 상당한 다운스트림 패치가 쌓여있다. -->

---

Unity
=====

동작이 다를 이유는 많다.

 -  상당한 다운스트림 패치가 적용된 별개의 Unity 내장 Mono
 -  Unity가 이미 깔아둔 메인 루프
 -  IL2CPP (Intermediate Language To C++)

<!-- TODO: 많다고는 했는데 막상 떠오르지가 않는다. -->

---

xunit-unity-runner
==================

github.com/planetarium/xunit-unity-runner

 -  Unity에 NUnit 실행기는 내장되어 있지만 Libplanet은 Xunit을 써서… 😭
 -  Unity 플레이어 환경에서 Xunit 테스트를 실행
 -  실제로 Mono에서 xunit.console.exe로 테스트를 실행할 때와 결과가 종종 다름

---

<!-- _class: image -->

[![Libplanet 테스트가 Unity에서도 통과한 모습](azure-matrix-unity.png)](https://github.com/planetarium/libplanet/pull/245)

<!-- 아직 Windows는 CI에서 자동화가 힘들어서 아직 못 했고,
Linux는 Unity가 Linux를 공식 지원하지 않아서 매끄럽게 되지 않는다.
추후 Linux와 Windows에서도 테스트를 돌릴 계획. -->

---

하지만 언젠가는 Unity가 .NET Core 기반으로 바뀌었으면 😇
========================================================

---

개발 환경의 일관성
==================

 *  전통적으로 IDE 친화적이었던 .NET 및 Windows 개발 문화
 *  GUI 중심의 워크플로우가 기본, CLI는 있으면 좋은 정도
 *  개발 환경의 간소화나 재현성이 아주 중요시되는 분위기는 아님
 *  개발하는 사람들의 환경의 일관성이 높다고 가정
 *  일관성이 보장되면 아주 편하기 때문에 보통의 팀에서는 일관성을 추구하는 것이 좋긴 한데…

---

개발 환경의 다양성
==================

 *  하지만 오픈 소스 프로젝트의 기여자들한테 우리가 월급을 주는 것도 아니고…
 *  기여하려면 꼭 Windows 사서 Visual Studio 설치하라고 할 수도 없고…

---

<!-- _class: image -->

[![libplanet 저장소의 주요 기여자들](github-libplanet-contributors.png)](https://github.com/planetarium/libplanet/graphs/contributors)

---

<!-- _class: image -->

[![vimrc](github-vimrc.png)](https://github.com/dahlia/nvimrc)

<!-- 한 명은 원래 Vim을 쓰던 사람이고… -->

---

<!-- _class: image -->

[![.emacs.d](github-emacsd.png)](https://github.com/longfin/.emacs.d)

<!-- 다른 한 사람은 Emacs 쓰던 사람. -->

---

개발 환경의 다양성
==================

 -  하지만 오픈 소스 프로젝트의 기여자들한테 우리가 월급을 주는 것도 아니고…
 -  기여하려면 꼭 Windows 사서 Visual Studio 설치하라고 할 수도 없고…
 -  아무튼 아주 편하게 돌아가는 단 하나의 환경을 구축하는 것보다,  
    여러 환경에서 똑같이 빌드할 수 있는 방법을 찾는 것부터 하자.

---

EditorConfig
============

IDE나 코드 편집기가 그 프로젝트의 (최소한의) 코드 스타일을 따르게 해준다.

 -  하드탭·소프트탭 여부
 -  들여 쓰기는 한 단계에 몇 칸으로 넣을지
 -  줄 당 최대 폭
 -  파일 마지막에 `LF` (EOL) 문자를 넣을지
 -  빈 줄에 들여쓰기를 위한 공백 문자를 남길지
 -  매 줄의 마지막 공백 문자들을 남길지

등등의 별 것도 아닌데 괜히 신경 쓰일 수 있는 것들을 자동으로 맞출 수 있다.

---

~~~~ ini
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
tab_width = 8
trim_trailing_whitespace = true
~~~~

<!-- 인코딩이나 들여쓰기에 쓸 문자, 들여쓰기 폭 등의 기본적인 설정. -->

---

~~~~ ini
[*.{cs,csproj,md,xml}]
indent_style = space
continuation_indent_size = 4

[*.{cs,md,xml}]
max_line_length = 100

[*.{cs,md}]
indent_size = 4

[{*.{ps1,sh},hooks/*}]
indent_size = 2

[*.{csproj,xml}]
indent_size = 2
quote_type = double
~~~~

<!-- 파일 종류마다 다른 설정이 적용 가능하고,
한 줄 당 최대 폭이나 홑따옴표나 쌍따옴표 중에 어떤 쪽으로 통일할 것인지 등을 정할 수 있다. -->

---

~~~~ ini
[*.cs]
curly_bracket_next_line = true
spaces_around_operators = true
indent_brace_style = Allman
dotnet_naming_rule.public_members_must_be_capitalized.symbols =
    public_symbols
dotnet_naming_symbols.public_symbols.applicable_kinds =
    property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities =
    public
dotnet_naming_rule.public_members_must_be_capitalized.style =
    first_word_upper_case_style
dotnet_naming_style.first_word_upper_case_style.capitalization =
    first_word_upper
dotnet_naming_rule.public_members_must_be_capitalized.severity =
    warning
~~~~

<!-- .NET만을 위한 속성들도 있다. 모든 코드 편집기나 IDE에서 지원하는 것은 아니지만,
어차피 서식을 아예 강제하는 것은 CI에서 별도의 처리가 필요하다. 뒤쪽에서 언급 예정. -->

---

[![No Plugin Necessary](editorconfig.png)](https://editorconfig.org/#download)

<!-- 이미 꽤 많은 코드 편집기나 IDE가 EditorConfig를 기본적으로 인식하고 있다.
VisualStudio나 Rider도 EditorConfig 지원이 내장되어 있다. -->

---

에디터 동작을 맞추는 것으로 충분한가?
=====================================

 *  메모장이나 `vi`로 고치는 사람도 있지 않을까?
 *  GitHub 웹 에디터로 파일 하나만 살짝 고쳐서 풀 리퀘스트를 보내면?
    (의외로 이런 경우 많음.)
 *  풀 리퀘스트가 머지되기 전에 최대한 사소한 실수들을 다 바로잡고 싶다.
 *  가능하면 로컬에서 빌드할 때 그런 체크도 함께 돌았으면 좋겠다.
    (따로 체크하는 프로그램을 돌리지 않아도 되게끔.)
 *  빌드하기 전에 코드 편집기에서 바로바로 보이면 금상첨화.

---

Roslyn Analyzers
================

 *  코먼 리스프의 매크로에 대한 .NET의 대답
 *  컴파일러 내부의 하이레벨 API인 Roslyn를 통해 코드를 읽거나 고칠 수 있다.
     *  C 전처리기 같은 토큰 수준 접근
     *  코먼 리스프 매크로 같은 구문 트리(AST) 수준 접근
     *  리플렉션 API 같은 의미론 수준 접근 (런타임 말고 빌드 시점)
     *  IL 바이트코드 수준에서도 조작 가능
 *  만든 Roslyn analyzer는 NuGet으로 배포 가능. 높은 재사용성
 *  근데 그래서 만들어 썼다는 얘기는 아니고… (아직)
 *  만들어진 Roslyn analyzer는 NuGet 의존성으로 설치하면 바로 동작 👍
 *  Visual Studio나 Rider 같은 IDE 뿐만 아니라,
    OmniSharp이 붙는 코드 편집기라면 코딩할 때 오류가 바로바로 빨간줄로 표시됨.

---

StyleCop.Analyzers
==================

github.com/DotNetAnalyzers/StyleCopAnalyzers

 *  옛날부터 쓰이던 StyleCop의 규칙들을 Roslyn analyzer로 재구현한 패키지
 *  들여쓰기, 줄바꿈, 공백 문자, 텍스트 인코딩 등의 규칙
 *  괄호 위치, 필요 없는 괄호 제거, 우선 순위가 모호한 연산자는 괄호 강제
 *  클래스나 멤버 등의 이름 규칙
 *  선언이나 `using`문의 나열 순서
 *  XML 문서 누락됐는지 체크
 *  세부적인 규칙 각각을 켜거나 끌 수 있음

---

Menees.Analyzers
================

menees.com/Analyzers.htm

 *  StyleCop에 없는 규칙이나 StyleCop의 규칙과 반대의 규칙을 구현
 *  Libplanet에서는 한 줄 당 최대 폭을 강제하기 위해 이용

---

Microsoft.DotNet.Analyzers.Compatibility
========================================

github.com/dotnet/platform-compat

 *  특정 OS 종속적인 API를 쓰는지 체크
 *  [`RuntimeInformation.IsOSPlatform()`][1] 메서드를 써서 조건문으로 감싸면 그 안쪽은 무시
 *  폐기된(deprecated) API를 쓰는지 체크
 *  옛 .NET Framework (4.6.1) 또는 UWP에서 못 쓰는 API를 쓰는지 체크

[1]: https://docs.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.runtimeinformation.isosplatform

---

테스트 코드 커버리지
====================

nuget.org/packages/Microsoft.CodeCoverage

~~~~ ps1
dotnet test --logger trx --collect "Code coverage"
CodeCoverage.exe analyze /output:report.xml *.coverage
~~~~

---

<!-- _class: image -->

[![](github-codecov.png)](https://github.com/planetarium/libplanet/pull/545#issuecomment-536581831)

---

DocFX
=====

dotnet.github.io/docfx

 *  Markdown 기반의 정적 웹사이트 생성기
 *  C# 문서의 XML 주석을 추출하여 API 문서도 자동 생성
 *  API 문서 뿐만 아니라 가이드나 튜토리얼 문서를 통합해서 관리 가능
 *  문서 생성기라기 보다는 문서를 포함한 프로젝트 웹사이트를 만들어주는 느낌
 *  Python 쪽에서 많이 쓰는 Sphinx와 비슷한 위치

---

<!-- _class: image -->

[![](libplanet-website.png)](https://docs.libplanet.io/)

<!-- DocFX로 생성한 Libplanet 웹사이트. -->

---

<!-- _class: image -->

[![](libplanet-api-docs.png)](https://docs.libplanet.io/)

<!-- DocFX로 생성한 Libplanet API 문서. -->

---

자질구래한 릴리스 과정
======================

 *  Git 태그 생성
 *  체인지로그 추출
 *  GitHub Releases에 패키지 파일 업로드
 *  API 문서와 웹사이트 생성 및 업로드
 *  NuGet에 패키지 업로드
 *  메인테이너 중 누구라도 쉽게 릴리스할 수 있게 자동화할 수 없을까?

---

<!-- _class: image -->

[![](github-actions.png)](https://github.com/planetarium/libplanet/runs/242816661)

<!-- Git에 새 태그를 푸시하면 GitHub Actions로 릴리스 작업이 수행됨. -->

---

<!-- _class: image -->

[![](github-releases.png)](https://github.com/planetarium/libplanet/releases)

<!-- GitHub Releases에 새 릴리스가 올라가고, CHANGES.md 파일의 해당 버전 섹션을 추출해서 내용으로 채움. -->

---

<!-- _class: image -->

[![](github-releases-file.png)](https://github.com/planetarium/libplanet/releases/tag/0.6.0)

<!-- 다운로드할 수 있도록 .nupkg 파일이 함께 첨부됨. -->

---

<!-- _class: image -->

[![](libplanet-website-release.png)](https://docs.libplanet.io/0.6.0/)

<!-- GitHub Pages에 해당 버전의 DocFX 웹사이트를 만들어서 업로드. -->

---

<!-- _class: image -->

[![](nuget-libplanet.png)](https://www.nuget.org/packages/Libplanet/)

<!-- NuGet에도 같이 올라감. -->

---

<!-- _class: image -->

[![](nuget-libplanet-prereleases.png)](https://www.nuget.org/packages/Libplanet/)

<!-- 태그 푸시가 아니더라도 매 푸시가 프리릴리스 형식으로 NuGet에 올라가게 되어 있음. -->

---

마무리: .NET + 오픈 소스, 어땠나
================================

아쉬웠던 것들.

 *  MS가 열심히 오픈 소스를 하고 있지만, 많은 .NET 프로그래머들은 아직은 오픈 소스에 미온적
     *  소스 코드를 여전히 Git이 아니라 압축 파일로 배포한다거나
     *  소스 코드 없이 DLL만 배포한다거나
     *  소스 코드는 공개했는데 라이선스 명시가 없어서 오픈 소스가 아니라거나
 *  .NET Core로 넘어가는 과도기적 상황
     *  아직 .NET Framework만 타깃하는 NuGet 패키지도 많다.
     *  Unity는 .NET Core로 언제 넘어갈 것인가.

---

마무리: .NET + 오픈 소스, 어땠나
================================

좋았던 것들.

 *  Windows 일변도에 오픈 소스와는 담을 쌓았다는 고정관념과 달리,
    .NET Core나 Mono 덕분에 Linux나 macOS에서도 얼마든지 개발 가능.
 *  Visual Studio를 쓰지 않으면 불편을 감수해야 했던 10년 전과는 다르게,
    `dotnet` CLI나 OmniSharp 등 다양한 개발 환경을 두루 지원할 수 있는 기반이 마련돼 있다.
 *  Roslyn analyzer의 활용 방법은 무궁무진해 보인다.
 *  GitHub이 이제 Microsoft 것이라 그런지, GitHub에서 C# 및 .NET 지원을 아주 잘 해준다.
    (예: 패키지 레지스트리, 코드 분석 등.)

---

<!-- _class: hiring -->

감사합니다! 같이 일해요! bit.ly/plnt-hire-2019
========================

[![](hiring.png)](https://bit.ly/plnt-hire-2019) [![](planetarium-sponser.png)](https://planetariumhq.com/)

발표 자료: bit.ly/hong-netconf-2019