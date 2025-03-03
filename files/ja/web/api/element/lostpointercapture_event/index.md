---
title: "Element: lostpointercapture イベント"
short-title: lostpointercapture
slug: Web/API/Element/lostpointercapture_event
original_slug: Web/API/GlobalEventHandlers/onlostpointercapture
l10n:
  sourceCommit: 7b3ccaec4a93584da12939587ea746acaabe30bc
---

{{APIRef}}

**`lostpointercapture`** イベントは、[キャプチャされたポインター](/ja/docs/Web/API/Pointer_events#pointer_capture)が解放されたときに発生します。

## 構文

このイベント名を {{domxref("EventTarget.addEventListener", "addEventListener()")}} などのメソッドで使用するか、イベントハンドラープロパティを設定するかしてください。

```js
addEventListener("lostpointercapture", (event) => {});

onlostpointercapture = (event) => {};
```

## イベント型

{{domxref("PointerEvent")}} です。 {{domxref("Event")}} を継承しています。

{{InheritanceDiagram("PointerEvent")}}

## イベントプロパティ

_このインターフェイスは {{domxref("MouseEvent")}} および {{domxref("Event")}} からプロパティを継承しています。_

- {{ domxref('PointerEvent.pointerId')}} {{ReadOnlyInline}}
  - : イベントを発生させたポインターの固有の識別子です。
- {{ domxref('PointerEvent.width')}} {{ReadOnlyInline}}
  - : ポインターが接触するジオメトリーの幅（X 軸の大きさ、CSS ピクセル単位）。
- {{ domxref('PointerEvent.height')}} {{ReadOnlyInline}}
  - : ポインターが接触するジオメトリーの高さ（Y 軸の大きさ、CSS ピクセル単位）。
- {{ domxref('PointerEvent.pressure')}} {{ReadOnlyInline}}
  - : ポインター入力の正規化された圧力で、範囲は `0` から `1` です。ここで `0` と `1` は、それぞれハードウェアが検出可能な最小圧力と最大圧力を表します。
- {{ domxref('PointerEvent.tangentialPressure')}} {{ReadOnlyInline}}
  - : ポインタ入力の正規化された接線圧力（バレル圧力またはシリンダー応力（[cylinder stress](https://en.wikipedia.org/wiki/Cylinder_stress)）とも呼ばれます）で、 `-1` から `1` の範囲であり、 `0` はコントロールの中立位置です。
- {{ domxref('PointerEvent.tiltX')}} {{ReadOnlyInline}}
  - : Y-Z 平面と、ポインター（ペンスタイラスなど）の軸と Y 軸の両方を含む平面との間の平面角度（度単位、 `-90` から `90` の範囲）。
- {{ domxref('PointerEvent.tiltY')}} {{ReadOnlyInline}}
  - : X-Z 平面と、ポインター（ペンスタイラスなど）の軸と X 軸の両方を含む平面との間の平面角度（度単位、 `-90` から `90` の範囲）。
- {{ domxref('PointerEvent.twist')}} {{ReadOnlyInline}}
  - : ポインター（ペンスタイラスなど）の長軸を中心とした時計回りの回転の度数（`0` から `359` の範囲の値）。
- {{ domxref('PointerEvent.pointerType')}} {{ReadOnlyInline}}
  - : イベントの原因となった機器の種類（マウス、ペン、タッチなど）を示します。
- {{ domxref('PointerEvent.isPrimary')}} {{ReadOnlyInline}}
  - : このポインターがこのポインター種別の主ポインターを表すかどうかを示します。

## 例

この例は要素で `lostpointercapture` イベントを待ち受けし、その要素の `pointerdown` でポインターをキャプチャします。その後でユーザーがポインターを開放すると、 `lostpointercapture` が発生します。

```js
const para = document.querySelector("p");

para.addEventListener("lostpointercapture", () => {
  console.log("I've been released!");
});

para.addEventListener("pointerdown", (event) => {
  para.setPointerCapture(event.pointerId);
});
```

同じ例ですが、 `onlostpointercapture` イベントハンドラーを使用して行います。

```js
const para = document.querySelector("p");

para.onlostpointercapture = () => {
  console.log("I've been released!");
};

para.addEventListener("pointerdown", (event) => {
  para.setPointerCapture(event.pointerId);
});
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- 関連イベント

  - [`gotpointercapture`](/ja/docs/Web/API/Element/gotpointercapture_event)
  - [`pointerover`](/ja/docs/Web/API/Element/pointerover_event)
  - [`pointerenter`](/ja/docs/Web/API/Element/pointerenter_event)
  - [`pointerdown`](/ja/docs/Web/API/Element/pointerdown_event)
  - [`pointermove`](/ja/docs/Web/API/Element/pointermove_event)
  - [`pointerup`](/ja/docs/Web/API/Element/pointerup_event)
  - [`pointercancel`](/ja/docs/Web/API/Element/pointercancel_event)
  - [`pointerout`](/ja/docs/Web/API/Element/pointerout_event)
  - [`pointerleave`](/ja/docs/Web/API/Element/pointerleave_event)
