# Anti-patterns

Short failure examples for Institutional Forensics.

## Anti-pattern 1 — Explaining an unverified premise

### BAD

```text
楠上第二住宅2号棟は、中高層建物の棟番号特例によって2-1-2になった。
```

### Why it fails

- 個別の付番記録を確認していない
- 「2号棟の正式住居番号が2-1-2」という前提自体が未確定
- 制度上可能であることを、個別適用の証拠にしている

### GOOD

```text
棟番号特例で説明できる可能性はある。
ただし個別付番記録が未確認なので、現時点の結論はUnresolved。
```

---

## Anti-pattern 2 — Reading only the base contract

### BAD

```text
基本約款に200GB制限がない。したがって完全無制限。
```

### Why it fails

- 数値条件が料金表・提供条件書・重要事項説明にある可能性を無視
- 「無制限」が容量、速度、料金、テザリング等のどのdimensionを指すか未分解

### GOOD

```text
Document Stackを確認し、固定容量閾値、速度制御、混雑制御、テザリングを別dimensionで評価する。
```

---

## Anti-pattern 3 — Official equals same weight

### BAD

```text
どちらも公式ページなので、両方とも同じ重みで契約条件を示している。
```

### Why it fails

商品ページと約款ではDocument Functionが違う。

### GOOD

各Sourceについて `issuer / function / object_level / valid_at / source` を確認する。

---

## Anti-pattern 4 — Label-to-label comparison

### BAD

```text
A社もB社も「無制限」なので同じ条件。
```

### GOOD

```text
volume / high-speed volume / throttling / window / tethering / geography
```

へ分解して比較する。

---

## Anti-pattern 5 — Overconfident negative claim

### BAD

```text
売買には「1年」という期間規定は存在しない。
```

### Why it fails

- 誤った通説を否定するための代替説明を、再度Premise Validationしていない
- `存在しない / 一度もない / only / 唯一` は強い否定命題なのに、法令全文や隣接条文を確認していない
- 実際には民法566条に、種類・品質の契約不適合を知った時から1年以内の通知期間がある

### GOOD

```text
「購入日から1年間の一律メーカー保証義務」は確認できない。
ただし、売買には民法566条の1年通知期間が存在する。
通知期間・消滅時効・商用保証期間を分離する。
```

---

## Anti-pattern 6 — Promoting current state to permanence

### BAD

```text
2021年6月1日前のGoogle Photosバックアップは永久に容量カウント対象外で、永久保存される。
```

### Why it fails

- 現行ポリシーの状態を将来不変の保証へ昇格している
- `quota_counting` と `retention_policy` を混同している

### GOOD

```text
現行ポリシーでは対象バックアップは容量にカウントされない。
将来不変か、永久保持されるかは別dimensionであり、明示的な保証がなければ断定しない。
```
