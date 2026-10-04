# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-05T06:10:01.957932+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ORPHAN_SCAN  ×1  [2026-10-05T06:00:22]
- key: `ORPHAN_SCAN|183 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-05T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-05T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-05T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-05T06:00:22]
- key: `ROI_STAT|S00: n=165 hit%=21.2% hit_CI[Bonf]=[13.5,31.7]% ROI=0.61 ROI_boot95=[0.41,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-05T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=29.1% hit_CI[Bonf]=[20.2,39.8]% ROI=0.95 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-05T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=48.2% hit_CI[Bonf]=[33.5,63.3]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-05T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=38.7% ROI=1.11 (コスト 8,600/回収 9,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-05T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=25.5% ROI=0.66 (コスト 11,800/回収 7,750)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-05T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=27.8% ROI=0.74 (コスト 20,400/回収 15,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-05T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=35.4% ROI=0.79 (コスト 11,000/回収 8,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-05T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=45 hit%=20.0% ROI=0.64 (コスト 11,900/回収 7,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|bt=win: n=422 pred=0.4801 actual=0.2986 error=+0.1816 (+38%) brier=0.2486 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|S00(win): n=165 pred=0.4491 hit=0.2121 cal_err=+0.2370 brier=0.2458 BSS=-0.47 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=172 pred=0.4892 hit=0.2907 cal_err=+0.1985 brier=0.2491 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=85 pred=0.5221 hit=0.4824 cal_err=+0.0397 brier=0.2529 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3224 actual=0.3103 gap=+0.0121`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=133 pred=0.4409 actual=0.2556 gap=+0.1853`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-05T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.50+: n=244 pred=0.5426 actual=0.3238 gap=+0.2188`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.95MB / last modified 2026-10-05T06:00:47.071997+09:00

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
36 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 23:55:04,936 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 23:55:05,000 [INFO] predictor: Models loaded OK
2026-10-04 23:55:05,002 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-04 23:56:04,293 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-04 23:56:04,293 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 23:56:04,293 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 23:56:04,324 [INFO] predictor: Models loaded OK
2026-10-04 23:56:04,326 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-04 23:57:04,900 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-04 23:57:04,900 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 23:57:04,900 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 23:57:04,932 [INFO] predictor: Models loaded OK
2026-10-04 23:57:04,935 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-04 23:58:03,628 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-10-04 23:58:03,628 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 23:58:03,628 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 23:58:03,676 [INFO] predictor: Models loaded OK
2026-10-04 23:58:03,680 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-04 23:59:04,293 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-04 23:59:04,294 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 23:59:04,294 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 23:59:04,324 [INFO] predictor: Models loaded OK
2026-10-04 23:59:04,326 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 91
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 91
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 22, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 142
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 32
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 12
  ANOMALY_SCAN_FINAL_RATIO: 9
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 12 | 15,900 | 11,100 | -4,800 | 0.698 |
| S01_NAKAANA1 | 51 | 18 | 10,200 | 13,280 | +3,080 | 1.302 |
| S02_TETSUBAN | 17 | 8 | 3,400 | 2,180 | -1,220 | 0.641 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 15900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 11100, "roi_7d": 0.698, "sid": "S00"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:52:04] FINAL_MISSING: {"deadline": "2026-10-04T15:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100412011517", "sid": "S00"}
[23:43:04] CIRCUIT_BREAKER_TRIP: {"cost": 15900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 11100, "roi_7d": 0.698, "sid": "S00"}
[23:43:04] FINAL_MISSING: {"deadline": "2026-10-04T13:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100413061307", "sid": "S02_TETSUBAN"}
[23:18:04] FINAL_MISSING: {"deadline": "2026-10-04T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100405031141", "sid": "S00"}
[23:12:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:12:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
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
| S02_TETSUBAN | 077R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.0 drift=+25.0% | 18:01:21 |
| S01_NAKAANA1 | 125R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=- drift=- | 16:58:19 |
| S01_NAKAANA1 | 124R | win | 1 | 0.5680 | 3.0 | 1.70 | 200 | scan=4.8 drift=-37.5% | 16:31:21 |
| S01_NAKAANA1 | 193R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=3.8 drift=+26.3% | 16:18:58 |
| S00 | 193R | win | 1 | 0.5334 | 4.8 | 2.56 | 300 | scan=4.3 drift=+11.6% | 16:18:55 |
| S01_NAKAANA1 | 0511R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 15:45:32 |
| S00 | 0610R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 15:36:24 |
| S00 | 119R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=6.7 drift=-22.4% | 14:19:20 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=3.2 drift=+31.2% | 13:47:19 |
| S01_NAKAANA1 | 118R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.1 drift=-14.6% | 13:44:36 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 83 | +6.1% | -76.2% | +169.2% | 25 | 11 | 60 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 456.3s |
| **Latency** (scan→final max) | 613.7s |
| **Traffic** (notifications 24h) | 91 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 422 | 0.4801 | 0.2986 | +0.1816 | 🟡+38% | 0.2486 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4491 | 0.2121 | 0.2458 | 🔴-0.47 | 0.607 |
| S01_NAKAANA1 | win | 172 | 0.4892 | 0.2907 | 0.2491 | 🔴-0.21 | 0.947 |
| S02_TETSUBAN | win | 85 | 0.5221 | 0.4824 | 0.2529 | 🔴-0.01 | 0.818 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 162 | 0.4197 | 0.2654 | 🔴+0.1543 |
| 0.50+ | 244 | 0.5426 | 0.3238 | 🔴+0.2188 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 168 | 0.768 |
| win | <5.0 | ✅learned | 293 | 0.768 |
| win | <10.0 | ✅learned | 134 | 0.459 |
| win | <20.0 | ✅learned | 36 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-05T06:10:01.957932+09:00_