# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-16T17:50:01.460936+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×44  [2026-07-16T17:06:51]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×54  [2026-07-16T15:56:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×48  [2026-07-16T11:42:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×39  [2026-07-16T10:00:43]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-16T06:00:09]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=42.6% hit_CI[Bonf]=[27.1,59.8]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=68 pred=0.5440 hit=0.4265 cal_err=+0.1175 brier=0.2626 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S00: n=177 hit%=28.8% hit_CI[Bonf]=[20.1,39.4]% ROI=0.74 ROI_boot95=[0.55,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=156 hit%=30.8% hit_CI[Bonf]=[21.3,42.2]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.76 (コスト 11,300/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=32.2% ROI=0.83 (コスト 19,900/回収 16,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=31.4% ROI=0.62 (コスト 8,700/回収 5,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=401 pred=0.4696 actual=0.3192 error=+0.1504 (+32%) brier=0.2376 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.76MB / last modified 2026-07-16T17:49:03.901274+09:00

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
ycle 17:46:03 ===
2026-07-16 17:46:03,472 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 17:46:03,472 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 17:46:03,498 [INFO] predictor: Models loaded OK
2026-07-16 17:46:14,536 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=12&hd=20260716: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-16 17:46:25,851 [WARNING] scraper: beforeinfo parse failed: jcd=12 rno=7
2026-07-16 17:46:25,852 [WARNING] run_cycle: fetch None: 12/7
2026-07-16 17:46:25,852 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 17:47:03,426 [INFO] run_cycle: === run_cycle 17:47:03 ===
2026-07-16 17:47:03,426 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 17:47:03,426 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 17:47:03,469 [INFO] predictor: Models loaded OK
2026-07-16 17:47:03,570 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 17:48:03,871 [INFO] run_cycle: === run_cycle 17:48:03 ===
2026-07-16 17:48:03,871 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 17:48:03,872 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 17:48:03,898 [INFO] predictor: Models loaded OK
2026-07-16 17:48:03,982 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 17:49:03,631 [INFO] run_cycle: === run_cycle 17:49:03 ===
2026-07-16 17:49:03,631 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 17:49:03,631 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 17:49:03,673 [INFO] predictor: Models loaded OK
2026-07-16 17:49:03,776 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 49
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 49
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 11, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 172
  FINAL_MISSING: 32
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 6
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_SCAN_FINAL_RATIO: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 16 | 14,400 | 14,070 | -330 | 0.977 |
| S01_NAKAANA1 | 38 | 12 | 7,600 | 6,340 | -1,260 | 0.834 |
| S02_TETSUBAN | 16 | 8 | 3,200 | 4,200 | +1,000 | 1.312 |

## 直近アラート (24h・新しい順)
```
[17:14:04] FINAL_MISSING: {"deadline": "2026-07-16T12:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071608051242", "sid": "S00"}
[17:06:51] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:55:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 965}
[16:54:03] FINAL_MISSING: {"deadline": "2026-07-16T15:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071601011523", "sid": "S00"}
[16:54:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 980}
[16:53:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 997}
[16:52:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 992}
[16:51:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1007}
[16:50:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1002}
[16:49:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1016}
```

## 本日残レース: 29件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 115件 締切済
- 通知発射: scan=14 nid / final=17 nid / result=10 nid
- predictions: 11 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 015R | win | 1 | 0.3177 | 6.3 | 2.00 | 300 | scan=- drift=- | 17:06:43 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=3.5 drift=+2.9% | 16:39:29 |
| S02_TETSUBAN | 072R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 15:44:29 |
| S02_TETSUBAN | 071R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 15:17:20 |
| S01_NAKAANA1 | 174R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 12:10:22 |
| S01_NAKAANA1 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 200 | scan=3.7 drift=+21.6% | 11:42:20 |
| S00 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 300 | scan=- drift=- | 11:42:19 |
| S01_NAKAANA1 | 132R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 11:00:23 |
| S01_NAKAANA1 | 186R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=3.7 drift=+27.0% | 10:56:20 |
| S02_TETSUBAN | 216R | win | 1 | 0.5515 | 2.4 | 1.32 | 200 | scan=- drift=- | 10:45:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +21.3% | -48.8% | +533.3% | 15 | 5 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 408.3s |
| **Latency** (scan→final max) | 598.9s |
| **Traffic** (notifications 24h) | 49 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 405 | 0.4695 | 0.3185 | +0.1510 | 🟡+32% | 0.2378 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4287 | 0.2898 | 0.2265 | 🔴-0.10 | 0.745 |
| S01_NAKAANA1 | win | 160 | 0.4824 | 0.3000 | 0.2398 | 🔴-0.14 | 0.777 |
| S02_TETSUBAN | win | 69 | 0.5438 | 0.4348 | 0.2620 | 🔴-0.07 | 0.887 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2282 | 0.2000 | ✅+0.0282 |
| 0.30-0.50 | 150 | 0.4169 | 0.2800 | 🔴+0.1369 |
| 0.50+ | 225 | 0.5427 | 0.3511 | 🔴+0.1916 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 73 | 0.802 |
| win | <5.0 | ✅learned | 143 | 0.71 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-16T17:50:01.460936+09:00_