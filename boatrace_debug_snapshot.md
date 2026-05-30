# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-30T15:00:01.615253+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×47 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 PSI_DRIFT_DETECTED×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×15  [2026-05-30T14:45:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-30T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-30T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×50  [2026-05-30T14:09:28]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-05-30T14:05:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×108  [2026-05-30T14:05:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×54  [2026-05-30T14:05:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×6  [2026-05-30T10:44:30]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-05-30T10:36:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=51 hit%=49.0% hit_CI[Bonf]=[30.4,67.9]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=51 pred=0.5110 hit=0.4902 cal_err=+0.0208 brier=0.2555 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S00: n=177 hit%=27.7% hit_CI[Bonf]=[19.1,38.2]% ROI=0.94 ROI_boot95=[0.68,1.22]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=100 hit%=30.0% hit_CI[Bonf]=[18.7,44.3]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=100<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-30T06:00:13]
- key: `ORPHAN_SCAN|233 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.84MB / last modified 2026-05-30T15:00:07.134670+09:00

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
= run_cycle 14:58:06 ===
2026-05-30 14:58:06,438 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-30 14:58:06,438 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-30 14:58:06,506 [INFO] predictor: Models loaded OK
2026-05-30 14:58:18,899 [INFO] scraper: odds3t: 120/120 parsed
2026-05-30 14:58:20,005 [INFO] scraper: odds3f: 20/20 parsed
2026-05-30 14:58:21,126 [INFO] scraper: odds2t: 30/30 parsed
2026-05-30 14:58:21,127 [INFO] scraper: odds2f: 15/15 parsed
2026-05-30 14:58:22,250 [INFO] scraper: odds_win: 5/6 parsed
2026-05-30 14:58:22,251 [INFO] scraper: fetch_race 17/9: boats=6 odds=190/191
2026-05-30 14:58:22,255 [INFO] predictor: CALIBRATION_MODE=on
2026-05-30 14:58:22,255 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-30 14:58:22,259 [INFO] run_cycle: fetched 17/9 [scan]: 155 combos
2026-05-30 14:58:25,763 [INFO] scraper: odds3t: 120/120 parsed
2026-05-30 14:58:26,932 [INFO] scraper: odds3f: 19/20 parsed
2026-05-30 14:58:28,045 [INFO] scraper: odds2t: 27/30 parsed
2026-05-30 14:58:28,046 [INFO] scraper: odds2f: 13/15 parsed
2026-05-30 14:58:29,130 [INFO] scraper: odds_win: 3/6 parsed
2026-05-30 14:58:29,130 [INFO] scraper: fetch_race 11/10: boats=6 odds=182/191
2026-05-30 14:58:29,139 [INFO] predictor: CALIBRATION_MODE=on
2026-05-30 14:58:29,139 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-05-30 14:58:29,147 [INFO] run_cycle: fetched 11/10 [scan]: 150 combos
2026-05-30 14:58:29,353 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-30 14:59:05,727 [INFO] run_cycle: === run_cycle 14:59:05 ===
2026-05-30 14:59:05,727 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-30 14:59:05,727 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-30 14:59:05,768 [INFO] predictor: Models loaded OK
2026-05-30 14:59:06,339 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 20, 'scan': 17}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 51
  CIRCUIT_BREAKER_TRIP: 47
  ANOMALY_SCRAPER_FAILURE_BURST: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  KS_ODDS_DRIFT: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
  PSI_DRIFT_DETECTED: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 5 | 11,100 | 3,720 | -7,380 | 0.335 |
| S01_NAKAANA1 | 40 | 12 | 8,000 | 6,020 | -1,980 | 0.752 |
| S02_TETSUBAN | 9 | 6 | 1,800 | 2,440 | +640 | 1.356 |

## 直近アラート (24h・新しい順)
```
[14:59:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1047}
[14:58:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1074}
[14:57:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1076}
[14:56:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1088}
[14:55:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1093}
[14:54:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1097}
[14:53:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1095}
[14:52:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[14:51:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1116}
[14:50:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1117}
```

## 本日残レース: 75件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 105件 締切済
- 通知発射: scan=13 nid / final=17 nid / result=14 nid
- predictions: 17 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 039R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 14:49:20 |
| S01_NAKAANA1 | 118R | win | 1 | 0.3599 | 3.0 | 1.08 | 200 | scan=- drift=- | 14:05:21 |
| S00 | 098R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=- drift=- | 13:59:31 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=3.0 drift=+23.3% | 13:58:27 |
| S02_TETSUBAN | 116R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 13:08:32 |
| S01_NAKAANA1 | 025R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=- drift=- | 12:41:29 |
| S00 | 084R | win | 1 | 0.2082 | 42.0 | 8.74 | 300 | scan=- drift=- | 12:09:21 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=3.1 drift=+22.6% | 11:52:31 |
| S00 | 147R | win | 1 | 0.5990 | 11.9 | 7.13 | 300 | scan=12.3 drift=-3.3% | 11:29:20 |
| S00 | 093R | win | 1 | 0.5053 | 24.7 | 12.48 | 300 | scan=7.5 drift=+229.3% | 11:26:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +8.1% | -81.4% | +229.3% | 14 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 472.4s |
| **Latency** (scan→final max) | 601.8s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,700円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 338 | 0.4568 | 0.3195 | +0.1372 | 🟡+30% | 0.2345 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4237 | 0.2778 | 0.2223 | 🔴-0.11 | 0.936 |
| S01_NAKAANA1 | win | 106 | 0.4861 | 0.3113 | 0.2447 | 🔴-0.14 | 0.805 |
| S02_TETSUBAN | win | 52 | 0.5115 | 0.4808 | 0.2561 | 🔴-0.03 | 0.915 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 5 | 0.1221 | 0.0000 | 🔴+0.1221 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2231 | 0.4545 | 🔴-0.2315 |
| 0.30-0.50 | 141 | 0.4144 | 0.2695 | 🔴+0.1449 |
| 0.50+ | 170 | 0.5390 | 0.3765 | 🔴+0.1626 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 51 | 0.765 |
| win | <10.0 | ✅learned | 37 | 0.538 |
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
_auto-generated by claude_snapshot.py at 2026-05-30T15:00:01.615253+09:00_