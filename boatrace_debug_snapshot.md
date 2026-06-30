# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-30T12:00:02.156880+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×65 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-30T11:30:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-30T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×51  [2026-06-30T11:08:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-06-30T11:02:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-06-30T11:02:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-06-30T11:02:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-06-30T10:35:48]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-30T06:00:44]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-30T06:00:44]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S00: n=160 hit%=26.9% hit_CI[Bonf]=[18.1,38.0]% ROI=0.72 ROI_boot95=[0.52,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=31.2% hit_CI[Bonf]=[21.1,43.3]% ROI=0.84 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=31.2% hit_CI[Bonf]=[18.4,47.6]% ROI=0.48 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=24.3% ROI=0.78 (コスト 10,700/回収 8,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=24.4% ROI=0.58 (コスト 9,700/回収 5,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=28.9% ROI=0.73 (コスト 19,400/回収 14,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=27 hit%=29.6% ROI=1.00 (コスト 6,500/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=26.7% ROI=0.55 (コスト 8,400/回収 4,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.48MB / last modified 2026-06-30T12:00:07.656157+09:00

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
1:59:27,793 [INFO] scraper: odds2f: 13/15 parsed
2026-06-30 11:59:28,918 [INFO] scraper: odds_win: 3/6 parsed
2026-06-30 11:59:28,918 [INFO] scraper: fetch_race 11/4: boats=6 odds=184/191
2026-06-30 11:59:28,926 [INFO] predictor: CALIBRATION_MODE=on
2026-06-30 11:59:28,928 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-06-30 11:59:28,965 [INFO] run_cycle: fetched 11/4 [scan]: 151 combos
2026-06-30 11:59:32,453 [INFO] scraper: odds3t: 120/120 parsed
2026-06-30 11:59:33,595 [INFO] scraper: odds3f: 20/20 parsed
2026-06-30 11:59:34,680 [INFO] scraper: odds2t: 25/30 parsed
2026-06-30 11:59:34,681 [INFO] scraper: odds2f: 12/15 parsed
2026-06-30 11:59:35,781 [INFO] scraper: odds_win: 2/6 parsed
2026-06-30 11:59:36,138 [INFO] scraper: fetch_race 08/4: boats=6 odds=179/191
2026-06-30 11:59:36,148 [INFO] predictor: CALIBRATION_MODE=on
2026-06-30 11:59:36,150 [INFO] predictor: combos: {'win': 2, '2t': 25, '3t': 120}
2026-06-30 11:59:36,159 [INFO] run_cycle: fetched 08/4 [scan]: 147 combos
2026-06-30 11:59:39,712 [INFO] scraper: odds3t: 120/120 parsed
2026-06-30 11:59:40,792 [INFO] scraper: odds3f: 20/20 parsed
2026-06-30 11:59:41,960 [INFO] scraper: odds2t: 30/30 parsed
2026-06-30 11:59:41,961 [INFO] scraper: odds2f: 15/15 parsed
2026-06-30 11:59:43,085 [INFO] scraper: odds_win: 6/6 parsed
2026-06-30 11:59:43,086 [INFO] scraper: fetch_race 16/4: boats=6 odds=191/191
2026-06-30 11:59:43,094 [INFO] predictor: CALIBRATION_MODE=on
2026-06-30 11:59:43,094 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-30 11:59:43,102 [INFO] run_cycle: fetched 16/4 [scan]: 156 combos
2026-06-30 11:59:43,306 [INFO] race_id: notif: nid=2026063016041212 sid=S02_TETSUBAN phase=scan rank=B
2026-06-30 11:59:43,906 [INFO] notifier: Discord notify OK (status=204)
2026-06-30 11:59:45,268 [INFO] notifier: Discord notify OK (status=204)
2026-06-30 11:59:45,538 [INFO] run_cycle: SCAN S02_TETSUBAN 児島4R B
2026-06-30 11:59:45,662 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 19, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 69
  FINAL_MISSING: 65
  CIRCUIT_BREAKER_TRIP: 23
  ANOMALY_BET_VOLUME_SPIKE: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  ANOMALY_SCAN_FINAL_RATIO: 5
  KS_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 7,500 | -5,400 | 0.581 |
| S01_NAKAANA1 | 39 | 17 | 7,800 | 8,500 | +700 | 1.09 |
| S02_TETSUBAN | 10 | 3 | 2,000 | 800 | -1,200 | 0.4 |

## 直近アラート (24h・新しい順)
```
[11:59:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1158}
[11:58:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1144}
[11:57:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1143}
[11:56:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1141}
[11:55:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1142}
[11:54:55] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1134}
[11:53:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[11:52:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1095}
[11:51:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1117}
[11:45:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1101}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 37件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 021R | win | 1 | 0.5891 | 4.1 | 2.42 | 200 | scan=4.2 drift=-2.4% | 10:44:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5476 | 4.2 | 2.30 | 200 | scan=4.0 drift=+5.0% | 10:41:32 |
| S01_NAKAANA1 | 203R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=4.1 drift=-4.9% | 18:31:25 |
| S00 | 127R | win | 1 | 0.5123 | 5.5 | 2.82 | 300 | scan=- drift=- | 18:18:22 |
| S02_TETSUBAN | 0512R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=- drift=- | 17:18:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 15:25:24 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.4 drift=+8.3% | 15:19:29 |
| S00 | 029R | win | 1 | 0.5334 | 5.0 | 2.67 | 300 | scan=16.1 drift=-68.9% | 14:45:33 |
| S02_TETSUBAN | 119R | win | 1 | 0.5990 | 2.7 | 1.62 | 200 | scan=- drift=- | 14:43:23 |
| S01_NAKAANA1 | 099R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 14:40:48 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +4.7% | -68.9% | +325.0% | 23 | 12 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.3s |
| **Latency** (scan→final max) | 649.9s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 374 | 0.4830 | 0.2914 | +0.1916 | 🟡+40% | 0.2406 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 158 | 0.4437 | 0.2658 | 0.2260 | 🔴-0.16 | 0.718 |
| S01_NAKAANA1 | win | 139 | 0.4941 | 0.3094 | 0.2426 | 🔴-0.14 | 0.819 |
| S02_TETSUBAN | win | 77 | 0.5439 | 0.3117 | 0.2672 | 🔴-0.25 | 0.481 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2269 | 0.0909 | 🔴+0.1360 |
| 0.30-0.50 | 123 | 0.4275 | 0.2439 | 🔴+0.1836 |
| 0.50+ | 227 | 0.5443 | 0.3304 | 🔴+0.2139 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 49 | 0.725 |
| win | <5.0 | ✅learned | 110 | 0.719 |
| win | <10.0 | ✅learned | 60 | 0.489 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-30T12:00:02.156880+09:00_