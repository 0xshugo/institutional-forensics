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
