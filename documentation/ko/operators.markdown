---
layout: documentation
title: ReactiveX - Operators
lang: ko
id: operators
---

<h1>연산자 소개</h1>

ReactiveX를 지원하는 언어 별 구현체들은 다양한 연산자들을 제공하는데, 이 중에는 공통적으로 제공되는 연산자도 있지만 반대로 특정 구현체에서만 제공하는 연산자들도 존재한다.
또한, 언어별 구현체들은 이미 언어에서 제공하는 메서드의 이름과 유사한 형태로 연산자의 네이밍 컨벤션을 유지하고 있다.

<h2>연산자 체인</h2>

거의 모든 연산자들은 Observable 상에서 동작하고 Observable을 리턴한다. 이 접근 방법은 연산자들을 연달아 호출 할 수 있는 연산자 체인을 제공한다. 
연산자 체인에서 각각의 연산자는 이전 연산자가 리턴한 Observable을 기반으로 동작하며 동작에 따라 Observable을 변경한다.

특정 클래스가 제공하는 여러 메서드들을 호출하여 클래스의 항목들을 변경하는 빌더 패턴과 같은 것도 존재한다. 빌더 패턴 역시 연산자 체인과 유사하게 메서드 체인을 제공한다.
하지만, 빌더 패턴의 메서드 체인과는 달리 Observable의 연산자 체인은 <em>호출 순서</em>에 따라 실행 결과가 달라지는 차이점이 있다.

따라서, Observable의 연산자 체인은 원본 Observable과 독립적으로 실행될 수 없고 <em>순서대로</em> 실행되어야 한다. 왜냐하면, 이미 이해하고 있듯이 연산자 체인에서 먼저 실행된 연산자가 리턴한 Observable을 기반으로 다음 연산자가 동작하기 때문이다.

<h2>ReactiveX의 연산자</h2>

이 페이지에서는 먼저 ReactiveX의 &ldquo;핵심&rdquo; 연산자들을 나열하고, 각 연산자별로 제공된 링크를 통해 연산자들이 어떻게 동작하고 ReactiveX의 여러 언어별 구현체에서 연산자자가 어떻게 구현했는지 자세히 설명한다.

그 후에는 &ldquo;결정 트리&rdquo;를 통해 여러분에게 필요한 적절한 연산자를 선택할 수 있는 유용한 가이드를 제공한다.

마지막으로, ReactiveX의 다양한 언어 별 구현체에서 제공하는 모든 연산자들을 알파벳 순으로 소개한다. 뿐만 아니라, 각각의 연산자 역시 링크를 통해 언어 별 구현체가 제공하는 연산자와 가장 유사한 핵심 연산자에 관한 자세한 설명을 제공한다.
(예를 들어, Rx.NET의 &ldquo;SelectMany&rdquo; 연산자가 제공하는 링크는 Rx.NET의 SelectMany 연산자가 구현하는 ReactiveX의 <span class="operator">FlatMap</span> 연산자에 대한 구체적으로 설명한다)

만약 직접 연산자를 구현하고 싶다면 <a href="implement-operator.html">연산자 구현하기</a>를 참고하기 바란다.

<h4>소개 순서</h4> 
<ol>
 <li><a href="#categorized">카테고리 별 연산자</a></li>
 <li><a href="#tree">Observable 연산자의 결정 트리</a></li>
 <li><a href="#alphabetical">Observable 연산자 리스트(알파벳순)</a></li>
</ol>

<h1 id="categorized">카테고리 별 연산자</h1>

<h2 id="creating">Observable 생성</h2>

새로운 Observable을 만드는 연산자들

* [**`Create`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html) — 직접적인 코드 구현을 통해 옵저버 메서드를 호출하여 Observable을 생성한다
* [**`Defer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html) — 옵저버가 구독하기 전까지는 Observable 생성을 지연하고  구독이 시작되면 옵저버 별로 새로운 Observable을 생성한다
* [**`Empty`/`Never`/`Throw`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html) — 아주 정확하고 제한된 행동을 하는 Observable을 생성한다
* [**`From`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html) — 다른 객체나 자료 구조를 Observable로 변환한다
* [**`Interval`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/interval.html) — 특정 시간별로 연속된 정수형을 배출하는 Observable을 생성한다
* [**`Just`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html) — 객체 하나 또는 객채집합을 Observable로 변환한다. 변환된 Observable은 원본 객체들을 발행한다
* [**`Range`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/range.html) — 연속된 범위(Range)의 정수를 발행하는 Observable을 생성한다
* [**`Repeat`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html) — 특정 항목이나 연속된 항목들을 반복적으로 배출하는 Observable을 생성한다
* [**`Start`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html) — 함수의 실행 결과를 배출하는 Observable을 생성한다
* [**`Timer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timer.html) — 지정된 시간이 지나고 난 후 항목을 하나 배출하는 Observable을 생성한다

<h2 id="transforming">Observable 변환</h2>

Observable이 배출한 항목들을 변환하는 연산자들

* [**`Buffer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html) — Observable로부터 정기적으로 항목들을 수집하고 묶음으로 만든 후에 묶음 안에 있는 항목들을 한번에 하나씩 배출하지 않고 수집된 묶음 단위로 배출한다
* [**`FlatMap`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html) — 하나의 Observable이 발행하는 항목들을 여러개의 Observable로 변환하고, 항목들의 배출을 차례차례 줄 세워 하나의 Observable로 전달한다
* [**`GroupBy`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/groupby.html) — 원본 Observable이 배출하는 항목들을 키(Key) 별로 묶은 후 Observable에 담는다. 이렇게 키 별로 만들어진 Observable들은 자기가 담고 있는 묶음의 항목들을 배출한다
* [**`Map`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html) — Observable이 배출한 항목에 함수를 적용한다
* [**`Scan`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/scan.html) — Observable이 배출한 항목에 연속적으로 함수를 적용하고 실행한 후 성공적으로 실행된 함수의 리턴 값을 발행한다
* [**`Window`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html) — 정기적으로 Observable의 항목들을 더 작은 단위의 Observable 윈도우로 나눈 후에, 한번에 하나씩 항목들을 발행하는 대신 작게 나눠진 윈도우 단위로 항목들을 배출한다

<h2 id="filtering">Observable 필터링</h2>

소스 Observable에서 선택적으로 항목을 배출하는 연산자들

* [**`Debounce`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/debounce.html) — Observable의 시간 흐름이 지속되는 상태에서 다른 항목들은 배출하지 않고 특정 시간 마다 그 시점에 존재하는 항목 하나를 Observable로부터 배출한다
* [**`Distinct`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/distinct.html) — Observable이 배출하는 항목들 중 중복을 제거한 항목들을 배출한다
* [**`ElementAt`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/elementat.html) — Obserable에서 <i>n</i>번째 항목만 배출한다
* [**`Filter`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html) — 테스트 조건을 만족하는 항목들만 배출한다
* [**`First`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html) — 맨 첫 번째 항목 또는 조건을 만족하는 첫 번째 항목만 배출한다
* [**`IgnoreElements`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/ignoreelements.html) — 항목들을 배출하지는 않고 종료 알림은 보낸다
* [**`Last`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html) — Observable의 마지막 항목만 배출한다
* [**`Sample`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sample.html) — 특정 시간 간격으로 최근에 Observable이 배출한 항목들을 배출한다
* [**`Skip`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skip.html) — Observable이 배출한 처음 <i>n</i>개의 항목들을 숨긴다
* [**`SkipLast`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skiplast.html) — Observable이 배출한 마지막 <i>n</i>개의 항목들을 숨긴다
* [**`Take`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/take.html) — Observable이 배츨한 처음 <i>n</i>개의 항목들만 배출한다
* [**`TakeLast`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html) — Observable이 배출한 마지막 <i>n</i>개의 항목들만 배출한다

<h2 id="combining">Observables 결합</h2>

여러 개의 소스 Observable들을 하나의 Observable로 만드는 연산자들

* [**`And`/`Then`/`When`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html) — 두 개 이상의 Observable들이 배출한 항목들을 'Pattern'과 'Plan' 중계자를 이용해서 결합한다
* [**`CombineLatest`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/combinelatest.html) — 두 개의 Observable 중 하나가 항목을 배출할 때 배출된 마지막 항목과 다른 한 Observable이 배출한 항목을 결합한 후 함수를 적용하여 실행 후 실행된 결과를 배출한다
* [**`Join`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/join.html) — A Observable과 B Observable이 배출한 항목들을 결합하는데, 이때 B Observable은 배출한 항목이 타임 윈도우를 가지고 있고 이 타임 윈도우가 열린 동안 A Observable은 항목의 배출을 계속한다. Join 연산자는 B Observable의 항목을 배출하고 배출된 항목은 타임 윈도우를 시작시킨다. 타임 윈도우가 열려 있는 동안 A Observable은 자신의 항목들을 계속 배출하여 이 두 항목들을 결합한다
* [**`Merge`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html) — 복수 개의 Observable들이 배출하는 항목들을 머지시켜 하나의 Observable로 만든다
* [**`StartWith`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/startwith.html) — 소스 Observable이 항목을 배출하기 전에 다른 항목들을 앞에 추가한 후 배출한다
* [**`Switch`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html) — Observable들을 배출하는 Observable을 싱글 Observable로 변환하다. 변환된 싱글 Observable은 변환 전 소스 Observable들이 배출한 항목들을 배출한다
* [**`Zip`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html) — 명시한 함수를 통해 여러 Observable들이 배출한 항목들을 결합하고 함수의 실행 결과를 배출한다

<h2 id="error">오류 처리 연산자</h2>

Observable이 던진 오류를 복구할 수 있도록 도와주는 연산자들

* [**`Catch`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html) — 오류를 무시하고 배출되는 항목들을 계속 진행시켜 'onError'로부터 전달된 오류를 복구한다
* [**`Retry`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/retry.html) — 만약 소스 Observable이 'onError' 알림을 보낼 경우, 오류 없이 실행이 완료되기를 기대하며 재구독을 시도한다

<h2 id="utility">Observable 유틸리티 연산자</h2>

Obserable과 함께 동작하는 유용한 도우미 연산자들

* [**`Delay`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/delay.html) — Observable의 배출을 특정 시간동안 미룬다
* [**`Do`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html) — Observable의 생명주기 동안 발생하는 여러 이벤트에서 실행 될 액션을 등록한다
* [**`Materialize`/`Dematerialize`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/materialize-dematerialize.html) — 배출된 항목이 어떤 알림을 통해 옵저버에게 전달 됐는지를 표현하며, 그 반대 과정을 수행할 수 있다
* [**`ObserveOn`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/observeon.html) — 옵저버가 어느 스케줄러 상에서 Observable을 관찰할지 명시한다
* [**`Serialize`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/serialize.html) — Observable이 직렬화된 호출을 생성하고 제대로 동작하도록 강제한다
* [**`Subscribe`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html) — Observable이 배출하는 항목과 알림을 기반으로 동작한다
* [**`SubscribeOn`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribeon.html) — Observable을 구독할 때 사용할 스케줄러를 명시한다
* [**`TimeInterval`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timeinterval.html) — 항목들을 배출하는 Observable을, 항목을 배출하는데 걸린 시간이 얼마인지를 가리키는 Observable로 변환한다
* [**`Timeout`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timeout.html) — 소스 Obvservable을 그대로 전달하지만, 대신 특정 시간 동안 배출된 항목이 없으면 오류 알림을 보낸다
* [**`Timestamp`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timestamp.html) — Observable이 배출한 항목에 타임 스탬프를 추가한다
* [**`Using`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/using.html) — 소스 Observable과 동일한 생명주기를 갖는 Observable을 생성하는데, 이 Observable은 생명주기가 완료되면 리소스를 종료하고 반환한다

<h2 id="conditional">조건과 불린 연산자(Boolean)</h2>

하나 이상의 Observable 또는 Observable이 배출한 항목을 평가하는 연산자들

* [**`All`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html) — Observable이 배출한 전체 항목들이 어떤 조건을 만족시키는지 판단한다
* [**`Amb`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/amb.html) — 두 개 이상의 소스 Observable이 주어 질때, 그 중 첫 번째로 항목을 배출한 Observable이 배출하는 항목들을 전달한다
* [**`Contains`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html) — Observable이 특정 항목을 배출하는지 아닌지를 판단한다
* [**`DefaultIfEmpty`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/defaultifempty.html) — 소스 Observable이 배출하는 항목을 전달한다. 만약 배출되는 항목이 없으면 기본 항목을 배출한다
* [**`SequenceEqual`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sequenceequal.html) — 두 개의 Observable이 항목을 같은 순서로 배출하는지 판단한다
* [**`SkipUntil`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipuntil.html) — 두 번째 Observable이 항목을 배출하기 전까지 배출된 항목들을 버린다
* [**`SkipWhile`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipwhile.html) — 특정 조건이 false를 리턴하기 전까지 Observable이 배출한 항목들을 버린다
* [**`TakeUntil`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takeuntil.html) — 두 번째 Observable이 항목을 발행하기 시작햤거나 두 번째 Observable이 종료되면 그 때부터 발행되는 항목들은 버린다
* [**`TakeWhile`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takewhile.html) — 특정 조건이 false를 리턴하기 시작하면 그 이후에 배출되는 항목들을 버린다

<h2 id="mathematical">수학과 집계 연산자</h2>

Observable이 배출하는 항목 전체를 대상으로 동작하는 연산자들

* [**`Average`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html) — Observable이 발행한 항목의 평균 값을 발행한다
* [**`Concat`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/concat.html) — 두 개 이상의 Observable들이 항목을 발행할 때 Observable 순서대로 배출하는 항목들을 하나의 Observable 배출로 연이어 배출한다
* [**`Count`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html) — 소스 Observable이 발행한 항목의 개수를 배출한다
* [**`Max`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/max.html) — Observable이 발행한 항목 중 값이 가장 큰 항목을 배출한다
* [**`Min`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/min.html) — Observable이 발행한 항목 중 값이 가장 작은 항목을 배출한다
* [**`Reduce`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html) — Observable이 배출한 항목에 함수를 순서대로 적용하고 함수를 연산한 후 최종 결과를 발행한다
* [**`Sum`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html) — Observable이 배출한 항목의 합계를 배출한다

<h2 id="backpressure">역압(Backpressure) 연산자</h2>

* [**backpressure operators**]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html) — 옵저버가 소비하는 것보다 더 빠르게 항목들을 생산하는 Observable을 복재하는 전략

<h2 id="connectable">연결 가능한 Observable 연산자</h2>

좀 더 정확히 제어되는 구독 역학을 가진 전문 Observable들

* [**`Connect`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/connect.html) — 구독자가 항목 배출을 시작할 수 있도록 연결 가능한 Observable에게 명령을 내린다
* [**`Publish`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html) — 일반 Observable을 연결 가능한 Observable로 변환한다
* [**`RefCount`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/refcount.html) — 일반 Observable처럼 동작하는 연결 가능한 Observable을 만든다
* [**`Replay`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/replay.html) — 비록 옵저버가 Observable이 항목 배출을 시작한 후에 구독을 했다 하더라도 배출된 모든 항목들을 볼 수 있도록 한다

<h2 id="conversion">Observable 변환 연산자</h2>

* [**`To`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html) — Observable을 다른 객체나 자료 구조로 변환한다

<div id="tree">
<style>
   div#tree dl { margin-top: 0;
                 margin-bottom: 1.5em;
                 margin-left: 1.5em; }
   div#tree dl#outer>dt { font-weight: bold;
                          margin-right: -1.5em;
                          margin-top: .5em; }
   div#tree dl#outer>dd { margin-top: .5em; }
   div#tree dt { font-weight: normal;
                 margin-right: -1.5em; }
   div#tree dl > dt::before { content: "…"; }
   div#tree dl#outer > dt::before { content: ""; }
   div#tree dd::before { content: ": "; }
   div#tree dd.sub::before { content: ""; }

   div#tree dt { float: left; clear: left; }
   div#tree dd { float: left;
                 margin-start: 0;
                 -webkit-margin-start: 0;
                 margin-left: 1.5em; }
   div#tree dd.sub { float: none;
                     margin-left: 0; }
</style>
  <h1>Observable 연산자 결정 트리</h1>
  <p>
   이 트리는 여러분이 원하는 ReactiveX의 Observable 연산자를 찾는데 도움을 줄 것이다.
  </p>
<dl id="outer">
 <dt>나는 새로운 Observable을 생성하고 싶은데 그 Observable이</dt>
  <dd class="sub"><dl>
   <dt>특정 항목을 생성해야 한다면:</dt>
    <dd><a href="operators/just.html">Just</a></dd>
    <dd class="sub"><dl>
     <dt>구독 시점에 호출된 함수를 통해 생성된 항목을 리턴해야 한다면:</dt>
      <dd><a href="operators/start.html">Start</a></dd>
     <dt>구독 시점에 호출된 <code>Action</code>, <code>Callable</code>, <code>Runnable</code> 또는 그와 유사한 함수 등을 통해 생성된 항목을 리턴해야 한다면:</dt>
      <dd><a href="operators/from.html">From</a></dd>
     <dt>지정된 시간 이후에 항목을 배출해야 한다면:</dt>
      <dd><a href="operators/timer.html">Timer</a></dd>
     </dl></dd>
   <dt>특정 <code>Array</code>, <code>Iterable</code> 또는 유사한 형태의 소스로부터 항목들을 배출해야 한다면:</dt>
    <dd><a href="operators/from.html">From</a></dd>
   <dt>퓨처(Future)에서 항목을 조회해서 배출해야 한다면:</dt>
    <dd><a href="operators/start.html">Start</a></dd>
   <dt>퓨처에서 연속된 항목을 가져와야 한다면:</dt>
    <dd><a href="operators/from.html">From</a></dd>
   <dt>반복적으로 연속된 항목을 배출해야 한다면:</dt>
    <dd><a href="operators/repeat.html">Repeat</a></dd>
   <dt>사용자가 정의한 로직을 통해 생성되어야 한다면:</dt>
    <dd><a href="operators/create.html">Create</a></dd>
   <dt>각각의 옵저버가 Observable을 구독한 후에 생성되어야 한다면:</dt>
    <dd><a href="operators/defer.html">Defer</a></dd>
   <dt>연속된 정수를 배출해야 한다면:</dt>
    <dd><a href="operators/range.html">Range</a></dd>
    <dd class="sub"><dl>
     <dt>특정 시간 간격별로 항목을 배출해야 한다면:</dt>
      <dd><a href="operators/interval.html">Interval</a></dd>
      <dd class="sub"><dl>
       <dt>특정 시간 후에 항목을 배출해야 한다면:</dt>
       <dd><a href="operators/timer.html">Timer</a></dd>
      </dl></dd>
    </dl></dd>
   <dt>항목 배출 없이 실행을 완료해야 한다면:</dt>
    <dd><a href="operators/empty-never-throw.html">Empty</a></dd>
   <dt>아무일도 하지 않아야 한다면:</dt>
    <dd><a href="operators/empty-never-throw.html">Never</a></dd>
  </dl></dd>

 <dt>다른 Observable을 결합시켜 새로운 Observable을 생성해야 한다</dt>
  <dd class="sub"><dl>
   <dt>그리고 순서와 상관없이 전달 된 모든 Observable이 가진 항목 전체를 배출해야 한다면:</dt>
    <dd><a href="operators/merge.html">Merge</a></dd>
   <dt>그리고 전달 된 Observable의 순서대로 Observable이 가진 모든 항목들을 배출해야 한다면:</dt>
    <dd><a href="operators/concat.html">Concat</a></dd>
   <dt>생성하고 싶은 Observable은, 두 개 이상의 Observable이 가진 항목들을 순서대로 결합시켜 새로운 항목을 배출해야 하는데:</dt>
    <dd class="sub"><dl>
     <dt><em>각각</em>의 Observable이 항목을 배출 할 때마다 그 항목들을 결합시켜 배출해야 한다면:</dt>
      <dd><a href="operators/zip.html">Zip</a></dd>
     <dt>Observable 중 <em>하나</em>라도 항목을 배출할 경우에 마지막으로 배출된 항목들을 결합시켜 배출해야 한다면:</dt>
      <dd><a href="operators/combinelatest.html">CombineLatest</a></dd>
     <dt>하나의 Observable이 배출한 항목의 타임 윈도우가 열려있는 시간 동안 다른 Observable이 항목을 배출할 때마다 새로운 항목을 배출해야 한다면:</dt>
      <dd><a href="operators/join.html">Join</a></dd>
     <dt><code>Pattern</code>과 <code>Plan</code> 중계자를 이용해서 항목을 배출해야 한다면:</dt>
      <dd><a href="operators/and-then-when.html">And/Then/When</a></dd>
    </dl></dd>
   <dt>그리고 가장 최근에 항목을 배출한 Observable을 통해서만 항목을 배출해야 한다면:</dt>
    <dd><a href="operators/switch.html">Switch</a></dd>
  </dl></dd>

 <dt>Observable이 배출한 항목들을 변환한 후에 다시 배출해야 하는데</dt>
  <dd class="sub"><dl>
   <dt>함수와 함께 항목을 한번에 하나씩 변환 후 배출해야 한다면:</dt>
    <dd><a href="operators/map.html">Map</a></dd>
   <dt>해당 Observable이 배출한 모든 항목들을 하나의 Observable이 배출하는 형태로 배출해야 한다면:</dt>
    <dd><a href="operators/flatmap.html">FlatMap</a></dd>
    <dd class="sub"><dl>
     <dt>순서대로 Observable이 배출한 항목들을 연결지어 배출해야 한다면:</dt>
      <dd><a href="operators/flatmap.html">ConcatMap</a></dd>
    </dl></dd>
   <dt>앞에서 실행 된 결과를 기반으로 항목을 변환한 후 배출해야 한다면:</dt>
    <dd><a href="operators/scan.html">Scan</a></dd>
   <dt>타임 스탬프를 추가하여 변환한 후 배출해야 한다면:</dt>
    <dd><a href="operators/timestamp.html">Timestamp</a></dd>
   <dt>항목 배출 전까지 경과한 시간을 가리키는 객체로 변환한 후에 배출해야 한다면:</dt>
    <dd><a href="operators/timeinterval.html">TimeInterval</a></dd>
  </dl></dd>

 <dt>Observable이 항목을 배출하기 전에 항목의 배출 시간을 지연시켜야 한다면:</dt>
  <dd><a href="operators/delay.html">Delay</a></dd>

 <dt>Observable이 배출하는 항목들<em>과</em> 알림들을 다시 항목들로 변환 후 배출해야 하는데</dt>
  <dd class="sub"><dl>
   <dt>이때 배출하는 항목들을 <code>알림</code> 객체로 감싸서(wrapping) 배출해야 한다면:</dt>
    <dd><a href="operators/materialize-dematerialize.html">Materialize</a></dd>
    <dd class="sub"><dl>
     <dt>이 알림 객체가 다시 풀릴 수(unwrapping) 있다면:</dt>
      <dd><a href="operators/materialize-dematerialize.html">Dematerialize</a></dd>
    </dl></dd>
  </dl></dd>

 <dt>Observable이 배출하는 모든 객체를 무시하고 completed/error 알림만 전달해야 한다면:</dt>
  <dd><a href="operators/ignoreelements.html">IgnoreElements</a></dd>

 <dt>Observable이 가진 항목을 그대로를 배출하지만 배출 전에 다른 항목들을 먼저 배출될 수 있도록 추가해야 한다면:</dt>
  <dd><a href="operators/startwith.html">StartWith</a></dd>
  <dd class="sub"><dl>
   <dt>만약 소스 Observable이 비어있을 경우 기본 항목을 추가해야 한다면:</dt>
    <dd><a href="operators/defaultifempty.html">DefaultIfEmpty</a></dd>
  </dl></dd>

 <dt>Observable이 배출하는 항목들을 모아둔 후 버퍼로 다시 배출해야 한다면:</dt>
  <dd><a href="operators/buffer.html">Buffer</a></dd>
  <dd class="sub"><dl>
   <dt>그 중 마지막에 배출된 항목이 추가된 버퍼만 배출해야 한다면:</dt>
    <dd><a href="operators/takelast.html">TakeLastBuffer</a></dd>
  </dl></dd>

 <dt>하나의 Observable을 여러 Observable로 나눠야 한다:</dt>
  <dd><a href="operators/window.html">Window</a></dd>
  <dd class="sub"><dl>
   <dt>그 중 유사한 항목들을 같은 Observable에 모아 두어야 한다면:</dt>
    <dd><a href="operators/groupby.html">GroupBy</a></dd>
  </dl></dd>

 <dt>Observable이 배출한 특정 항목을 조회해야 하는데</dt>
  <dd class="sub"><dl>
   <dt>Observable이 완료되기 전에 마지막으로 배출한 항목을 조회해야 한다면:</dt>
    <dd><a href="operators/last.html">Last</a></dd>
   <dt>배출된 항목이 단지 하나이고 이것을 조회해야 한다면:</dt>
    <dd><a href="operators/first.html">Single</a></dd>
   <dt>배출한 첫 번째 항목을 조회해야 한다면:</dt>
    <dd><a href="operators/first.html">First</a></dd>
  </dl></dd>

 <dt>Observable의 특정 항목만 재배출 해야 하는데</dt>
  <dd class="sub"><dl>
   <dt>어떤 조건을 만족시키지 않는 항목들을 필터링해서 재배출 해야 한다면:</dt>
    <dd><a href="operators/filter.html">Filter</a></dd>
   <dt>첫 번째 항목만 재배출 해야 한다면:</dt>
    <dd><a href="operators/first.html">First</a></dd>
   <dt>처음 몇 개의 항목<em>들</em>만 재배출 해야 한다면:</dt>
    <dd><a href="operators/take.html">Take</a></dd>
   <dt>마지막 항목만 재배출 해야 한다면:</dt>
    <dd><a href="operators/last.html">Last</a></dd>
   <dt><i>몇 번째</i> 위치한 항목만 재배출 해야 한다면:</dt>
    <dd><a href="operators/elementat.html">ElementAt</a></dd>
   <dt>재배출할 항목들이 처음 몇개 이후의 것들일 경우</dt>
    <dd class="sub"><dl>
     <dt>처음 <i>몇 개</i>의 항목들 이후의 것들 이라면:</dt>
      <dd><a href="operators/skip.html">Skip</a></dd>
     <dt>특정 조건을 만족시킨 이후의 것들 이라면:</dt>
      <dd><a href="operators/skipwhile.html">SkipWhile</a></dd>
     <dt>초기 특정 시간 이후에 배출된 항목들 이라면:</dt>
      <dd><a href="operators/skip.html">Skip</a></dd>
     <dt>두 번째 Observable이 항목을 배출한 이후의 것들 이라면:</dt>
      <dd><a href="operators/skipuntil.html">SkipUntil</a></dd>
    </dl></dd>
   <dt>마지막 항목 몇개를 제외한 경우</dt>
    <dd class="sub"><dl>
     <dt>마지막 <i>몇 개</i> 항목을 제외한 것들 이라면:</dt>
      <dd><a href="operators/skiplast.html">SkipLast</a></dd>
     <dt>특정 조건을 만족할때 까지의 것들 이라면:</dt>
      <dd><a href="operators/takewhile.html">TakeWhile</a></dd>
     <dt>소스 Observable이 완료되기 이전 특정 시간 동안 배출한 것들을 제외한 것이라면:</dt>
      <dd><a href="operators/skiplast.html">SkipLast</a></dd>
     <dt>두 번째 Observable이 항목을 배출한 이후에 배출된 것들을 제외한 것이라면:</dt>
      <dd><a href="operators/takeuntil.html">TakeUntil</a></dd>
    </dl></dd>
   <dt>주기적으로 Observable을 샘플링해서 재배출해야 한다면:</dt>
    <dd><a href="operators/sample.html">Sample</a></dd>
   <dt>특정 시간이 지나고 나서 배출된 항목들만 재배출 해야 한다면:</dt>
    <dd><a href="operators/debounce.html">Debounce</a></dd>
   <dt>이미 배출된 항목과 동일한 것들을 제외시켜 재배출 해야 한다면:</dt>
    <dd><a href="operators/distinct.html">Distinct</a></dd>
    <dd class="sub"><dl>
     <dt>만약 중복된 항목이 바로 연이어 배출된다면:</dt>
      <dd><a href="operators/distinct.html">DistinctUntilChanged</a></dd>
    </dl></dd>
   <dt>항목 배출이 시작된 이후에 얼마 동안 구독을 지연시켜야 한다면:</dt>
    <dd><a href="operators/delay.html">DelaySubscription</a></dd>
  </dl></dd>

 <dt>항목들을 배출하는 Observable 컬랙션 중에 첫 번째로 항목을 배출하는 Observable의 항목만 배출해야 한다면:</dt>
  <dd><a href="operators/amb.html">Amb</a></dd>

 <dt>Observable이 배출한 연속된 항목 전체를 평가해야 한다</dt>
  <dd class="sub"><dl>
   <dt>그리고 항목 <em>전체</em>가 테스트를 통과했는지를 가리키는 boolean 타입 항목 하나를 배출해야 한다면:</dt>
    <dd><a href="operators/all.html">All</a></dd>
   <dt>그리고 항목 전체 중 <em>하나라도</em> 테스트를 통과했는지를 가리키는 boolean 타입 항목 하나를 배출해야 한다면:</dt>
    <dd><a href="operators/contains.html">Contains</a></dd>
   <dt>그리고 Observable이 항목을 배출하지 못했는지를 가리키는 boolean 타입 항목 하나를 배출해야 한다면:</dt>
    <dd><a href="operators/contains.html">IsEmpty</a></dd>
   <dt>그리고 두 Observable이 같은 순서대로 항목들을 배출했는지를 가리키는 boolean 타입 하나를 배출해야 한다면:</dt>
    <dd><a href="operators/sequenceequal.html">SequenceEqual</a></dd>
   <dt>그리고 전체 배출된 항목의 평균 값을 항목을 배출해야 한다면:</dt>
    <dd><a href="operators/average.html">Average</a></dd>
   <dt>그리고 전체 배출된 항목의 합계를 배출해야 한다면:</dt>
    <dd><a href="operators/sum.html">Sum</a></dd>
   <dt>그리고 얼마나 많은 항목들이 배출됐는지를 배출해야 한다면:</dt>
    <dd><a href="operators/count.html">Count</a></dd>
   <dt>그리고 가장 큰 값을 가진 항목을 배출해야 한다면:</dt>
    <dd><a href="operators/max.html">Max</a></dd>
   <dt>그리고 가장 작은 값을 가진 항목을 배출해야 한다면:</dt>
    <dd><a href="operators/min.html">Min</a></dd>
   <dt>배출되는 항목 순서대로 각각에 집계 함수를 적용해서 결과를 배출해야 한다면:</dt>
    <dd><a href="operators/scan.html">Scan</a></dd>
  </dl></dd>

 <dt>Observable이 배출한 전체 항목들을 특정 자료구조로 배출하고 싶다면</dt>
  <dd><a href="operators/to.html">To</a></dd>

 <dt>연산자가 특정 <a href="../scheduler.html">스케줄러</a> 상에서 동작해야 한다면:</dt>
  <dd><a href="operators/subscribeon.html">SubscribeOn</a></dd>
  <dd class="sub"><dl>
   <dt>연산자가 옵저버한테 알림을 줄 때 동작할 스케줄러를 지정해야 한다면:</dt>
    <dd><a href="operators/observeon.html">ObserveOn</a></dd>
  </dl></dd>

 <dt>특정 이벤트가 발생 할 때 Observable 상에서 어떤 동작을 실행시켜야 한다면:</dt>
  <dd><a href="operators/do.html">Do</a></dd>

 <dt>오류가 발생했을 때 Observable이 옵저버에게 오류를 알려야 하다면:</dt>
  <dd><a href="operators/empty-never-throw.html">Throw</a></dd>
  <dd class="sub"><dl>
   <dt>만약 항목이 배출되지 않은 상태에서 특정 시간이 경과했다면</dt>
    <dd><a href="operators/timeout.html">Timeout</a></dd>
  </dl></dd>

 <dt>자연스럽게 Observable을 복구해야 하는데</dt>
  <dd class="sub"><dl>
   <dt>타임 아웃이 발생한 경우 백업 Observable로 전환시켜 복구해야 한다면:</dt>
    <dd><a href="operators/timeout.html">Timeout</a></dd>
   <dt>앞에서 발생한 오류 알림으로부터 복구해야 한다면:</dt>
    <dd><a href="operators/catch.html">Catch</a></dd>
    <dd class="sub"><dl>
     <dt>이전 Observable에 재구독을 시도해야 한다면:</dt>
      <dd><a href="operators/retry.html">Retry</a></dd>
    </dl></dd>
  </dl></dd>

 <dt>동일한 생명주기를 가진 리소스를 Observable로 생성해야 한다면:</dt>
  <dd><a href="operators/using.html">Using</a></dd>

 <dt>Observable을 구독하고 Observable이 완료될 때까지 블로킹 상태에 있는 <code>퓨처(Future)</code>를 전달 받고 싶다면:</dt>
  <dd><a href="operators/start.html">Start</a></dd>

 <dt>구독자의 요청 전까지 Observable이 항목을 구독자에게 배포하지 말아야 한다면:</dt>
  <dd><a href="operators/publish.html">Publish</a></dd>
  <dd class="sub"><dl>
   <dt>그리고 맨 마지막 항목만을 배출해야 한다면:</dt>
    <dd><a href="operators/publish.html">PublishLast</a></dd>
   <dt>그리고 배출 이후에 구독자가 구독을 시작했다 하더라고 동일하게 배출 순서를 전달해야 한다면:</dt>
    <dd><a href="operators/replay.html">Replay</a></dd>
   <dt>하지만 모든 구독자가 한번에 구독을 해지할 수 있어야 한다면:</dt>
    <dd><a href="operators/refcount.html">RefCount</a></dd>
   <dt>그리고 배출을 시작하도록 Observable에게 요청해야 한다면:</dt>
    <dd><a href="operators/connect.html">Connect</a></dd>
  </dl></dd>
</dl>
</div>
<h4 style="clear:both;">참고</h4>
<ul>
 <li><a href="http://xgrommx.github.io/rx-book/content/which_operator_do_i_use/index.html">Which Operator do I use?</a> by Dennis Stoyanov (a similar decision tree, specific to RxJS operators)</li>
</ul>

<h1 id="alphabetical" style="clear: left;">Observable 연산자 리스트(알파벳순)</h1>

표준 연산자나 핵심 연산자의 이름은 **boldface**로 표시했다. 그 외 연산자들은 언어 별로 구현된 다양한 연산자들을 포함하거나 ReactiveX의 주요 연산자 이외의 특별한 연산자들을 포함한다.

* [`Aggregate`]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [**`All`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html)
* [**`Amb`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/amb.html)
* [`and_`]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html)
* [**`And`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html)
* [`Any`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`apply`]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`as_blocking`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`asObservable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`AssertEqual`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sequenceequal.html)
* [`asyncAction`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [`asyncFunc`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [**`Average`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html)
* [`averageDouble`]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html)
* [`averageFloat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html)
* [`averageInteger`]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html)
* [`averageLong`]({{ site.url }}{{ site.baseurl }}/documentation/operators/average.html)
* [`blocking`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [**`Buffer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`bufferWithCount`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`bufferWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`bufferWithTimeOrCount`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`byLine`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`cache`]({{ site.url }}{{ site.baseurl }}/documentation/operators/replay.html)
* [`case`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html)
* [`Cast`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [**`Catch`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`catchError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`catchException`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`collect`]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [`collect`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html) (RxScala version of **`Filter`**)
* [**`CombineLatest`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/combinelatest.html)
* [`combineLatestWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/combinelatest.html)
* [**`Concat`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/concat.html)
* [`concat_all`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`concatMap`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`concatMapObserver`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`concatMapTo`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`concatAll`]({{ site.url }}{{ site.baseurl }}/documentation/operators/concat.html)
* [`concatWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/concat.html)
* [**`Connect`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/connect.html)
* [`connect_forever`]({{ site.url }}{{ site.baseurl }}/documentation/operators/connect.html)
* [`cons`]({{ site.url }}{{ site.baseurl }}/documentation/operators/startwith.html)
* [**`Contains`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`controlled`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [**`Count`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html)
* [`countLong`]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html)
* [**`Create`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`cycle`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [**`Debounce`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/debounce.html)
* [`decode`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [**`DefaultIfEmpty`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/defaultifempty.html)
* [**`Defer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html)
* [`deferFuture`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [**`Delay`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/delay.html)
* [`delaySubscription`]({{ site.url }}{{ site.baseurl }}/documentation/operators/delay.html)
* [`delayWithSelector`]({{ site.url }}{{ site.baseurl }}/documentation/operators/delay.html)
* [**`Dematerialize`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/materialize-dematerialize.html)
* [**`Distinct`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/distinct.html)
* [`distinctKey`]({{ site.url }}{{ site.baseurl }}/documentation/operators/distinct.html)
* [`distinctUntilChanged`]({{ site.url }}{{ site.baseurl }}/documentation/operators/distinct.html)
* [`distinctUntilKeyChanged`]({{ site.url }}{{ site.baseurl }}/documentation/operators/distinct.html)
* [**`Do`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doAction`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doAfterTerminate`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnCompleted`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnEach`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnRequest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnSubscribe`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnTerminate`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doOnUnsubscribe`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`doseq`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [`doWhile`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [`drop`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skip.html)
* [`dropRight`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skiplast.html)
* [`dropUntil`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipuntil.html)
* [`dropWhile`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipwhile.html)
* [**`ElementAt`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/elementat.html)
* [`ElementAtOrDefault`]({{ site.url }}{{ site.baseurl }}/documentation/operators/elementat.html)
* [**`Empty`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`emptyObservable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`empty?`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`encode`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`ensures`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`error`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`every`]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html)
* [`exclusive`]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html)
* [`exists`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`expand`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`failWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [**`Filter`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`filterNot`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`Finally`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`finallyAction`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`finallyDo`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`find`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`findIndex`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [**`First`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`FirstOrDefault`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`firstOrElse`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [**`FlatMap`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapFirst`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapIterable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapIterableWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapLatest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapObserver`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatMapWithMaxConcurrent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flat_map_with_index`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`flatten`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`flattenDelayError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`foldl`]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [`foldLeft`]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [`for`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`forall`]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html)
* [`ForEach`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [`forEachFuture`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [`forIn`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`forkJoin`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html)
* [**`From`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromAction`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromArray`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`FromAsyncPattern`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromCallable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromCallback`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`FromEvent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`FromEventPattern`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromFunc0`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`from_future`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`from_iterable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromIterator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`from_list`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromNodeCallback`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromPromise`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`fromRunnable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`Generate`]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`generateWithAbsoluteTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`generateWithRelativeTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`generator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/create.html)
* [`GetEnumerator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`getIterator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [**`GroupBy`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/groupby.html)
* [`GroupByUntil`]({{ site.url }}{{ site.baseurl }}/documentation/operators/groupby.html)
* [`GroupJoin`]({{ site.url }}{{ site.baseurl }}/documentation/operators/join.html)
* [`head`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`headOption`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`headOrElse`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`if`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html)
* [`ifThen`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html)
* [**`IgnoreElements`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/ignoreelements.html)
* [`indexOf`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`interleave`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`interpose`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [**`Interval`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/interval.html)
* [`into`]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [`isEmpty`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`items`]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
* [**`Join`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/join.html)
* [`join`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html) (string)
* [`jortSort`]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html)
* [`jortSortUntil`]({{ site.url }}{{ site.baseurl }}/documentation/operators/all.html)
* [**`Just`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
* [`keep`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`keep-indexed`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [**`Last`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html)
* [`lastOption`]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html)
* [`LastOrDefault`]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html)
* [`lastOrElse`]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html)
* [`Latest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`latest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html) (Rx.rb version of **`Switch`**)
* [`length`]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html)
* [`let`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`letBind`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`limit`]({{ site.url }}{{ site.baseurl }}/documentation/operators/take.html)
* [`LongCount`]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html)
* [`ManySelect`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [**`Map`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`map`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html) (RxClojure version of **`Zip`**)
* [`MapCat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`mapCat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html) (RxClojure version of **`Zip`**)
* [`map-indexed`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`mapTo`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`mapWithIndex`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [**`Materialize`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/materialize-dematerialize.html)
* [**`Max`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/max.html)
* [`MaxBy`]({{ site.url }}{{ site.baseurl }}/documentation/operators/max.html)
* [**`Merge`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`mergeAll`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`merge_concurrent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`mergeDelayError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`mergeObservable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [`mergeWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/merge.html)
* [**`Min`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/min.html)
* [`MinBy`]({{ site.url }}{{ site.baseurl }}/documentation/operators/min.html)
* [`MostRecent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`Multicast`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`multicastWithSelector`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`nest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [**`Never`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`Next`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`Next`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html) (BlockingObservable version)
* [`none`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`nonEmpty`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`nth`]({{ site.url }}{{ site.baseurl }}/documentation/operators/elementat.html)
* [**`ObserveOn`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/observeon.html)
* [`ObserveOnDispatcher`]({{ site.url }}{{ site.baseurl }}/documentation/operators/observeon.html)
* [`observeSingleOn`]({{ site.url }}{{ site.baseurl }}/documentation/operators/observeon.html)
* [`of`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`of_array`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`ofArrayChanges`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`of_enumerable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`of_enumerator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`ofObjectChanges`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`OfType`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`ofWithScheduler`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`onBackpressureBlock`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`onBackpressureBuffer`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`onBackpressureDrop`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`OnErrorResumeNext`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`onErrorReturn`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`onExceptionResumeNext`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`orElse`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defaultifempty.html)
* [`pairs`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`pairwise`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`partition`]({{ site.url }}{{ site.baseurl }}/documentation/operators/groupby.html)
* [`partition-all`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`pausable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`pausableBuffered`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`pluck`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html)
* [`product`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [**`Publish`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`PublishLast`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`publish_synchronized`]({{ site.url }}{{ site.baseurl }}/documentation/operators/replay.html)
* [`publishValue`]({{ site.url }}{{ site.baseurl }}/documentation/operators/publish.html)
* [`raise_error`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [**`Range`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/range.html)
* [**`Reduce`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/reduce.html)
* [`reductions`]({{ site.url }}{{ site.baseurl }}/documentation/operators/scan.html)
* [**`RefCount`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/refcount.html)
* [**`Repeat`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [`repeat_infinitely`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [`repeatWhen`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [**`Replay`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/replay.html)
* [`rescue_error`]({{ site.url }}{{ site.baseurl }}/documentation/operators/catch.html)
* [`rest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [**`Retry`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/retry.html)
* [`retry_infinitely`]({{ site.url }}{{ site.baseurl }}/documentation/operators/retry.html)
* [`retryWhen`]({{ site.url }}{{ site.baseurl }}/documentation/operators/retry.html)
* [`Return`]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
* [`returnElement`]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
* [`returnValue`]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
* [`runAsync`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [**`Sample`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sample.html)
* [**`Scan`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/scan.html)
* [`scope`]({{ site.url }}{{ site.baseurl }}/documentation/operators/using.html)
* [`Select`]({{ site.url }}{{ site.baseurl }}/documentation/operators/map.html) (alternate name of **`Map`**)
* [`select`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html) (alternate name of **`Filter`**)
* [`selectConcat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`selectConcatObserver`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`SelectMany`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`selectManyObserver`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`select_switch`]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html)
* [`selectSwitch`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`selectSwitchFirst`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`selectWithMaxConcurrent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`select_with_index`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`seq`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [**`SequenceEqual`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sequenceequal.html)
* [`sequence_eql?`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sequenceequal.html)
* [`SequenceEqualWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sequenceequal.html)
* [**`Serialize`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/serialize.html)
* [`share`]({{ site.url }}{{ site.baseurl }}/documentation/operators/refcount.html)
* [`shareReplay`]({{ site.url }}{{ site.baseurl }}/documentation/operators/replay.html)
* [`shareValue`]({{ site.url }}{{ site.baseurl }}/documentation/operators/refcount.html)
* [`Single`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`SingleOrDefault`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`singleOption`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`singleOrElse`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [`size`]({{ site.url }}{{ site.baseurl }}/documentation/operators/count.html)
* [**`Skip`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skip.html)
* [**`SkipLast`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skiplast.html)
* [`skipLastWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skiplast.html)
* [**`SkipUntil`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipuntil.html)
* [`skipUntilWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipuntil.html)
* [**`SkipWhile`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipwhile.html)
* [`skipWhileWithIndex`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skipwhile.html)
* [`skip_with_time`]({{ site.url }}{{ site.baseurl }}/documentation/operators/skip.html)
* [`slice`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`sliding`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`slidingBuffer`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`some`]({{ site.url }}{{ site.baseurl }}/documentation/operators/contains.html)
* [`sort`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`sort-by`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`sorted-list-by`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`split`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`split-with`]({{ site.url }}{{ site.baseurl }}/documentation/operators/groupby.html)
* [**`Start`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [`startAsync`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [`startFuture`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [**`StartWith`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/startwith.html)
* [`startWithArray`]({{ site.url }}{{ site.baseurl }}/documentation/operators/startwith.html)
* [`stringConcat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [`stopAndWait`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`subscribe`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [**`SubscribeOn`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribeon.html)
* [`SubscribeOnDispatcher`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribeon.html)
* [`subscribeOnCompleted`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [`subscribeOnError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [`subscribeOnNext`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribe.html)
* [**`Sum`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [`sumDouble`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [`sumFloat`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [`sumInteger`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [`sumLong`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sum.html)
* [**`Switch`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html)
* [`switchCase`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defer.html)
* [`switchIfEmpty`]({{ site.url }}{{ site.baseurl }}/documentation/operators/defaultifempty.html)
* [`switchLatest`]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html)
* [`switchMap`]({{ site.url }}{{ site.baseurl }}/documentation/operators/flatmap.html)
* [`switchOnNext`]({{ site.url }}{{ site.baseurl }}/documentation/operators/switch.html)
* [`Synchronize`]({{ site.url }}{{ site.baseurl }}/documentation/operators/serialize.html)
* [**`Take`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/take.html)
* [`take_with_time`]({{ site.url }}{{ site.baseurl }}/documentation/operators/take.html)
* [`takeFirst`]({{ site.url }}{{ site.baseurl }}/documentation/operators/first.html)
* [**`TakeLast`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`takeLastBuffer`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`takeLastBufferWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`takeLastWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`takeRight`]({{ site.url }}{{ site.baseurl }}/documentation/operators/last.html) (see also: [**`TakeLast`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html))
* [**`TakeUntil`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takeuntil.html)
* [`takeUntilWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takeuntil.html)
* [**`TakeWhile`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/takewhile.html)
* [`takeWhileWithIndex`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takewhile.html)
* [`tail`]({{ site.url }}{{ site.baseurl }}/documentation/operators/takelast.html)
* [`tap`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`tapOnCompleted`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`tapOnError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [`tapOnNext`]({{ site.url }}{{ site.baseurl }}/documentation/operators/do.html)
* [**`Then`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html)
* [`thenDo`]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html)
* [`Throttle`]({{ site.url }}{{ site.baseurl }}/documentation/operators/debounce.html)
* [`throttleFirst`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sample.html)
* [`throttleLast`]({{ site.url }}{{ site.baseurl }}/documentation/operators/sample.html)
* [`throttleWithSelector`]({{ site.url }}{{ site.baseurl }}/documentation/operators/debounce.html)
* [`throttleWithTimeout`]({{ site.url }}{{ site.baseurl }}/documentation/operators/debounce.html)
* [**`Throw`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`throwError`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [`throwException`]({{ site.url }}{{ site.baseurl }}/documentation/operators/empty-never-throw.html)
* [**`TimeInterval`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timeinterval.html)
* [**`Timeout`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timeout.html)
* [`timeoutWithSelector`]({{ site.url }}{{ site.baseurl }}/documentation/operators/timeout.html)
* [**`Timer`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timer.html)
* [**`Timestamp`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/timestamp.html)
* [**`To`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`to_a`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToArray`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToAsync`]({{ site.url }}{{ site.baseurl }}/documentation/operators/start.html)
* [`toBlocking`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toBuffer`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`to_dict`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToDictionary`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToEnumerable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToEvent`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToEventPattern`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToFuture`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`to_h`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toIndexedSeq`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toIterable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toIterator`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToList`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToLookup`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toMap`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toMultiMap`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToObservable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/from.html)
* [`toSet`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toSortedList`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toStream`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`ToTask`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toTraversable`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`toVector`]({{ site.url }}{{ site.baseurl }}/documentation/operators/to.html)
* [`tumbling`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`tumblingBuffer`]({{ site.url }}{{ site.baseurl }}/documentation/operators/buffer.html)
* [`unsubscribeOn`]({{ site.url }}{{ site.baseurl }}/documentation/operators/subscribeon.html)
* [**`Using`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/using.html)
* [**`When`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/and-then-when.html)
* [`Where`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`while`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [`whileDo`]({{ site.url }}{{ site.baseurl }}/documentation/operators/repeat.html)
* [**`Window`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`windowWithCount`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`windowWithTime`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`windowWithTimeOrCount`]({{ site.url }}{{ site.baseurl }}/documentation/operators/window.html)
* [`windowed`]({{ site.url }}{{ site.baseurl }}/documentation/operators/backpressure.html)
* [`withFilter`]({{ site.url }}{{ site.baseurl }}/documentation/operators/filter.html)
* [`withLatestFrom`]({{ site.url }}{{ site.baseurl }}/documentation/operators/combinelatest.html)
* [**`Zip`**]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html)
* [`zipArray`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html)
* [`zipWith`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html)
* [`zipWithIndex`]({{ site.url }}{{ site.baseurl }}/documentation/operators/zip.html)
* [`++`]({{ site.url }}{{ site.baseurl }}/documentation/operators/concat.html)
* [`+:`]({{ site.url }}{{ site.baseurl }}/documentation/operators/startwith.html)
* [`:+`]({{ site.url }}{{ site.baseurl }}/documentation/operators/just.html)
