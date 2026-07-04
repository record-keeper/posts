# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-04T22:10:02.413699+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×73 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×4  [2026-07-04T22:08:08]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×2  [2026-07-04T22:08:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T21:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-04T21:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-07-04T16:49:52]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-04T12:35:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-04T06:00:14]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=32.0% ROI=1.06 (コスト 6,100/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=23.3% ROI=0.51 (コスト 8,400/回収 4,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3216 actual=0.1818 gap=+0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=27.8% ROI=0.85 (コスト 10,500/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S00: n=168 hit%=26.8% hit_CI[Bonf]=[18.2,37.6]% ROI=0.72 ROI_boot95=[0.53,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=32.5% hit_CI[Bonf]=[19.4,48.9]% ROI=0.54 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=24.4% ROI=0.61 (コスト 9,700/回収 5,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-04T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=29.7% ROI=0.71 (コスト 21,300/回収 15,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-04T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=382 pred=0.4791 actual=0.2958 error=+0.1833 (+38%) brier=0.2396 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.72MB / last modified 2026-07-04T22:09:08.489871+09:00

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
80 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 22:05:06,180 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 22:05:06,295 [INFO] predictor: Models loaded OK
2026-07-04 22:05:06,305 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-04 22:06:07,212 [INFO] run_cycle: === run_cycle 22:06:07 ===
2026-07-04 22:06:07,214 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 22:06:07,214 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 22:06:07,301 [INFO] predictor: Models loaded OK
2026-07-04 22:06:07,306 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-04 22:07:07,791 [INFO] run_cycle: === run_cycle 22:07:07 ===
2026-07-04 22:07:07,791 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 22:07:07,792 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 22:07:07,880 [INFO] predictor: Models loaded OK
2026-07-04 22:07:07,883 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-04 22:08:07,182 [INFO] run_cycle: === run_cycle 22:08:07 ===
2026-07-04 22:08:07,182 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 22:08:07,182 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 22:08:07,224 [INFO] predictor: Models loaded OK
2026-07-04 22:08:07,228 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-04 22:09:06,879 [INFO] run_cycle: === run_cycle 22:09:06 ===
2026-07-04 22:09:06,879 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-04 22:09:06,879 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-04 22:09:06,992 [INFO] predictor: Models loaded OK
2026-07-04 22:09:07,000 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 82
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 82
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 14, 'scan': 36}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 76
  FINAL_MISSING: 73
  CIRCUIT_BREAKER_NO_ACTION: 35
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 11 | 10,800 | 8,190 | -2,610 | 0.758 |
| S01_NAKAANA1 | 37 | 15 | 7,400 | 7,540 | +140 | 1.019 |
| S02_TETSUBAN | 22 | 11 | 4,400 | 3,780 | -620 | 0.859 |

## 直近アラート (24h・新しい順)
```
[22:08:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:08:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[22:08:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:06:07] FINAL_MISSING: {"deadline": "2026-07-04T15:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070404081532", "sid": "S00"}
[22:04:05] FINAL_MISSING: {"deadline": "2026-07-04T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070413031129", "sid": "S01_NAKAANA1"}
[21:58:06] FINAL_MISSING: {"deadline": "2026-07-04T15:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070419011522", "sid": "S00"}
[21:45:06] FINAL_MISSING: {"deadline": "2026-07-04T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409041209", "sid": "S00"}
[21:43:06] FINAL_MISSING: {"deadline": "2026-07-04T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070409061308", "sid": "S00"}
[21:28:06] FINAL_MISSING: {"deadline": "2026-07-04T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070404051355", "sid": "S00"}
[21:24:05] FINAL_MISSING: {"deadline": "2026-07-04T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070421061047", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 168件 締切済
- 通知発射: scan=32 nid / final=28 nid / result=13 nid
- predictions: 14 / うち結果DB記録済: 14
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 073R | win | 1 | 0.3177 | 4.8 | 1.53 | 200 | scan=- drift=- | 16:39:24 |
| S00 | 073R | win | 1 | 0.3177 | 4.8 | 1.53 | 300 | scan=5.0 drift=-4.0% | 16:39:21 |
| S01_NAKAANA1 | 072R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.2 drift=+6.2% | 16:04:31 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=- drift=- | 16:00:25 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.5 drift=+17.1% | 15:25:21 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5729 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 15:13:33 |
| S02_TETSUBAN | 138R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 14:03:22 |
| S00 | 223R | win | 1 | 0.5269 | 18.7 | 9.85 | 300 | scan=- drift=- | 13:07:21 |
| S00 | 222R | win | 1 | 0.5050 | 4.2 | 2.12 | 300 | scan=5.2 drift=-19.2% | 12:37:33 |
| S01_NAKAANA1 | 188R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=4.2 drift=-26.2% | 12:00:26 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +7.3% | -68.9% | +584.6% | 19 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 488.0s |
| **Latency** (scan→final max) | 604.6s |
| **Traffic** (notifications 24h) | 82 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 383 | 0.4786 | 0.3081 | +0.1705 | 🟡+36% | 0.2395 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4416 | 0.2781 | 0.2232 | 🔴-0.11 | 0.736 |
| S01_NAKAANA1 | win | 140 | 0.4900 | 0.3214 | 0.2456 | 🔴-0.13 | 0.88 |
| S02_TETSUBAN | win | 74 | 0.5414 | 0.3514 | 0.2651 | 🔴-0.16 | 0.591 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 134 | 0.4204 | 0.2761 | 🔴+0.1443 |
| 0.50+ | 225 | 0.5433 | 0.3422 | 🔴+0.2011 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 57 | 0.742 |
| win | <5.0 | ✅learned | 115 | 0.718 |
| win | <10.0 | ✅learned | 65 | 0.479 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-04T22:10:02.413699+09:00_