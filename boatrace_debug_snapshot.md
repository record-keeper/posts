# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-17T06:50:01.375710+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×86 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×65 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,600/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=22.5% ROI=0.91 (コスト 11,000/回収 9,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.63 ROI_boot95=[0.44,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=176 hit%=21.6% hit_CI[Bonf]=[14.0,31.7]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-17T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-17T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=50.7% hit_CI[Bonf]=[34.4,66.8]% ROI=0.80 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-17T06:00:14]
- key: `ORPHAN_SCAN|208 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=36.1% ROI=1.09 (コスト 8,500/回収 9,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=80 hit%=26.2% ROI=0.60 (コスト 18,700/回収 11,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-17T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=25.0% ROI=0.49 (コスト 11,100/回収 5,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=418 pred=0.4673 actual=0.2703 error=+0.1970 (+42%) brier=0.2368 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=171 pred=0.4195 hit=0.2281 cal_err=+0.1915 brier=0.2218 BSS=-0.26 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=176 pred=0.4893 hit=0.2159 cal_err=+0.2733 brier=0.2497 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=71 pred=0.5279 hit=0.5070 cal_err=+0.0209 brier=0.2410 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2246 actual=0.5000 gap=-0.2754`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-17T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3177 actual=0.2903 gap=+0.0274`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.68MB / last modified 2026-08-17T06:30:08.728357+09:00

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
16 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 23:55:04,516 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 23:55:04,567 [INFO] predictor: Models loaded OK
2026-08-16 23:55:04,570 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 23:56:03,931 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-08-16 23:56:03,931 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 23:56:03,931 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 23:56:03,974 [INFO] predictor: Models loaded OK
2026-08-16 23:56:03,976 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 23:57:03,755 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-08-16 23:57:03,755 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 23:57:03,755 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 23:57:03,788 [INFO] predictor: Models loaded OK
2026-08-16 23:57:03,791 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 23:58:03,508 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-08-16 23:58:03,508 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 23:58:03,508 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 23:58:03,542 [INFO] predictor: Models loaded OK
2026-08-16 23:58:03,544 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 23:59:04,168 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-08-16 23:59:04,168 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 23:59:04,168 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 23:59:04,200 [INFO] predictor: Models loaded OK
2026-08-16 23:59:04,203 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 13, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 133
  FINAL_MISSING: 86
  CIRCUIT_BREAKER_TRIP: 65
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 10 | 12,600 | 7,830 | -4,770 | 0.621 |
| S01_NAKAANA1 | 49 | 10 | 9,800 | 6,840 | -2,960 | 0.698 |
| S02_TETSUBAN | 20 | 10 | 4,000 | 2,680 | -1,320 | 0.67 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2680, "roi_7d": 0.67, "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 6840, "roi_7d": 0.698, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 7830, "roi_7d": 0.621, "sid": "S00"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:53:04] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2680, "roi_7d": 0.67, "sid": "S02_TETSUBAN"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-08-16T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081611041212", "sid": "S00"}
[23:40:05] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 6840, "roi_7d": 0.698, "sid": "S01_NAKAANA1"}
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
| S02_TETSUBAN | 076R | win | 1 | 0.5476 | 2.5 | 1.37 | 200 | scan=2.6 drift=-3.8% | 17:33:18 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5007 | 4.9 | 2.45 | 200 | scan=4.7 drift=+4.3% | 16:30:21 |
| S01_NAKAANA1 | 048R | win | 1 | 0.3177 | 3.6 | 1.14 | 200 | scan=3.7 drift=-2.7% | 15:28:19 |
| S02_TETSUBAN | 099R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 14:21:20 |
| S01_NAKAANA1 | 028R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=- drift=- | 14:13:19 |
| S02_TETSUBAN | 098R | win | 1 | 0.5476 | 2.5 | 1.37 | 200 | scan=2.0 drift=+25.0% | 13:48:18 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=4.6 drift=-6.5% | 13:46:30 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5334 | 4.2 | 2.24 | 200 | scan=4.5 drift=-6.7% | 13:32:20 |
| S00 | 1011R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=4.5 drift=-6.7% | 13:32:18 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 12:47:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +10.1% | -62.9% | +287.7% | 16 | 7 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 481.6s |
| **Latency** (scan→final max) | 606.0s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 418 | 0.4673 | 0.2703 | +0.1970 | 🟡+42% | 0.2368 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4195 | 0.2281 | 0.2218 | 🔴-0.26 | 0.635 |
| S01_NAKAANA1 | win | 176 | 0.4893 | 0.2159 | 0.2497 | 🔴-0.48 | 0.686 |
| S02_TETSUBAN | win | 71 | 0.5279 | 0.5070 | 0.2410 | ✅+0.04 | 0.799 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 8 | 0.2246 | 0.5000 | 🔴-0.2754 |
| 0.30-0.50 | 156 | 0.4165 | 0.2179 | 🔴+0.1986 |
| 0.50+ | 231 | 0.5417 | 0.3160 | 🔴+0.2257 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 111 | 0.765 |
| win | <5.0 | ✅learned | 189 | 0.731 |
| win | <10.0 | ✅learned | 95 | 0.448 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-17T06:50:01.375710+09:00_