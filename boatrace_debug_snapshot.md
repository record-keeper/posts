# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-13T06:20:01.424233+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×62 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×67 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×62 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-13T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-13T06:00:14]
- key: `ORPHAN_SCAN|180 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-13T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-13T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=47 hit%=17.0% ROI=0.73 (コスト 12,700/回収 9,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-13T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=29.3% ROI=0.97 (コスト 9,300/回収 9,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-13T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=16.7% ROI=0.30 (コスト 9,200/回収 2,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-09-13T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=28.1% hit_CI[Bonf]=[19.3,38.8]% ROI=0.95 ROI_boot95=[0.66,1.29]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-13T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=181 hit%=23.8% hit_CI[Bonf]=[15.9,33.9]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-13T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-13T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=34.1% hit_CI[Bonf]=[21.1,50.1]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-13T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=23.5% ROI=0.68 (コスト 9,700/回収 6,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-13T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=94 hit%=24.5% ROI=0.92 (コスト 21,600/回収 19,910)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=434 pred=0.4729 actual=0.2742 error=+0.1987 (+42%) brier=0.2412 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=171 pred=0.4295 hit=0.2807 cal_err=+0.1488 brier=0.2218 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=181 pred=0.4804 hit=0.2376 cal_err=+0.2429 brier=0.2477 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=82 pred=0.5466 hit=0.3415 cal_err=+0.2052 brier=0.2672 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1780 actual=0.2857 gap=-0.1077`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2244 actual=0.1429 gap=+0.0815`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-13T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=43 pred=0.3229 actual=0.3023 gap=+0.0205`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.05MB / last modified 2026-09-13T06:00:19.067269+09:00

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
97 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-12 23:55:04,497 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-12 23:55:04,546 [INFO] predictor: Models loaded OK
2026-09-12 23:55:04,552 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-12 23:56:03,710 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-12 23:56:03,710 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-12 23:56:03,710 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-12 23:56:03,761 [INFO] predictor: Models loaded OK
2026-09-12 23:56:03,767 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-12 23:57:04,017 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-09-12 23:57:04,017 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-12 23:57:04,017 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-12 23:57:04,068 [INFO] predictor: Models loaded OK
2026-09-12 23:57:04,073 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-12 23:58:04,023 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-09-12 23:58:04,023 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-12 23:58:04,023 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-12 23:58:04,058 [INFO] predictor: Models loaded OK
2026-09-12 23:58:04,060 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-12 23:59:03,768 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-09-12 23:59:03,768 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-12 23:59:03,768 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-12 23:59:03,801 [INFO] predictor: Models loaded OK
2026-09-12 23:59:03,803 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 42
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 42
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 6, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  FINAL_MISSING: 67
  CIRCUIT_BREAKER_TRIP: 62
  CIRCUIT_BREAKER_NO_ACTION: 51
  KS_ODDS_DRIFT: 45
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 6 | 8,400 | 5,280 | -3,120 | 0.629 |
| S01_NAKAANA1 | 36 | 7 | 7,200 | 4,940 | -2,260 | 0.686 |
| S02_TETSUBAN | 21 | 8 | 4,200 | 2,320 | -1,880 | 0.552 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2320, "roi_7d": 0.552, "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 7200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 4940, "roi_7d": 0.686, "sid": "S01_NAKAANA1"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 5280, "roi_7d": 0.629, "sid": "S00"}
[06:00:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008329, "ks_stat": 0.197}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:54:04] FINAL_MISSING: {"deadline": "2026-09-12T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091210051018", "sid": "S00"}
[23:52:03] FINAL_MISSING: {"deadline": "2026-09-12T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091202061314", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 201R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=3.0 drift=+3.3% | 15:17:27 |
| S02_TETSUBAN | 058R | win | 1 | 0.5998 | 2.1 | 1.26 | 200 | scan=- drift=- | 14:29:19 |
| S00 | 024R | win | 1 | 0.4111 | 8.3 | 3.41 | 300 | scan=6.2 drift=+33.9% | 12:11:31 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.8 drift=-21.1% | 11:42:54 |
| S00 | 022R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=4.1 drift=+36.6% | 11:13:26 |
| S00 | 216R | win | 1 | 0.5719 | 4.3 | 2.46 | 300 | scan=- drift=- | 10:56:32 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5334 | 3.0 | 1.60 | 200 | scan=- drift=- | 16:38:21 |
| S01_NAKAANA1 | 201R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.7 drift=-10.8% | 15:20:51 |
| S01_NAKAANA1 | 066R | win | 1 | 0.5086 | 3.1 | 1.58 | 200 | scan=- drift=- | 13:51:32 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.7 drift=-8.1% | 12:58:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +4.3% | -49.1% | +135.7% | 16 | 7 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 537.6s |
| **Latency** (scan→final max) | 621.3s |
| **Traffic** (notifications 24h) | 42 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 434 | 0.4729 | 0.2742 | +0.1987 | 🟡+42% | 0.2412 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4295 | 0.2807 | 0.2218 | 🔴-0.10 | 0.954 |
| S01_NAKAANA1 | win | 181 | 0.4804 | 0.2376 | 0.2477 | 🔴-0.37 | 0.754 |
| S02_TETSUBAN | win | 82 | 0.5466 | 0.3415 | 0.2672 | 🔴-0.19 | 0.591 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 7 | 0.1780 | 0.2857 | 🔴-0.1077 |
| 0.20-0.30 | 7 | 0.2244 | 0.1429 | 🔴+0.0815 |
| 0.30-0.50 | 158 | 0.4019 | 0.2278 | 🔴+0.1741 |
| 0.50+ | 253 | 0.5450 | 0.3123 | 🔴+0.2328 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 136 | 0.767 |
| win | <5.0 | ✅learned | 242 | 0.748 |
| win | <10.0 | ✅learned | 120 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-13T06:20:01.424233+09:00_