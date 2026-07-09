# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-09T13:10:02.009653+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×7  [2026-07-09T13:03:07]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-07-09T13:03:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×32  [2026-07-09T12:28:33]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×53  [2026-07-09T12:11:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-09T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×6  [2026-07-09T10:46:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×19  [2026-07-09T09:09:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=38.2% ROI=1.06 (コスト 9,900/回収 10,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-09T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.67 (コスト 10,100/回収 6,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2291 actual=0.0769 gap=+0.1522`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3230 actual=0.1379 gap=+0.1850`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-09T06:00:14]
- key: `ROI_STAT|S00: n=164 hit%=31.1% hit_CI[Bonf]=[21.8,42.2]% ROI=0.80 ROI_boot95=[0.60,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-09T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=147 hit%=32.7% hit_CI[Bonf]=[22.7,44.5]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-09T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=41.3% hit_CI[Bonf]=[26.6,57.8]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-09T06:00:14]
- key: `ORPHAN_SCAN|160 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-09T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=33.7% ROI=0.82 (コスト 21,400/回収 17,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-09T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=30 hit%=36.7% ROI=1.04 (コスト 7,500/回収 7,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.18MB / last modified 2026-07-09T13:09:07.292363+09:00

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
arsed
2026-07-09 13:07:27,958 [INFO] scraper: odds2t: 30/30 parsed
2026-07-09 13:07:27,959 [INFO] scraper: odds2f: 15/15 parsed
2026-07-09 13:07:29,072 [INFO] scraper: odds_win: 6/6 parsed
2026-07-09 13:07:29,072 [INFO] scraper: fetch_race 11/6: boats=6 odds=191/191
2026-07-09 13:07:29,082 [INFO] predictor: CALIBRATION_MODE=on
2026-07-09 13:07:29,082 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-09 13:07:29,090 [INFO] run_cycle: fetched 11/6 [scan]: 156 combos
2026-07-09 13:07:32,635 [INFO] scraper: odds3t: 120/120 parsed
2026-07-09 13:07:33,742 [INFO] scraper: odds3f: 20/20 parsed
2026-07-09 13:07:34,918 [INFO] scraper: odds2t: 29/30 parsed
2026-07-09 13:07:34,919 [INFO] scraper: odds2f: 13/15 parsed
2026-07-09 13:07:36,016 [INFO] scraper: odds_win: 5/6 parsed
2026-07-09 13:07:36,016 [INFO] scraper: fetch_race 10/11: boats=6 odds=187/191
2026-07-09 13:07:36,025 [INFO] predictor: CALIBRATION_MODE=on
2026-07-09 13:07:36,025 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-07-09 13:07:36,033 [INFO] run_cycle: fetched 10/11 [scan]: 154 combos
2026-07-09 13:07:36,148 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-09 13:08:06,411 [INFO] run_cycle: === run_cycle 13:08:06 ===
2026-07-09 13:08:06,411 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-09 13:08:06,411 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-09 13:08:06,485 [INFO] predictor: Models loaded OK
2026-07-09 13:08:06,699 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-09 13:09:06,208 [INFO] run_cycle: === run_cycle 13:09:06 ===
2026-07-09 13:09:06,208 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-09 13:09:06,208 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-09 13:09:06,285 [INFO] predictor: Models loaded OK
2026-07-09 13:09:06,488 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 140
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_NO_ACTION: 27
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 11
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_SCAN_FINAL_RATIO: 3
  CIRCUIT_BREAKER_TRIP: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 12 | 9,900 | 8,280 | -1,620 | 0.836 |
| S01_NAKAANA1 | 39 | 11 | 7,800 | 6,220 | -1,580 | 0.797 |
| S02_TETSUBAN | 27 | 16 | 5,400 | 5,980 | +580 | 1.107 |

## 直近アラート (24h・新しい順)
```
[13:09:06] FINAL_MISSING: {"deadline": "2026-07-09T11:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070911031138", "sid": "S00"}
[13:04:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1005}
[13:03:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:03:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 988}
[13:02:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 998}
[13:00:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 999}
[12:59:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 986}
[12:57:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 992}
[12:56:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 991}
```

## 本日残レース: 90件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 54件 締切済
- 通知発射: scan=18 nid / final=17 nid / result=9 nid
- predictions: 10 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1410R | win | 1 | 0.5476 | 3.4 | 1.86 | 200 | scan=4.0 drift=-15.0% | 13:06:21 |
| S02_TETSUBAN | 053R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 12:30:25 |
| S00 | 148R | win | 1 | 0.5174 | 6.1 | 3.16 | 300 | scan=- drift=- | 11:57:21 |
| S01_NAKAANA1 | 113R | win | 1 | 0.5990 | 3.7 | 2.22 | 200 | scan=- drift=- | 11:35:34 |
| S00 | 083R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=4.5 drift=+33.3% | 11:33:31 |
| S00 | 147R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=17.6 drift=-73.3% | 11:28:21 |
| S00 | 082R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=4.5 drift=+24.4% | 11:05:22 |
| S01_NAKAANA1 | 186R | win | 1 | 0.5476 | 3.4 | 1.86 | 200 | scan=4.2 drift=-19.0% | 10:50:23 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.7 drift=-2.7% | 09:09:21 |
| S01_NAKAANA1 | 102R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.9 drift=+7.7% | 08:55:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | -2.4% | -73.3% | +44.2% | 16 | 5 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.8s |
| **Latency** (scan→final max) | 678.3s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 389 | 0.4783 | 0.3368 | +0.1416 | 🟡+30% | 0.2360 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4453 | 0.3091 | 0.2244 | 🔴-0.05 | 0.798 |
| S01_NAKAANA1 | win | 149 | 0.4830 | 0.3289 | 0.2379 | 🔴-0.08 | 0.901 |
| S02_TETSUBAN | win | 75 | 0.5417 | 0.4133 | 0.2579 | 🔴-0.06 | 0.717 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1743 | 0.5000 | 🔴-0.3257 |
| 0.20-0.30 | 13 | 0.2291 | 0.0769 | 🔴+0.1522 |
| 0.30-0.50 | 142 | 0.4170 | 0.2958 | 🔴+0.1213 |
| 0.50+ | 225 | 0.5447 | 0.3778 | 🔴+0.1669 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 65 | 0.754 |
| win | <5.0 | ✅learned | 126 | 0.716 |
| win | <10.0 | ✅learned | 68 | 0.47 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-09T13:10:02.009653+09:00_