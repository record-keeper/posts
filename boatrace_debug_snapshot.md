# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-02T07:50:01.117731+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×115 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-11-02T07:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-11-02T06:00:13]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=34.1% ROI=0.94 (コスト 9,500/回収 8,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S00: n=174 hit%=30.5% hit_CI[Bonf]=[21.5,41.2]% ROI=0.83 ROI_boot95=[0.61,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=33.7% hit_CI[Bonf]=[24.3,44.6]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=65 hit%=47.7% hit_CI[Bonf]=[31.1,64.8]% ROI=1.07 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=22 hit%=50.0% ROI=1.35 (コスト 6,400/回収 8,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=76 hit%=40.8% ROI=1.12 (コスト 17,400/回収 19,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=61 hit%=32.8% ROI=0.97 (コスト 14,700/回収 14,190)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=43 hit%=23.3% ROI=0.75 (コスト 11,400/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=414 pred=0.4767 actual=0.3454 error=+0.1313 (+28%) brier=0.2393 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=174 pred=0.4389 hit=0.3046 cal_err=+0.1343 brier=0.2275 BSS=-0.07 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=175 pred=0.4863 hit=0.3371 cal_err=+0.1492 brier=0.2420 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=65 pred=0.5519 hit=0.4769 cal_err=+0.0749 brier=0.2640 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2291 actual=0.2000 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3213 actual=0.2059 gap=+0.1154`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.4MB / last modified 2026-11-02T07:30:03.141043+09:00

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
45 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 23:55:04,545 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 23:55:04,594 [INFO] predictor: Models loaded OK
2026-11-01 23:55:04,597 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-01 23:56:03,041 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-11-01 23:56:03,041 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 23:56:03,041 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 23:56:03,070 [INFO] predictor: Models loaded OK
2026-11-01 23:56:03,072 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-01 23:57:03,674 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-11-01 23:57:03,674 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 23:57:03,674 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 23:57:03,701 [INFO] predictor: Models loaded OK
2026-11-01 23:57:03,703 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-01 23:58:03,566 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-11-01 23:58:03,566 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 23:58:03,566 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 23:58:03,609 [INFO] predictor: Models loaded OK
2026-11-01 23:58:03,613 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-01 23:59:03,175 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-11-01 23:59:03,175 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 23:59:03,175 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 23:59:03,202 [INFO] predictor: Models loaded OK
2026-11-01 23:59:03,204 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 27
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 27
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 4, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 270
  FINAL_MISSING: 115
  CIRCUIT_BREAKER_NO_ACTION: 33
  ANOMALY_SCAN_FINAL_RATIO: 22
  CIRCUIT_BREAKER_TRIP: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 8 | 10,800 | 6,750 | -4,050 | 0.625 |
| S01_NAKAANA1 | 29 | 7 | 5,800 | 4,260 | -1,540 | 0.734 |
| S02_TETSUBAN | 12 | 4 | 2,400 | 3,840 | +1,440 | 1.6 |

## 直近アラート (24h・新しい順)
```
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 6750, "roi_7d": 0.625, "sid": "S00"}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:57:03] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 6750, "roi_7d": 0.625, "sid": "S00"}
[23:57:03] FINAL_MISSING: {"deadline": "2026-11-01T09:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110114020901", "sid": "S00"}
[23:57:03] FINAL_MISSING: {"deadline": "2026-11-01T13:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110103061309", "sid": "S02_TETSUBAN"}
[23:57:03] FINAL_MISSING: {"deadline": "2026-11-01T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110102041206", "sid": "S01_NAKAANA1"}
[23:57:03] FINAL_MISSING: {"deadline": "2026-11-01T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110102041206", "sid": "S00"}
[23:44:05] FINAL_MISSING: {"deadline": "2026-11-01T16:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110107031609", "sid": "S02_TETSUBAN"}
[23:41:05] FINAL_MISSING: {"deadline": "2026-11-01T11:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110104031148", "sid": "S01_NAKAANA1"}
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
| S02_TETSUBAN | 0711R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 20:05:24 |
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |
| S00 | 022R | win | 1 | 0.2290 | 5.7 | 1.31 | 300 | scan=- drift=- | 11:11:18 |
| S00 | 243R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 16:23:14 |
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:54:24 |
| S00 | 048R | win | 1 | 0.5174 | 7.7 | 3.98 | 300 | scan=15.8 drift=-51.3% | 14:08:04 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5719 | 3.8 | 2.17 | 200 | scan=3.8 drift=+0.0% | 13:53:40 |
| S00 | 024R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=10.5 drift=-50.5% | 12:04:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +7.9% | -58.7% | +111.7% | 13 | 6 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 340.4s |
| **Latency** (scan→final max) | 554.6s |
| **Traffic** (notifications 24h) | 27 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 414 | 0.4767 | 0.3454 | +0.1313 | 🟡+28% | 0.2393 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4389 | 0.3046 | 0.2275 | 🔴-0.07 | 0.825 |
| S01_NAKAANA1 | win | 175 | 0.4863 | 0.3371 | 0.2420 | 🔴-0.08 | 0.877 |
| S02_TETSUBAN | win | 65 | 0.5519 | 0.4769 | 0.2640 | 🔴-0.06 | 1.069 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2291 | 0.2000 | ✅+0.0291 |
| 0.30-0.50 | 149 | 0.4100 | 0.3221 | 🔴+0.0879 |
| 0.50+ | 242 | 0.5447 | 0.3802 | 🔴+0.1646 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 359 | 0.742 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-11-02T07:50:01.117731+09:00_