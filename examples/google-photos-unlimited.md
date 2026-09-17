# Case Study: Google Photos「無制限ストレージ」の日落とコホート併存

Status: corrected verified case / device-detail matrix partly unresolved  
Skill: `institutional-forensics`  
Primary mechanisms: Premise / Claim Dimensions / Scope / Cohort / Legacy / Timeline / Source Drift

## Premise status

**Cohort-dependent.**

検証対象の通説:

```text
Google Photosのストレージは「無制限」である
（あるいは「無制限だった」）
```

現行のGoogle公式ヘルプでは、同じGoogle Photosでもコホートごとに異なる扱いが併存している。

```text
一般アカウント
→ Googleアカウント全体で最大15GBの共有保存容量

2021-06-01より前に
高画質 / エクスプレス画質でバックアップした写真・動画
→ 現行ポリシー上、Googleアカウント保存容量にカウントされない

Pixel 5以前のGoogle Pixel
→ そのデバイスから無制限ストレージに無料でバックアップできる、と現行ヘルプが案内
```

したがって、「無制限は終わった」「無制限は今もある」のどちらも、コホートと条件を指定しなければ粗すぎる。

Confidence: **Confirmed for the cohort split stated by the current official help.**

---

## Important correction from the previous version

旧版は、2021年6月1日より前の対象バックアップについて

```text
永久に容量カウント対象外
恒久除外
```

と表現していた。

これは一次資料より強い。

Googleの現行文言から直接確認できるのは、

```text
2021年6月1日より前に対象画質でバックアップした写真・動画は、
現在のルール上、Googleアカウントの保存容量にカウントされない
```

という状態である。

そこから

```text
将来も絶対に変更されない
永久に保持される
```

まで推論してはいけない。

特にGoogleは同じヘルプ体系で、長期間の非アクティブや保存容量条件によってコンテンツが削除される可能性についても説明している。

したがって、

```text
quota exemption
!=
permanent retention guarantee
```

である。

---

## Claim Dimensions

「無料」「無制限」「残る」を一つの次元として扱わない。

```text
account_quota          アカウント保存容量の総枠
quota_counting         個々の写真・動画が容量計算に入るか
upload_entitlement     特定端末から無制限アップロードできるか
backup_quality         元の画質 / 保存容量の節約画質等
upload_date            いつバックアップされたか
device_cohort          どのPixel世代か
retention_policy       コンテンツが保持される条件
activity_policy        非アクティブ時の扱い
```

特に、

```text
容量にカウントされない
!=
削除されないことが永久に保証される
```

---

## Governing evidence

### 現行の一般枠

Google公式ヘルプは、各Googleアカウントで最大15GBの保存容量を利用でき、その容量がGmail、Google Drive、Google Photosで共有されると説明している。

- issuer: Google
- function: explanatory / operational
- object_level: Google account storage policy
- valid_at: 2026-09-17
- source: https://support.google.com/photos/answer/10100180?hl=ja

このHelpページは公式一次情報だが、契約条項そのものと決めつけて `normative` と扱わない。

---

### 2021年6月1日前の対象バックアップ

同ページは、2021年6月1日より前に高画質またはエクスプレス画質でバックアップした写真・動画はGoogleアカウントの保存容量にカウントされない、と現行形で説明している。

確認できるのは**現在のquota-counting rule**であり、将来不変の永久保証ではない。

---

### Pixel 5以前

同ページは、Pixel 5以前のGoogle Pixelについて、そのデバイスから無制限ストレージに写真と動画を無料でバックアップできると説明している。

ただし、旧版は「Pixel 5以前」を一つの均一なコホートとして扱いすぎていた。

実際には、端末世代・バックアップ画質・時期によって条件が細分される可能性があるため、詳細比較を行う場合は次の粒度まで下げる必要がある。

```text
Pixel model
× backup quality
× upload date
```

本ケースでは、現行の概要ヘルプで直接確認できる範囲をConfirmedとし、Pixel各世代の詳細マトリクスは別途一次資料で確認するまで過剰に一般化しない。

---

## Timeline / Source Drift

```text
〜2021-05-31
一般ユーザーにも「高画質」等で容量カウントされない運用が存在

2021-06-01
一般の新規バックアップについて保存容量ポリシー変更

現行
一般枠は15GB共有
旧対象バックアップは現行ルール上カウント対象外
Pixel 5以前について無制限バックアップ案内が残る
```

旧マーケティングページや制度変更告知のURLは、現在のヘルプ構造から直接再現できないものがあるため、過去の広告表現を引用する場合はアーカイブ等で別途保全する。

---

## Current conclusion

### Confirmed

- 現行Google Photos Helpでは、一般アカウントの保存容量はGoogleアカウントの最大15GB共有枠として説明されている。
- 2021年6月1日より前に対象画質でバックアップした写真・動画は、現行ポリシー上Googleアカウント保存容量にカウントされない。
- Pixel 5以前について、現行ヘルプは無制限ストレージへの無料バックアップを案内している。
- 同じ「無制限」「無料」でも、account quota / quota counting / device entitlement / backup quality / upload date は別次元。

### Not confirmed

- 旧対象バックアップが「将来にわたり永久に」容量カウント除外され続けること。
- 容量カウント除外が「永久保持」を意味すること。
- Pixel 5以前のすべての世代・画質・期間が同一条件であること。

### Confidence

**Confirmed for the current cohort split; long-term permanence and detailed Pixel sub-cohorts remain Unresolved unless separately sourced.**

---

## Falsification

この結論を覆し得るもの:

1. Google公式の現行資料が、旧対象バックアップを保存容量へ再びカウントすると明示する。
2. Pixel 5以前の概要記述を具体化する公式資料が、特定世代について条件を否定・限定する。
3. 「容量カウント対象外」と「永久保持」を同義とする明示的なGoogleの保証文言が見つかる。

3が見つからない限り、quota exemptionからretention guaranteeを推論しない。

---

## Why this case matters

このケースは、制度フォレンジックに次の失敗モードを追加した。

```text
現行状態を確認する
↓
その状態を「永久」「恒久」に昇格する
↓
隣接する別dimension（保持・削除）まで保証されたと誤読する
```

必要なのは新しいSTEPではなく、Claim DimensionsとFalsificationを厳密に使うこと。

```text
current state
!=
permanent promise

quota exemption
!=
retention guarantee
```
