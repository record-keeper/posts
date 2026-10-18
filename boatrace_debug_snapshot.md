# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-19T02:10:01.099007+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-10-18T23:08:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-10-18T15:09:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×47  [2026-10-18T14:41:38]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-10-18T10:59:30]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_BET_VOLUME_DROP  ×42  [2026-10-18T10:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-18T06:00:07]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=42.4% ROI=1.07 (コスト 9,500/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=47 hit%=29.8% ROI=0.93 (コスト 12,000/回収 11,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1845 actual=0.0000 gap=+0.1845`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S00: n=176 hit%=28.4% hit_CI[Bonf]=[19.7,39.0]% ROI=0.76 ROI_boot95=[0.56,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=36.0% hit_CI[Bonf]=[26.3,47.0]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=86 hit%=52.3% hit_CI[Bonf]=[37.3,67.0]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=49 hit%=34.7% ROI=0.78 (コスト 11,500/回収 8,980)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=85 hit%=41.2% ROI=1.22 (コスト 19,200/回収 23,500)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=59 hit%=33.9% ROI=0.86 (コスト 14,200/回収 12,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.18MB / last modified 2026-10-19T02:00:02.073200+09:00

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
01 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 23:55:03,502 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 23:55:03,534 [INFO] predictor: Models loaded OK
2026-10-18 23:55:03,536 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-18 23:56:03,395 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-10-18 23:56:03,395 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 23:56:03,395 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 23:56:03,441 [INFO] predictor: Models loaded OK
2026-10-18 23:56:03,445 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-18 23:57:03,521 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-10-18 23:57:03,521 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 23:57:03,522 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 23:57:03,567 [INFO] predictor: Models loaded OK
2026-10-18 23:57:03,574 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-18 23:58:04,136 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-18 23:58:04,136 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 23:58:04,136 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 23:58:04,181 [INFO] predictor: Models loaded OK
2026-10-18 23:58:04,185 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-18 23:59:04,254 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-18 23:59:04,254 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 23:59:04,254 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 23:59:04,288 [INFO] predictor: Models loaded OK
2026-10-18 23:59:04,290 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 80
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 80
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 18, 'scan': 32}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 78
  ANOMALY_SCRAPER_FAILURE_BURST: 37
  ANOMALY_SCAN_FINAL_RATIO: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 16 | 15,000 | 13,200 | -1,800 | 0.88 |
| S01_NAKAANA1 | 44 | 17 | 8,800 | 8,420 | -380 | 0.957 |
| S02_TETSUBAN | 20 | 11 | 4,000 | 3,880 | -120 | 0.97 |

## 直近アラート (24h・新しい順)
```
[23:57:03] FINAL_MISSING: {"deadline": "2026-10-18T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101808071320", "sid": "S00"}
[23:52:03] FINAL_MISSING: {"deadline": "2026-10-18T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101802021116", "sid": "S00"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-10-18T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101801051715", "sid": "S00"}
[23:38:03] FINAL_MISSING: {"deadline": "2026-10-18T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101809041159", "sid": "S00"}
[23:34:04] FINAL_MISSING: {"deadline": "2026-10-18T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101816011055", "sid": "S00"}
[23:24:04] FINAL_MISSING: {"deadline": "2026-10-18T13:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101808081348", "sid": "S00"}
[23:08:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:06:04] FINAL_MISSING: {"deadline": "2026-10-18T11:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101809031130", "sid": "S00"}
[22:56:03] FINAL_MISSING: {"deadline": "2026-10-18T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101808071320", "sid": "S00"}
[22:52:03] FINAL_MISSING: {"deadline": "2026-10-18T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101802021116", "sid": "S00"}
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
| S01_NAKAANA1 | 015R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.8 drift=+15.8% | 17:12:19 |
| S00 | 0812R | win | 1 | 0.5735 | 7.9 | 4.53 | 300 | scan=8.7 drift=-9.2% | 16:00:32 |
| S00 | 0810R | win | 1 | 0.5123 | 28.6 | 14.65 | 300 | scan=4.8 drift=+495.8% | 14:47:18 |
| S00 | 089R | win | 1 | 0.5323 | 21.0 | 11.18 | 300 | scan=14.2 drift=+47.9% | 14:15:19 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.8 drift=-7.9% | 13:58:19 |
| S00 | 037R | win | 1 | 0.4111 | 15.7 | 6.45 | 300 | scan=6.0 drift=+161.7% | 13:53:18 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=4.5 drift=-22.2% | 13:11:18 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.1 drift=+0.0% | 13:02:43 |
| S01_NAKAANA1 | 163R | win | 1 | 0.5719 | 4.8 | 2.75 | 200 | scan=3.7 drift=+29.7% | 11:49:19 |
| S00 | 163R | win | 1 | 0.5719 | 4.8 | 2.75 | 300 | scan=4.1 drift=+17.1% | 11:49:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +21.5% | -52.2% | +495.8% | 17 | 6 | 51 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 429.7s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 80 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 440 | 0.4794 | 0.3545 | +0.1249 | 🟡+26% | 0.2440 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4428 | 0.2793 | 0.2382 | 🔴-0.18 | 0.761 |
| S01_NAKAANA1 | win | 177 | 0.4912 | 0.3559 | 0.2441 | 🔴-0.06 | 0.994 |
| S02_TETSUBAN | win | 84 | 0.5328 | 0.5119 | 0.2564 | 🔴-0.03 | 0.886 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 6 | 0.1845 | 0.0000 | 🔴+0.1845 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 159 | 0.4165 | 0.3145 | 🔴+0.1020 |
| 0.50+ | 260 | 0.5436 | 0.3885 | 🔴+0.1551 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 187 | 0.773 |
| win | <5.0 | ✅learned | 337 | 0.752 |
| win | <10.0 | ✅learned | 147 | 0.459 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-19T02:10:01.099007+09:00_