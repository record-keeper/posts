# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-25T13:40:01.522492+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×31 (24h)
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-09-25T13:38:31]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×68  [2026-09-25T13:03:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×68  [2026-09-25T13:03:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×34  [2026-09-25T13:03:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×7  [2026-09-25T12:53:30]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-09-25T11:25:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-25T06:00:23]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=27.6% ROI=0.90 (コスト 8,200/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3237 actual=0.2333 gap=+0.0904`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S00: n=171 hit%=22.2% hit_CI[Bonf]=[14.5,32.6]% ROI=0.71 ROI_boot95=[0.47,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=21.9% hit_CI[Bonf]=[13.9,32.8]% ROI=0.65 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=44.9% hit_CI[Bonf]=[29.9,60.8]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=20.5% ROI=0.58 (コスト 9,100/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.05MB / last modified 2026-09-25T13:39:51.744775+09:00

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
un_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-25 13:39:04,437 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-25 13:39:04,508 [INFO] predictor: Models loaded OK
2026-09-25 13:39:15,581 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=18&hd=20260925: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-25 13:39:26,614 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=18&hd=20260925: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-25 13:39:41,232 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 13:39:42,319 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 13:39:43,394 [INFO] scraper: odds2t: 30/30 parsed
2026-09-25 13:39:43,395 [INFO] scraper: odds2f: 14/15 parsed
2026-09-25 13:39:44,499 [INFO] scraper: odds_win: 4/6 parsed
2026-09-25 13:39:44,499 [INFO] scraper: fetch_race 18/11: boats=6 odds=188/191
2026-09-25 13:39:44,502 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 13:39:44,502 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-25 13:39:44,506 [INFO] run_cycle: fetched 18/11 [final]: 154 combos
2026-09-25 13:39:48,006 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 13:39:49,118 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 13:39:50,226 [INFO] scraper: odds2t: 30/30 parsed
2026-09-25 13:39:50,227 [INFO] scraper: odds2f: 14/15 parsed
2026-09-25 13:39:51,313 [INFO] scraper: odds_win: 4/6 parsed
2026-09-25 13:39:51,313 [INFO] scraper: fetch_race 22/5: boats=6 odds=188/191
2026-09-25 13:39:51,315 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 13:39:51,315 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-25 13:39:51,319 [INFO] run_cycle: fetched 22/5 [scan]: 154 combos
2026-09-25 13:39:51,586 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 83
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 83
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 14, 'scan': 35}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 161
  CIRCUIT_BREAKER_TRIP: 31
  CIRCUIT_BREAKER_NO_ACTION: 21
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 6 | 10,200 | 3,990 | -6,210 | 0.391 |
| S01_NAKAANA1 | 32 | 7 | 6,400 | 3,220 | -3,180 | 0.503 |
| S02_TETSUBAN | 22 | 11 | 4,400 | 3,760 | -640 | 0.855 |

## 直近アラート (24h・新しい順)
```
[13:38:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1062}
[13:37:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1079}
[13:35:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[13:34:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1074}
[13:33:02] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3220, "roi_7d": 0.503, "sid": "S01_NAKAANA1"}
[13:33:02] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1087}
[13:31:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1082}
[13:30:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1094}
[13:28:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1086}
[13:27:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1106}
```

## 本日残レース: 75件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 69件 締切済
- 通知発射: scan=19 nid / final=17 nid / result=8 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 137R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.2 drift=-9.5% | 13:21:22 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=2.5 drift=-16.0% | 13:14:31 |
| S00 | 096R | win | 1 | 0.4989 | 15.0 | 7.48 | 300 | scan=- drift=- | 12:53:20 |
| S02_TETSUBAN | 054R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=- drift=- | 12:30:24 |
| S00 | 053R | win | 1 | 0.1485 | 9.7 | 1.44 | 300 | scan=4.8 drift=+102.1% | 12:03:19 |
| S01_NAKAANA1 | 094R | win | 1 | 0.5663 | 3.9 | 2.21 | 200 | scan=3.7 drift=+5.4% | 11:54:32 |
| S01_NAKAANA1 | 083R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 11:31:20 |
| S00 | 051R | win | 1 | 0.5891 | 6.1 | 3.59 | 300 | scan=4.0 drift=+52.5% | 11:04:56 |
| S01_NAKAANA1 | 131R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=3.7 drift=+2.7% | 10:43:19 |
| S00 | 111R | win | 1 | 0.1485 | 4.0 | 0.59 | 300 | scan=10.5 drift=-61.9% | 10:27:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | -1.1% | -81.7% | +102.1% | 16 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 476.2s |
| **Latency** (scan→final max) | 671.0s |
| **Traffic** (notifications 24h) | 83 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 398 | 0.4765 | 0.2663 | +0.2101 | 🟡+44% | 0.2445 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4445 | 0.2229 | 0.2345 | 🔴-0.35 | 0.688 |
| S01_NAKAANA1 | win | 153 | 0.4847 | 0.2157 | 0.2483 | 🔴-0.47 | 0.633 |
| S02_TETSUBAN | win | 79 | 0.5278 | 0.4557 | 0.2582 | 🔴-0.04 | 0.814 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.30-0.50 | 151 | 0.4148 | 0.2318 | 🔴+0.1830 |
| 0.50+ | 229 | 0.5443 | 0.2969 | 🔴+0.2474 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 154 | 0.771 |
| win | <5.0 | ✅learned | 265 | 0.757 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-25T13:40:01.522492+09:00_