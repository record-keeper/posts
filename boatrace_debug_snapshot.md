# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-14T05:20:01.191220+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-14T04:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-13T23:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-06-13T23:08:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×104  [2026-06-13T23:08:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-06-13T23:08:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×49  [2026-06-13T14:56:22]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×20  [2026-06-13T13:42:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-13T09:00:28]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=133<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-13T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-13T06:00:10]
- key: `ROI_STAT|S00: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.84 ROI_boot95=[0.57,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-13T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=133 hit%=27.8% hit_CI[Bonf]=[18.2,40.1]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-13T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=35.4% hit_CI[Bonf]=[22.1,51.3]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-13T06:00:10]
- key: `ORPHAN_SCAN|139 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-13T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=33.3% ROI=0.92 (コスト 9,700/回収 8,910)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-13T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=17.6% ROI=0.36 (コスト 7,500/回収 2,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-13T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=30.3% ROI=0.55 (コスト 15,400/回収 8,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-13T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=20.0% ROI=0.89 (コスト 8,000/回収 7,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.03MB / last modified 2026-06-14T05:00:08.680485+09:00

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
94 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-13 23:55:06,094 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-13 23:55:06,131 [INFO] predictor: Models loaded OK
2026-06-13 23:55:06,133 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-13 23:56:05,931 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-13 23:56:05,931 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-13 23:56:05,932 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-13 23:56:05,975 [INFO] predictor: Models loaded OK
2026-06-13 23:56:05,979 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-13 23:57:06,340 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-13 23:57:06,340 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-13 23:57:06,340 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-13 23:57:06,386 [INFO] predictor: Models loaded OK
2026-06-13 23:57:06,390 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-13 23:58:05,364 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-06-13 23:58:05,364 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-13 23:58:05,364 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-13 23:58:05,426 [INFO] predictor: Models loaded OK
2026-06-13 23:58:05,431 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-13 23:59:06,201 [INFO] run_cycle: === run_cycle 23:59:06 ===
2026-06-13 23:59:06,202 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-13 23:59:06,202 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-13 23:59:06,289 [INFO] predictor: Models loaded OK
2026-06-13 23:59:06,295 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 8, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 117
  FINAL_MISSING: 64
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 20
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 14 | 10,800 | 13,110 | +2,310 | 1.214 |
| S01_NAKAANA1 | 32 | 12 | 6,400 | 6,840 | +440 | 1.069 |
| S02_TETSUBAN | 27 | 9 | 5,400 | 2,720 | -2,680 | 0.504 |

## 直近アラート (24h・新しい順)
```
[23:53:06] FINAL_MISSING: {"deadline": "2026-06-13T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061310051016", "sid": "S00"}
[23:45:07] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 2720, "roi_7d": 0.504, "sid": "S02_TETSUBAN"}
[23:33:06] FINAL_MISSING: {"deadline": "2026-06-13T13:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061322041357", "sid": "S00"}
[23:24:05] FINAL_MISSING: {"deadline": "2026-06-13T12:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061310101247", "sid": "S00"}
[23:12:06] FINAL_MISSING: {"deadline": "2026-06-13T15:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061316101537", "sid": "S00"}
[23:12:06] FINAL_MISSING: {"deadline": "2026-06-13T12:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061303041235", "sid": "S00"}
[23:08:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:08:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:08:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:04:06] FINAL_MISSING: {"deadline": "2026-06-13T13:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061303061329", "sid": "S00"}
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
| S00 | 069R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=- drift=- | 15:31:21 |
| S02_TETSUBAN | 168R | win | 1 | 0.5053 | 2.5 | 1.26 | 200 | scan=2.1 drift=+19.0% | 14:20:27 |
| S00 | 037R | win | 1 | 0.3177 | 8.3 | 2.64 | 300 | scan=8.0 drift=+3.8% | 13:53:47 |
| S01_NAKAANA1 | 148R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.5 drift=-31.1% | 12:08:26 |
| S01_NAKAANA1 | 033R | win | 1 | 0.4920 | 3.7 | 1.82 | 200 | scan=- drift=- | 12:05:26 |
| S02_TETSUBAN | 134R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=- drift=- | 11:54:45 |
| S00 | 163R | win | 1 | 0.5719 | 6.2 | 3.55 | 300 | scan=8.4 drift=-26.2% | 11:47:32 |
| S00 | 113R | win | 1 | 0.5358 | 9.0 | 4.82 | 300 | scan=- drift=- | 11:21:32 |
| S02_TETSUBAN | 208R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 18:41:32 |
| S02_TETSUBAN | 072R | win | 1 | 0.5719 | 2.9 | 1.66 | 200 | scan=- drift=- | 16:05:48 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +10.3% | -82.9% | +274.6% | 13 | 5 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 525.3s |
| **Latency** (scan→final max) | 661.1s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 351 | 0.4677 | 0.2963 | +0.1714 | 🟡+37% | 0.2383 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 141 | 0.4169 | 0.2837 | 0.2172 | 🔴-0.07 | 0.865 |
| S01_NAKAANA1 | win | 130 | 0.4843 | 0.2769 | 0.2456 | 🔴-0.23 | 0.777 |
| S02_TETSUBAN | win | 80 | 0.5301 | 0.3500 | 0.2634 | 🔴-0.16 | 0.569 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1231 | 0.2000 | 🔴-0.0769 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 7 | 0.2244 | 0.2857 | 🔴-0.0613 |
| 0.30-0.50 | 127 | 0.4169 | 0.2283 | 🔴+0.1886 |
| 0.50+ | 199 | 0.5409 | 0.3568 | 🔴+0.1841 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 40 | 0.725 |
| win | <5.0 | ✅learned | 73 | 0.74 |
| win | <10.0 | ✅learned | 49 | 0.506 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-14T05:20:01.191220+09:00_