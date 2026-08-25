# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-26T06:30:01.802953+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-26T06:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-08-26T06:00:09]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.3333 gap=-0.1082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=187 hit%=27.3% hit_CI[Bonf]=[19.0,37.5]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1799 actual=0.2222 gap=-0.0423`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S00: n=161 hit%=26.7% hit_CI[Bonf]=[18.0,37.7]% ROI=0.83 ROI_boot95=[0.57,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=41.0% hit_CI[Bonf]=[26.6,57.2]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=18.4% ROI=0.58 (コスト 11,000/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=37.5% ROI=1.00 (コスト 9,100/回収 9,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=28.9% ROI=0.91 (コスト 20,500/回収 18,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=51 hit%=23.5% ROI=0.49 (コスト 11,700/回収 5,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=22.2% ROI=1.01 (コスト 9,800/回収 9,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=426 pred=0.4721 actual=0.2958 error=+0.1763 (+37%) brier=0.2409 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=161 pred=0.4213 hit=0.2671 cal_err=+0.1542 brier=0.2250 BSS=-0.15 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=187 pred=0.4885 hit=0.2727 cal_err=+0.2158 brier=0.2481 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=78 pred=0.5374 hit=0.4103 cal_err=+0.1271 brier=0.2565 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.46MB / last modified 2026-08-26T06:30:03.641802+09:00

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
40 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 23:55:04,140 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 23:55:04,176 [INFO] predictor: Models loaded OK
2026-08-25 23:55:04,178 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 23:56:04,258 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-25 23:56:04,258 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 23:56:04,258 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 23:56:04,291 [INFO] predictor: Models loaded OK
2026-08-25 23:56:04,293 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 23:57:04,582 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-08-25 23:57:04,582 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 23:57:04,582 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 23:57:04,630 [INFO] predictor: Models loaded OK
2026-08-25 23:57:04,634 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 23:58:04,250 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-08-25 23:58:04,250 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 23:58:04,250 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 23:58:04,297 [INFO] predictor: Models loaded OK
2026-08-25 23:58:04,299 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 23:59:04,125 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-08-25 23:59:04,125 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 23:59:04,125 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 23:59:04,167 [INFO] predictor: Models loaded OK
2026-08-25 23:59:04,169 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 59
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 59
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 10, 'scan': 25}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 63
  ANOMALY_SCRAPER_FAILURE_BURST: 45
  CIRCUIT_BREAKER_TRIP: 18
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 12 | 11,400 | 10,560 | -840 | 0.926 |
| S01_NAKAANA1 | 47 | 15 | 9,400 | 7,360 | -2,040 | 0.783 |
| S02_TETSUBAN | 20 | 6 | 4,000 | 2,380 | -1,620 | 0.595 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2380, "roi_7d": 0.595, "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-08-25T13:13:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082510101313", "sid": "S00"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-08-25T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082508041212", "sid": "S00"}
[23:39:04] FINAL_MISSING: {"deadline": "2026-08-25T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082508021101", "sid": "S00"}
[23:37:04] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2380, "roi_7d": 0.595, "sid": "S02_TETSUBAN"}
[23:27:04] FINAL_MISSING: {"deadline": "2026-08-25T10:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082521061049", "sid": "S00"}
[23:21:04] FINAL_MISSING: {"deadline": "2026-08-25T14:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082522061447", "sid": "S00"}
[23:10:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S02_TETSUBAN | 208R | win | 1 | 0.5640 | 2.0 | 1.13 | 200 | scan=2.8 drift=-28.6% | 18:34:30 |
| S00 | 228R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 15:43:20 |
| S01_NAKAANA1 | 038R | win | 1 | 0.4989 | 4.3 | 2.15 | 200 | scan=- drift=- | 14:21:19 |
| S00 | 224R | win | 1 | 0.5174 | 14.2 | 7.35 | 300 | scan=- drift=- | 13:43:21 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=3.8 drift=+5.3% | 13:10:33 |
| S00 | 188R | win | 1 | 0.5123 | 7.8 | 4.00 | 300 | scan=6.3 drift=+23.8% | 11:57:19 |
| S01_NAKAANA1 | 133R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.1 drift=+19.4% | 11:25:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=- drift=- | 11:01:36 |
| S00 | 186R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=8.8 drift=-44.3% | 10:52:29 |
| S02_TETSUBAN | 212R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 08:55:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +5.4% | -79.6% | +320.7% | 25 | 11 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.1s |
| **Latency** (scan→final max) | 672.7s |
| **Traffic** (notifications 24h) | 59 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 426 | 0.4721 | 0.2958 | +0.1763 | 🟡+37% | 0.2409 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 161 | 0.4213 | 0.2671 | 0.2250 | 🔴-0.15 | 0.832 |
| S01_NAKAANA1 | win | 187 | 0.4885 | 0.2727 | 0.2481 | 🔴-0.25 | 0.851 |
| S02_TETSUBAN | win | 78 | 0.5374 | 0.4103 | 0.2565 | 🔴-0.06 | 0.653 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 9 | 0.1799 | 0.2222 | ✅-0.0423 |
| 0.20-0.30 | 9 | 0.2251 | 0.3333 | 🔴-0.1082 |
| 0.30-0.50 | 151 | 0.4114 | 0.2384 | 🔴+0.1730 |
| 0.50+ | 246 | 0.5447 | 0.3415 | 🔴+0.2033 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 118 | 0.77 |
| win | <5.0 | ✅learned | 218 | 0.748 |
| win | <10.0 | ✅learned | 104 | 0.453 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-26T06:30:01.802953+09:00_