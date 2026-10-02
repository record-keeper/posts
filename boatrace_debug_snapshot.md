# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-03T08:10:01.594236+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×73 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×10  [2026-10-03T08:00:54]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×10  [2026-10-03T08:00:54]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×10  [2026-10-03T08:00:54]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-03T08:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-03T06:00:21]
- key: `ORPHAN_SCAN|188 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.67 (コスト 10,200/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-03T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=27.9% ROI=0.50 (コスト 9,700/回収 4,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S00: n=163 hit%=20.9% hit_CI[Bonf]=[13.2,31.3]% ROI=0.62 ROI_boot95=[0.40,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=25.9% hit_CI[Bonf]=[17.3,36.9]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=47.6% hit_CI[Bonf]=[32.6,63.0]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=27.5% ROI=0.83 (コスト 21,100/回収 17,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift ≥+30%: n=44 hit%=13.6% ROI=0.36 (コスト 11,600/回収 4,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-03T06:00:21]
- key: `CALIBRATION_LIVE|bt=win: n=407 pred=0.4802 actual=0.2826 error=+0.1976 (+41%) brier=0.2446 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-03T06:00:21]
- key: `CALIBRATION_LIVE|S00(win): n=163 pred=0.4509 hit=0.2086 cal_err=+0.2423 brier=0.2407 BSS=-0.46 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-03T06:00:21]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=162 pred=0.4888 hit=0.2593 cal_err=+0.2295 brier=0.2446 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.81MB / last modified 2026-10-03T08:09:05.186477+09:00

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
43 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 08:05:05,743 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 08:05:05,809 [INFO] predictor: Models loaded OK
2026-10-03 08:05:05,811 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-03 08:06:04,924 [INFO] run_cycle: === run_cycle 08:06:04 ===
2026-10-03 08:06:04,924 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 08:06:04,924 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 08:06:05,014 [INFO] predictor: Models loaded OK
2026-10-03 08:06:05,020 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-03 08:07:05,716 [INFO] run_cycle: === run_cycle 08:07:05 ===
2026-10-03 08:07:05,716 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 08:07:05,716 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 08:07:05,803 [INFO] predictor: Models loaded OK
2026-10-03 08:07:05,805 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-03 08:08:05,184 [INFO] run_cycle: === run_cycle 08:08:05 ===
2026-10-03 08:08:05,184 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 08:08:05,184 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 08:08:05,236 [INFO] predictor: Models loaded OK
2026-10-03 08:08:05,240 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-03 08:09:04,704 [INFO] run_cycle: === run_cycle 08:09:04 ===
2026-10-03 08:09:04,704 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 08:09:04,704 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 08:09:04,783 [INFO] predictor: Models loaded OK
2026-10-03 08:09:04,786 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 17, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 73
  ANOMALY_SCRAPER_FAILURE_BURST: 60
  CIRCUIT_BREAKER_TRIP: 26
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 10 | 13,800 | 7,890 | -5,910 | 0.572 |
| S01_NAKAANA1 | 46 | 13 | 9,200 | 8,140 | -1,060 | 0.885 |
| S02_TETSUBAN | 19 | 10 | 3,800 | 2,720 | -1,080 | 0.716 |

## 直近アラート (24h・新しい順)
```
[08:00:53] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:53] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 7890, "roi_7d": 0.572, "sid": "S00"}
[08:00:53] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:14] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:14] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 7890, "roi_7d": 0.572, "sid": "S00"}
[06:00:14] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:50:08] FINAL_MISSING: {"deadline": "2026-10-02T19:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100219091918", "sid": "S00"}
[23:48:05] FINAL_MISSING: {"deadline": "2026-10-02T09:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100223020909", "sid": "S00"}
[23:43:05] FINAL_MISSING: {"deadline": "2026-10-02T16:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100212031610", "sid": "S00"}
[23:36:05] FINAL_MISSING: {"deadline": "2026-10-02T18:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100207071803", "sid": "S00"}
```

## 本日残レース: 156件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 0件 締切済
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
| S02_TETSUBAN | 078R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=2.2 drift=+0.0% | 18:37:19 |
| S01_NAKAANA1 | 197R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=3.1 drift=+9.7% | 18:12:20 |
| S02_TETSUBAN | 075R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.1 drift=+14.3% | 17:08:21 |
| S00 | 154R | win | 1 | 0.5123 | 4.4 | 2.25 | 300 | scan=- drift=- | 16:34:21 |
| S00 | 124R | win | 1 | 0.4111 | 14.0 | 5.76 | 300 | scan=5.2 drift=+169.2% | 16:31:31 |
| S00 | 0611R | win | 1 | 0.5303 | 5.8 | 3.08 | 300 | scan=9.0 drift=-35.6% | 16:16:21 |
| S00 | 072R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=4.5 drift=+48.9% | 15:45:31 |
| S02_TETSUBAN | 098R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=- drift=- | 13:53:20 |
| S01_NAKAANA1 | 239R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:33:19 |
| S01_NAKAANA1 | 063R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=3.2 drift=+18.7% | 12:17:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 75 | +10.4% | -76.2% | +357.1% | 22 | 11 | 52 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.9s |
| **Latency** (scan→final max) | 611.7s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 407 | 0.4802 | 0.2826 | +0.1976 | 🟡+41% | 0.2446 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4509 | 0.2086 | 0.2407 | 🔴-0.46 | 0.621 |
| S01_NAKAANA1 | win | 162 | 0.4888 | 0.2593 | 0.2446 | 🔴-0.27 | 0.809 |
| S02_TETSUBAN | win | 82 | 0.5214 | 0.4756 | 0.2522 | 🔴-0.01 | 0.818 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 155 | 0.4185 | 0.2323 | 🔴+0.1862 |
| 0.50+ | 237 | 0.5422 | 0.3207 | 🔴+0.2215 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 166 | 0.771 |
| win | <5.0 | ✅learned | 285 | 0.759 |
| win | <10.0 | ✅learned | 131 | 0.461 |
| win | <20.0 | ✅learned | 35 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-10-03T08:10:01.594236+09:00_