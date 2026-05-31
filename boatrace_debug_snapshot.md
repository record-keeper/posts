# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-31T16:20:01.743706+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×24 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×45 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-05-31T16:04:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-05-31T16:04:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-05-31T16:04:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-31T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-31T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-05-31T15:01:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-05-31T11:35:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-05-31T09:00:14]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-31T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-31T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-31T06:00:15]
- key: `ORPHAN_SCAN|231 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.05 (コスト 8,400/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S00: n=181 hit%=28.2% hit_CI[Bonf]=[19.7,38.6]% ROI=0.94 ROI_boot95=[0.68,1.23]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=110 hit%=31.8% hit_CI[Bonf]=[20.7,45.5]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=110<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=53 hit%=47.2% hit_CI[Bonf]=[29.1,66.0]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=53<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=30.0% ROI=0.85 (コスト 14,700/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=32.4% ROI=0.88 (コスト 16,200/回収 14,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.97MB / last modified 2026-05-31T16:19:22.232774+09:00

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
os
2026-05-31 16:18:37,446 [INFO] scraper: odds3t: 120/120 parsed
2026-05-31 16:18:38,549 [INFO] scraper: odds3f: 20/20 parsed
2026-05-31 16:18:39,668 [INFO] scraper: odds2t: 30/30 parsed
2026-05-31 16:18:39,669 [INFO] scraper: odds2f: 12/15 parsed
2026-05-31 16:18:40,733 [INFO] scraper: odds_win: 3/6 parsed
2026-05-31 16:18:40,733 [INFO] scraper: fetch_race 20/3: boats=6 odds=185/191
2026-05-31 16:18:40,741 [INFO] predictor: CALIBRATION_MODE=on
2026-05-31 16:18:40,741 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-31 16:18:40,749 [INFO] run_cycle: fetched 20/3 [scan]: 153 combos
2026-05-31 16:18:40,993 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-31 16:19:06,035 [INFO] run_cycle: === run_cycle 16:19:06 ===
2026-05-31 16:19:06,035 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-31 16:19:06,035 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-31 16:19:06,081 [INFO] predictor: Models loaded OK
2026-05-31 16:19:17,500 [INFO] scraper: odds3t: 120/120 parsed
2026-05-31 16:19:18,598 [INFO] scraper: odds3f: 20/20 parsed
2026-05-31 16:19:19,665 [INFO] scraper: odds2t: 30/30 parsed
2026-05-31 16:19:19,666 [INFO] scraper: odds2f: 15/15 parsed
2026-05-31 16:19:20,758 [INFO] scraper: odds_win: 4/6 parsed
2026-05-31 16:19:20,758 [INFO] scraper: fetch_race 15/3: boats=6 odds=189/191
2026-05-31 16:19:20,769 [INFO] predictor: CALIBRATION_MODE=on
2026-05-31 16:19:20,770 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-31 16:19:20,777 [INFO] run_cycle: fetched 15/3 [final]: 154 combos
2026-05-31 16:19:20,807 [INFO] race_id: notif: nid=2026053115031622 sid=S00 phase=final rank=S
2026-05-31 16:19:21,252 [INFO] notifier: Discord notify OK (status=204)
2026-05-31 16:19:21,630 [INFO] notifier: Discord notify OK (status=204)
2026-05-31 16:19:21,643 [INFO] run_cycle: FINAL S00 丸亀3R S
2026-05-31 16:19:22,112 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 11, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 70
  FINAL_MISSING: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 24
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 8
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 7 | 11,700 | 4,770 | -6,930 | 0.408 |
| S01_NAKAANA1 | 38 | 14 | 7,600 | 6,900 | -700 | 0.908 |
| S02_TETSUBAN | 13 | 5 | 2,600 | 2,240 | -360 | 0.862 |

## 直近アラート (24h・新しい順)
```
[16:19:22] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 4770, "roi_7d": 0.408, "sid": "S00"}
[16:07:35] FINAL_MISSING: {"deadline": "2026-05-31T14:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026053113091437", "sid": "S00"}
[16:04:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:04:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:04:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:42:35] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 4770, "roi_7d": 0.418, "sid": "S00"}
[15:31:21] FINAL_MISSING: {"deadline": "2026-05-31T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026053109041159", "sid": "S00"}
[15:27:20] FINAL_MISSING: {"deadline": "2026-05-31T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026053103071356", "sid": "S00"}
[15:25:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1208}
[15:24:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1213}
```

## 本日残レース: 57件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 135件 締切済
- 通知発射: scan=20 nid / final=22 nid / result=9 nid
- predictions: 12 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 153R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=7.5 drift=-20.0% | 16:19:20 |
| S02_TETSUBAN | 059R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.8 drift=-21.4% | 16:01:45 |
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 15:58:20 |
| S02_TETSUBAN | 0911R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=2.2 drift=+0.0% | 15:43:21 |
| S02_TETSUBAN | 058R | win | 1 | 0.5998 | 2.3 | 1.38 | 200 | scan=2.0 drift=+15.0% | 15:23:21 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.2 drift=+12.5% | 15:21:45 |
| S01_NAKAANA1 | 138R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.7 drift=-34.0% | 14:04:21 |
| S00 | 034R | win | 1 | 0.4920 | 5.2 | 2.56 | 300 | scan=4.5 drift=+15.6% | 12:32:28 |
| S00 | 149R | win | 1 | 0.5174 | 12.0 | 6.21 | 300 | scan=- drift=- | 12:29:32 |
| S00 | 132R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=- drift=- | 11:06:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +9.9% | -81.4% | +229.3% | 14 | 8 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 503.6s |
| **Latency** (scan→final max) | 646.4s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 348 | 0.4566 | 0.3218 | +0.1347 | 🟡+30% | 0.2363 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4222 | 0.2833 | 0.2240 | 🔴-0.10 | 0.912 |
| S01_NAKAANA1 | win | 113 | 0.4832 | 0.3186 | 0.2444 | 🔴-0.13 | 0.814 |
| S02_TETSUBAN | win | 55 | 0.5145 | 0.4545 | 0.2597 | 🔴-0.05 | 0.865 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 10 | 0.2246 | 0.4000 | 🔴-0.1754 |
| 0.30-0.50 | 148 | 0.4141 | 0.2770 | 🔴+0.1371 |
| 0.50+ | 173 | 0.5395 | 0.3757 | 🔴+0.1638 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 55 | 0.757 |
| win | <10.0 | ✅learned | 38 | 0.529 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-31T16:20:01.743706+09:00_