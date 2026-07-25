# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-26T07:30:01.386959+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-26T07:00:01]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-07-26T06:00:08]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=80 hit%=33.8% ROI=0.82 (コスト 18,300/回収 14,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=23.7% ROI=0.67 (コスト 10,500/回収 6,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2273 actual=0.3077 gap=-0.0804`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S00: n=182 hit%=28.6% hit_CI[Bonf]=[20.0,39.0]% ROI=0.77 ROI_boot95=[0.57,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=26.7% hit_CI[Bonf]=[18.0,37.5]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-26T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-26T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=50.6% hit_CI[Bonf]=[35.0,66.2]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.59 (コスト 10,300/回収 6,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=31.0% ROI=0.89 (コスト 10,200/回収 9,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-26T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=25.7% ROI=0.52 (コスト 8,200/回収 4,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=424 pred=0.4637 actual=0.3184 error=+0.1453 (+31%) brier=0.2333 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=182 pred=0.4195 hit=0.2857 cal_err=+0.1338 brier=0.2220 BSS=-0.09 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=165 pred=0.4767 hit=0.2667 cal_err=+0.2100 brier=0.2371 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=77 pred=0.5404 hit=0.5065 cal_err=+0.0339 brier=0.2517 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1262 actual=0.1429 gap=-0.0167`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-26T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1804 actual=0.3333 gap=-0.1530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.74MB / last modified 2026-07-26T07:30:02.494418+09:00

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
88 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-25 23:55:03,888 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-25 23:55:03,930 [INFO] predictor: Models loaded OK
2026-07-25 23:55:03,934 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-25 23:56:03,750 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-25 23:56:03,750 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-25 23:56:03,750 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-25 23:56:03,778 [INFO] predictor: Models loaded OK
2026-07-25 23:56:03,780 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-25 23:57:03,470 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-07-25 23:57:03,470 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-25 23:57:03,470 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-25 23:57:03,497 [INFO] predictor: Models loaded OK
2026-07-25 23:57:03,499 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-25 23:58:04,057 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-07-25 23:58:04,058 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-25 23:58:04,058 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-25 23:58:04,101 [INFO] predictor: Models loaded OK
2026-07-25 23:58:04,107 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-25 23:59:04,049 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-07-25 23:59:04,049 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-25 23:59:04,049 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-25 23:59:04,093 [INFO] predictor: Models loaded OK
2026-07-25 23:59:04,100 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 12, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 141
  FINAL_MISSING: 37
  CIRCUIT_BREAKER_NO_ACTION: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 3
  CIRCUIT_BREAKER_TRIP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 11 | 13,800 | 10,140 | -3,660 | 0.735 |
| S01_NAKAANA1 | 36 | 6 | 7,200 | 5,180 | -2,020 | 0.719 |
| S02_TETSUBAN | 15 | 8 | 3,000 | 2,720 | -280 | 0.907 |

## 直近アラート (24h・新しい順)
```
[06:00:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:52:03] FINAL_MISSING: {"deadline": "2026-07-25T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072514020912", "sid": "S00"}
[23:50:07] FINAL_MISSING: {"deadline": "2026-07-25T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072502061314", "sid": "S00"}
[23:12:03] FINAL_MISSING: {"deadline": "2026-07-25T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072503041235", "sid": "S00"}
[23:08:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:08:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:08:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:52:03] FINAL_MISSING: {"deadline": "2026-07-25T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072514020912", "sid": "S00"}
[22:49:03] FINAL_MISSING: {"deadline": "2026-07-25T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072502061314", "sid": "S00"}
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
| S00 | 015R | win | 1 | 0.1231 | 8.0 | 0.98 | 300 | scan=- drift=- | 17:22:30 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=3.6 drift=+16.7% | 17:10:21 |
| S00 | 204R | win | 1 | 0.5174 | 4.2 | 2.17 | 300 | scan=4.0 drift=+5.0% | 17:10:20 |
| S00 | 1711R | win | 1 | 0.5735 | 7.3 | 4.19 | 300 | scan=39.7 drift=-81.6% | 16:10:44 |
| S00 | 202R | win | 1 | 0.3177 | 8.6 | 2.73 | 300 | scan=7.5 drift=+14.7% | 16:00:31 |
| S02_TETSUBAN | 0311R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=2.0 drift=+25.0% | 15:50:19 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 15:13:19 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5334 | 4.6 | 2.45 | 200 | scan=3.8 drift=+21.1% | 14:21:19 |
| S00 | 038R | win | 1 | 0.5334 | 4.6 | 2.45 | 300 | scan=33.0 drift=-86.1% | 14:21:18 |
| S01_NAKAANA1 | 044R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 13:21:17 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +22.1% | -86.1% | +628.9% | 17 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 500.8s |
| **Latency** (scan→final max) | 604.2s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 424 | 0.4637 | 0.3184 | +0.1453 | 🟡+31% | 0.2333 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4195 | 0.2857 | 0.2220 | 🔴-0.09 | 0.766 |
| S01_NAKAANA1 | win | 165 | 0.4767 | 0.2667 | 0.2371 | 🔴-0.21 | 0.75 |
| S02_TETSUBAN | win | 77 | 0.5404 | 0.5065 | 0.2517 | 🔴-0.01 | 0.996 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 9 | 0.1804 | 0.3333 | 🔴-0.1530 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 168 | 0.4163 | 0.2798 | 🔴+0.1365 |
| 0.50+ | 223 | 0.5420 | 0.3587 | 🔴+0.1833 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 85 | 0.807 |
| win | <5.0 | ✅learned | 152 | 0.725 |
| win | <10.0 | ✅learned | 81 | 0.457 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-26T07:30:01.386959+09:00_