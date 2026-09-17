# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-17T20:20:01.842332+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×51 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×56 (24h)
- 🔴 PSI_DRIFT_DETECTED×51 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×7 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×22  [2026-09-17T20:09:09]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×11  [2026-09-17T20:09:09]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-09-17T20:09:09]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×34  [2026-09-17T19:46:26]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-17T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-17T19:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-09-17T17:18:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-17T06:00:22]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-17T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-17T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S00: n=178 hit%=27.5% hit_CI[Bonf]=[19.0,38.0]% ROI=0.96 ROI_boot95=[0.69,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=176 hit%=23.9% hit_CI[Bonf]=[15.9,34.2]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=35.1% hit_CI[Bonf]=[21.5,51.5]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.85 (コスト 9,200/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.73 (コスト 10,300/回収 7,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=22.1% ROI=0.85 (コスト 19,800/回収 16,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=21.3% ROI=0.43 (コスト 10,300/回収 4,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.46MB / last modified 2026-09-17T20:19:21.679289+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-17 20:18:27,241 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=15&hd=20260917: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-17 20:18:40,769 [INFO] scraper: odds3t: 120/120 parsed
2026-09-17 20:18:41,887 [INFO] scraper: odds3f: 20/20 parsed
2026-09-17 20:18:43,007 [INFO] scraper: odds2t: 30/30 parsed
2026-09-17 20:18:43,009 [INFO] scraper: odds2f: 15/15 parsed
2026-09-17 20:18:44,098 [INFO] scraper: odds_win: 5/6 parsed
2026-09-17 20:18:44,098 [INFO] scraper: fetch_race 15/12: boats=6 odds=190/191
2026-09-17 20:18:44,102 [INFO] predictor: CALIBRATION_MODE=on
2026-09-17 20:18:44,102 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-17 20:18:44,106 [INFO] run_cycle: fetched 15/12 [scan]: 155 combos
2026-09-17 20:18:44,259 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-17 20:19:05,114 [INFO] run_cycle: === run_cycle 20:19:05 ===
2026-09-17 20:19:05,115 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-17 20:19:05,115 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-17 20:19:05,184 [INFO] predictor: Models loaded OK
2026-09-17 20:19:17,649 [INFO] scraper: odds3t: 120/120 parsed
2026-09-17 20:19:18,773 [INFO] scraper: odds3f: 20/20 parsed
2026-09-17 20:19:19,979 [INFO] scraper: odds2t: 30/30 parsed
2026-09-17 20:19:19,980 [INFO] scraper: odds2f: 14/15 parsed
2026-09-17 20:19:21,087 [INFO] scraper: odds_win: 6/6 parsed
2026-09-17 20:19:21,087 [INFO] scraper: fetch_race 24/7: boats=6 odds=190/191
2026-09-17 20:19:21,091 [INFO] predictor: CALIBRATION_MODE=on
2026-09-17 20:19:21,091 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-17 20:19:21,095 [INFO] run_cycle: fetched 24/7 [scan]: 156 combos
2026-09-17 20:19:21,308 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 70
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 70
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 11, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 56
  PSI_DRIFT_DETECTED: 51
  ANOMALY_SCRAPER_FAILURE_BURST: 34
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 7
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 7 | 11,100 | 7,110 | -3,990 | 0.641 |
| S01_NAKAANA1 | 31 | 9 | 6,200 | 5,760 | -440 | 0.929 |
| S02_TETSUBAN | 13 | 7 | 2,600 | 2,880 | +280 | 1.108 |

## 直近アラート (24h・新しい順)
```
[20:14:24] FINAL_MISSING: {"deadline": "2026-09-17T15:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091709111541", "sid": "S00"}
[20:09:04] FINAL_MISSING: {"deadline": "2026-09-17T13:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091708071336", "sid": "S00"}
[20:07:27] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[20:07:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[20:07:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[19:57:31] FINAL_MISSING: {"deadline": "2026-09-17T11:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091704021123", "sid": "S00"}
[19:51:20] FINAL_MISSING: {"deadline": "2026-09-17T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091714051016", "sid": "S00"}
[19:43:31] FINAL_MISSING: {"deadline": "2026-09-17T16:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091715031610", "sid": "S00"}
[19:39:05] FINAL_MISSING: {"deadline": "2026-09-17T18:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091724021808", "sid": "S00"}
[19:33:20] FINAL_MISSING: {"deadline": "2026-09-17T17:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091715051701", "sid": "S00"}
```

## 本日残レース: 9件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 171件 締切済
- 通知発射: scan=24 nid / final=26 nid / result=11 nid
- predictions: 11 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 245R | win | 1 | 0.4989 | 5.3 | 2.64 | 300 | scan=- drift=- | 19:28:31 |
| S01_NAKAANA1 | 242R | win | 1 | 0.5334 | 4.0 | 2.13 | 200 | scan=4.6 drift=-13.0% | 18:05:31 |
| S00 | 154R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=6.7 drift=+0.0% | 16:33:20 |
| S02_TETSUBAN | 057R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=- drift=- | 13:27:21 |
| S02_TETSUBAN | 117R | win | 1 | 0.5612 | 2.0 | 1.12 | 200 | scan=- drift=- | 13:19:20 |
| S00 | 165R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 12:49:21 |
| S00 | 222R | win | 1 | 0.5174 | 7.5 | 3.88 | 300 | scan=7.5 drift=+0.0% | 12:11:20 |
| S00 | 114R | win | 1 | 0.5334 | 13.5 | 7.20 | 300 | scan=- drift=- | 11:47:30 |
| S00 | 113R | win | 1 | 0.0754 | 5.6 | 0.42 | 300 | scan=7.5 drift=-25.3% | 11:19:18 |
| S02_TETSUBAN | 092R | win | 1 | 0.5460 | 2.2 | 1.20 | 200 | scan=2.0 drift=+10.0% | 10:58:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +5.6% | -80.2% | +119.5% | 13 | 2 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 444.1s |
| **Latency** (scan→final max) | 612.3s |
| **Traffic** (notifications 24h) | 70 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 423 | 0.4779 | 0.2695 | +0.2084 | 🟡+44% | 0.2419 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4391 | 0.2500 | 0.2304 | 🔴-0.23 | 0.815 |
| S01_NAKAANA1 | win | 170 | 0.4874 | 0.2353 | 0.2444 | 🔴-0.36 | 0.658 |
| S02_TETSUBAN | win | 77 | 0.5455 | 0.3896 | 0.2628 | 🔴-0.11 | 0.732 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 6 | 0.2221 | 0.0000 | 🔴+0.2221 |
| 0.30-0.50 | 145 | 0.4105 | 0.2138 | 🔴+0.1967 |
| 0.50+ | 255 | 0.5454 | 0.3098 | 🔴+0.2356 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 142 | 0.777 |
| win | <5.0 | ✅learned | 254 | 0.757 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 33 | 0.234 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-17T20:20:01.842332+09:00_