# Case Study: 携帯4社の「ギガ無制限」は同じ意味か

Date checked: 2026-09-17 JST
Status: cross-domain validation sample
Skill: `institutional-forensics` + `modules/telecom-contracts.md`

## Question

携帯4社が「ギガ無制限」「データ使い放題」等を掲げている一方で、通信制御、速度制限、テザリング条件などが存在する。

これは「無制限」と矛盾するのか。それとも「無制限」が指す対象次元が異なるのか。

対象:

- NTTドコモ: ドコモ MAX
- KDDI/au: auバリューリンクプラン
- SoftBank: テイガク無制限
- 楽天モバイル: Rakuten最強プラン

## Premise status

**Established, but requires semantic decomposition.**

4社はいずれも公式ページで無制限系の表現を使用している。同時に条件付き通信制御を公式に開示している。

したがって、調査すべきなのは「無制限なのに制限がある」という単純矛盾ではなく、

```text
各社の「無制限」が
何の次元を
どのscopeで
どの条件まで
無制限としているか
```

である。

## Claim Dimensions

```text
billing_limit
volume_limit
high_speed_limit
speed_guarantee
throttling_trigger
throttled_speed
window
traffic_type
geography
network_condition
abuse_condition
```

## Current comparison

| Carrier / plan | Marketing claim | Fixed domestic threshold | Tethering / share | General control |
|---|---|---|---|---|
| Docomo MAX | ギガ無制限 | 商品ページ上、国内スマホ本体について固定GB閾値は明示せず | テザリングも無制限と案内。データプラス等は別条件 | 大量通信時など制限の場合あり。基本約款にも輻輳・大量通信等の制御条項 |
| au Value Link | データ容量使い放題 | 200GB/月超で最大5Mbps | テザリング等は通常プランで合計60GB（プラン種別により異なる） | 混雑時等の速度制限あり。約款に通信利用制限条項 |
| SoftBank Teigaku Unlimited | ギガ無制限 | 直近30日間300GB超で最大4.5Mbps | テザリングも同じデータ量計算・制御条件の対象 | 時間帯・機械的通信等の制御あり。約款に通信利用制限条項 |
| Rakuten Saikyo | ギガ無制限 / 高速データ無制限（国内） | 国内月間データ量に基本的な固定上限なし | プラン・サービスごとに確認 | 混雑時など公平なサービス提供のため速度制御の場合あり。約款に帯域・速度・大量通信制御条項 |

## Important observation

同じ「無制限」という日本語でも、4社の条件は同型ではない。

### Docomo

現行商品ページでは「ギガ無制限」としつつ「大量通信時などに通信制限がかかる場合」が明記される。テザリングページではドコモ MAXを「テザリングも無制限」と案内している。

つまり、固定GB閾値によるプラン容量上限と、ネットワーク運用上の通信制御は別概念として扱われている。

Sources:
- https://www.docomo.ne.jp/charge/docomo_max/
- https://www.docomo.ne.jp/service/tethering/
- https://www.docomo.ne.jp/corporate/disclosure/agreement/

### au

「データ容量使い放題」だが、現行auバリューリンクプランでは200GB/月超で最大5Mbps、テザリング・データシェアには別上限がある。

ここでは「使い放題」は通信停止や追加従量課金のないデータ利用と、常時同じ速度での利用を同義にしていない。

Sources:
- https://www.au.com/mobile/charge/smartphone/plan/auvaluelink/
- https://www.au.com/mobile/information/charge/plan/
- https://www.kddi.com/corporate/kddi/public/conditions/

### SoftBank

「ギガ無制限」を掲げる一方、直近30日間で300GB超の場合に最大4.5Mbpsへ制御することを同じ商品ページ上で明示している。月単位ではなくrolling 30-day windowなのも重要。

Sources:
- https://www.softbank.jp/mobile/price_plan/data/teigaku-museigen/
- https://www.softbank.jp/mobile/price_plan/
- https://www.softbank.jp/mobile/legal/articles/5g/

### Rakuten Mobile

Rakuten最強プランは国内の高速データ容量を無制限としており、FAQでも国内月間データ利用量に基本的な上限がないと説明している。一方、混雑時など公平なサービス提供のため速度制御する場合がある。

つまり「固定GB閾値なし」と「通信制御権限なし」は同義ではない。

Sources:
- https://network.mobile.rakuten.co.jp/fee/saikyo-plan/detail/
- https://network.mobile.rakuten.co.jp/faq/detail/10001119/
- https://network.mobile.rakuten.co.jp/terms/

## Document Stack finding

このケースは基本約款だけでは解けない。

```text
基本約款
→ 通信制御の一般権限

料金表 / 提供条件 / 重要事項説明
→ プラン固有の容量・速度・料金

商品ページ / FAQ
→ 現行プランの利用者向け表現と運用説明
```

したがって、制度フォレンジックのEvidence Classとは別に、**Document Function** を記録する必要がある。

## Working conclusion

Confidence: Confirmed for the structural finding.

4社の「無制限」は、**絶対的に一切の制限がないことを共通して意味しているわけではない**。

今回比較した現行プランでは、主に「所定scopeにおけるデータ容量または料金体系の上限」を表す一方、速度、混雑、公平制御、テザリング、海外、計測期間などは別条件として定義されている。

ただし「無制限」の具体的scopeは各社・各プランで異なるため、語だけで横並び比較してはいけない。

## What would falsify this conclusion

- 各社の契約文書に、商品表示より強い「いかなる条件でも速度・量を制限しない」とする条項が存在する
- 現行提供条件書が上記商品ページの条件を否定している
- 比較対象プラン・加入時期が異なり、別契約条件が適用される
