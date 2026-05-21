# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-21T18:20:01.483595+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×14  [2026-05-21T18:06:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×14  [2026-05-21T18:06:23]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×41  [2026-05-21T17:39:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-05-21T17:13:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-05-21T11:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-21T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-21T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-21T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=22.2% ROI=0.64 (コスト 9,500/回収 6,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-21T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-21T06:00:09]
- key: `ROI_STAT|S00: n=199 hit%=27.1% hit_CI[Bonf]=[19.1,37.0]% ROI=0.92 ROI_boot95=[0.68,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-21T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=199<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-21T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=55 hit%=32.7% hit_CI[Bonf]=[17.8,52.2]% ROI=0.90 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-21T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=55<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-21T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=36 hit%=44.4% hit_CI[Bonf]=[23.9,67.1]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-21T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=36<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-21T06:00:09]
- key: `ORPHAN_SCAN|249 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-21T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=46 hit%=26.1% ROI=0.71 (コスト 13,600/回収 9,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-21T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=31.6% ROI=1.31 (コスト 9,100/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-21T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=58 hit%=27.6% ROI=0.92 (コスト 14,300/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-21T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=0.96 (コスト 5,900/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.11MB / last modified 2026-05-21T18:19:21.953635+09:00

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
5-21 18:16:20,697 [INFO] run_cycle: fetched 01/7 [final]: 156 combos
2026-05-21 18:16:20,903 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-21 18:17:06,561 [INFO] run_cycle: === run_cycle 18:17:06 ===
2026-05-21 18:17:06,561 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-21 18:17:06,561 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-21 18:17:06,610 [INFO] predictor: Models loaded OK
2026-05-21 18:17:06,707 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-21 18:18:06,236 [INFO] run_cycle: === run_cycle 18:18:06 ===
2026-05-21 18:18:06,236 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-21 18:18:06,236 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-21 18:18:06,306 [INFO] predictor: Models loaded OK
2026-05-21 18:18:06,461 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-21 18:19:05,977 [INFO] run_cycle: === run_cycle 18:19:05 ===
2026-05-21 18:19:05,978 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-21 18:19:05,978 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-21 18:19:06,050 [INFO] predictor: Models loaded OK
2026-05-21 18:19:18,476 [INFO] scraper: odds3t: 120/120 parsed
2026-05-21 18:19:19,546 [INFO] scraper: odds3f: 20/20 parsed
2026-05-21 18:19:20,619 [INFO] scraper: odds2t: 30/30 parsed
2026-05-21 18:19:20,620 [INFO] scraper: odds2f: 15/15 parsed
2026-05-21 18:19:21,717 [INFO] scraper: odds_win: 6/6 parsed
2026-05-21 18:19:21,717 [INFO] scraper: fetch_race 15/7: boats=6 odds=191/191
2026-05-21 18:19:21,729 [INFO] predictor: CALIBRATION_MODE=on
2026-05-21 18:19:21,729 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-21 18:19:21,737 [INFO] run_cycle: fetched 15/7 [scan]: 156 combos
2026-05-21 18:19:21,847 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 50
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 50
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 10, 'scan': 18}

## アラート件数 (24h・種類別)
```
  KS_ODDS_DRIFT: 38
  ANOMALY_SCRAPER_FAILURE_BURST: 33
  FINAL_MISSING: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 16
  CIRCUIT_BREAKER_NO_ACTION: 5
  ANOMALY_BET_VOLUME_DROP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 11 | 8,400 | 11,100 | +2,700 | 1.321 |
| S01_NAKAANA1 | 23 | 5 | 4,600 | 4,520 | -80 | 0.983 |
| S02_TETSUBAN | 15 | 5 | 3,000 | 1,400 | -1,600 | 0.467 |

## 直近アラート (24h・新しい順)
```
[18:06:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:00:26] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 6.2e-05, "ks_stat": 0.313}
[17:26:32] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.217, "baseline_mean": 0.783, "baseline_stdev": 0.073, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 15, "z_score": 2.95}
[17:21:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 735}
[17:19:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 731}
[17:18:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 732}
[17:16:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 730}
[17:15:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 748}
[17:14:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 743}
[17:13:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 733}
```

## 本日残レース: 21件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 111件 締切済
- 通知発射: scan=15 nid / final=18 nid / result=9 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 16:25:23 |
| S00 | 013R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=5.5 drift=-16.4% | 16:25:21 |
| S00 | 0911R | win | 1 | 0.5891 | 5.2 | 3.06 | 300 | scan=- drift=- | 15:35:22 |
| S00 | 099R | win | 1 | 0.5476 | 11.4 | 6.24 | 300 | scan=6.0 drift=+90.0% | 14:26:22 |
| S00 | 089R | win | 1 | 0.5123 | 5.7 | 2.92 | 300 | scan=- drift=- | 14:05:22 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 13:43:31 |
| S02_TETSUBAN | 116R | win | 1 | 0.5123 | 2.8 | 1.43 | 200 | scan=2.3 drift=+21.7% | 12:59:32 |
| S00 | 096R | win | 1 | 0.5678 | 7.1 | 4.03 | 300 | scan=12.0 drift=-40.8% | 12:49:21 |
| S01_NAKAANA1 | 113R | win | 1 | 0.3222 | 3.4 | 1.10 | 200 | scan=- drift=- | 11:32:22 |
| S00 | 093R | win | 1 | 0.5123 | 30.5 | 15.63 | 300 | scan=45.0 drift=-32.2% | 11:22:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 37 | -0.3% | -76.3% | +148.9% | 15 | 7 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.2s |
| **Latency** (scan→final max) | 610.4s |
| **Traffic** (notifications 24h) | 50 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 294 | 0.4550 | 0.3095 | +0.1455 | 🟡+32% | 0.2319 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 199 | 0.4358 | 0.2814 | 0.2256 | 🔴-0.12 | 0.924 |
| S01_NAKAANA1 | win | 58 | 0.4850 | 0.3276 | 0.2395 | 🔴-0.09 | 0.874 |
| S02_TETSUBAN | win | 37 | 0.5113 | 0.4324 | 0.2535 | 🔴-0.03 | 0.808 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 131 | 0.4221 | 0.2443 | 🔴+0.1779 |
| 0.50+ | 137 | 0.5399 | 0.3869 | 🔴+0.1530 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 16 | 0.775 |
| win | <5.0 | ✅learned | 35 | 0.819 |
| win | <10.0 | ✅learned | 30 | 0.526 |
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
_auto-generated by claude_snapshot.py at 2026-05-21T18:20:01.483595+09:00_