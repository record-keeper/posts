# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-26T06:50:01.485495+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×82 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 CALIBRATION_DRIFT×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1802 actual=0.3750 gap=-0.1948`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=34 hit%=26.5% ROI=0.84 (コスト 8,200/回収 6,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S00: n=160 hit%=24.4% hit_CI[Bonf]=[16.0,35.3]% ROI=0.64 ROI_boot95=[0.45,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=30.7% hit_CI[Bonf]=[20.7,42.9]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=31.6% hit_CI[Bonf]=[18.7,48.1]% ROI=0.53 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-26T06:00:13]
- key: `ORPHAN_SCAN|152 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=19.4% ROI=0.65 (コスト 8,800/回収 5,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 8,500/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=75 hit%=28.0% ROI=0.64 (コスト 17,900/回収 11,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=29 hit%=20.7% ROI=0.42 (コスト 8,200/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=373 pred=0.4777 actual=0.2815 error=+0.1962 (+41%) brier=0.2413 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=160 pred=0.4363 hit=0.2437 cal_err=+0.1926 brier=0.2260 BSS=-0.23 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=137 pred=0.4911 hit=0.3066 cal_err=+0.1846 brier=0.2426 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=76 pred=0.5408 hit=0.3158 cal_err=+0.2250 brier=0.2711 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=102 pred=0.4430 actual=0.2255 gap=+0.2176`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.0MB / last modified 2026-06-26T06:30:05.003575+09:00

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
25 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-25 23:55:06,526 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 23:55:06,583 [INFO] predictor: Models loaded OK
2026-06-25 23:55:06,587 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-25 23:56:05,897 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-25 23:56:05,897 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-25 23:56:05,897 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 23:56:05,941 [INFO] predictor: Models loaded OK
2026-06-25 23:56:05,945 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-25 23:57:06,847 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-25 23:57:06,847 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-25 23:57:06,847 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 23:57:06,907 [INFO] predictor: Models loaded OK
2026-06-25 23:57:06,911 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-25 23:58:05,751 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-06-25 23:58:05,751 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-25 23:58:05,751 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 23:58:05,820 [INFO] predictor: Models loaded OK
2026-06-25 23:58:05,826 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-25 23:59:05,629 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-25 23:59:05,629 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-25 23:59:05,629 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 23:59:05,701 [INFO] predictor: Models loaded OK
2026-06-25 23:59:05,705 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 13, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 195
  FINAL_MISSING: 82
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 28
  CALIBRATION_DRIFT: 20
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 9
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 9 | 15,000 | 6,240 | -8,760 | 0.416 |
| S01_NAKAANA1 | 37 | 11 | 7,400 | 5,440 | -1,960 | 0.735 |
| S02_TETSUBAN | 11 | 2 | 2,200 | 1,020 | -1,180 | 0.464 |

## 直近アラート (24h・新しい順)
```
[06:00:09] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:09] CIRCUIT_BREAKER_TRIP: {"cost": 15000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 6240, "roi_7d": 0.416, "sid": "S00"}
[06:00:09] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008307, "ks_stat": 0.192}
[06:00:09] CALIBRATION_DRIFT: {"avg_actual": 0.2245, "avg_pred": 0.4723, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 98, "overconf_pct": 52.5}
[06:00:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:57:06] FINAL_MISSING: {"deadline": "2026-06-25T15:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062503101522", "sid": "S00"}
[23:51:06] FINAL_MISSING: {"deadline": "2026-06-25T11:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062503011114", "sid": "S00"}
[23:40:09] CALIBRATION_DRIFT: {"avg_actual": 0.2245, "avg_pred": 0.4723, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 98, "overconf_pct": 52.5}
[23:40:09] FINAL_MISSING: {"deadline": "2026-06-25T16:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062504091605", "sid": "S00"}
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
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=4.4 drift=-15.9% | 18:05:23 |
| S01_NAKAANA1 | 075R | win | 1 | 0.5020 | 3.7 | 1.86 | 200 | scan=- drift=- | 17:40:33 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=- drift=- | 16:02:21 |
| S01_NAKAANA1 | 0311R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 15:50:23 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=- drift=- | 15:11:37 |
| S00 | 225R | win | 1 | 0.4111 | 45.0 | 18.50 | 300 | scan=- drift=- | 14:23:33 |
| S00 | 067R | win | 1 | 0.5735 | 12.0 | 6.88 | 300 | scan=- drift=- | 14:18:32 |
| S00 | 037R | win | 1 | 0.5174 | 5.6 | 2.90 | 300 | scan=9.0 drift=-37.8% | 13:53:27 |
| S00 | 188R | win | 1 | 0.4111 | 10.5 | 4.32 | 300 | scan=- drift=- | 11:59:44 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4920 | 3.3 | 1.62 | 200 | scan=- drift=- | 11:52:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +15.7% | -49.2% | +482.2% | 22 | 8 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 427.0s |
| **Latency** (scan→final max) | 610.2s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 373 | 0.4777 | 0.2815 | +0.1962 | 🟡+41% | 0.2413 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4363 | 0.2437 | 0.2260 | 🔴-0.23 | 0.643 |
| S01_NAKAANA1 | win | 137 | 0.4911 | 0.3066 | 0.2426 | 🔴-0.14 | 0.803 |
| S02_TETSUBAN | win | 76 | 0.5408 | 0.3158 | 0.2711 | 🔴-0.25 | 0.53 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 123 | 0.4223 | 0.2276 | 🔴+0.1947 |
| 0.50+ | 224 | 0.5430 | 0.3259 | 🔴+0.2171 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 95 | 0.727 |
| win | <10.0 | ✅learned | 57 | 0.496 |
| win | <20.0 | ✅learned | 15 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-26T06:50:01.485495+09:00_