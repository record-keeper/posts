# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-05T18:30:02.045336+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×59 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-07-05T18:27:59]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×19  [2026-07-05T18:11:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-07-05T18:05:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×29  [2026-07-05T18:01:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-05T17:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×19  [2026-07-05T15:48:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×11  [2026-07-05T10:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=140<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=14 pred=0.2291 actual=0.0714 gap=+0.1577`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S00: n=169 hit%=27.8% hit_CI[Bonf]=[19.1,38.6]% ROI=0.74 ROI_boot95=[0.54,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=140 hit%=32.1% hit_CI[Bonf]=[22.0,44.3]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-05T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=35.1% hit_CI[Bonf]=[21.4,51.9]% ROI=0.59 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-05T06:00:11]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.88 (コスト 10,200/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=23.8% ROI=0.59 (コスト 10,000/回収 5,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=32.3% ROI=0.78 (コスト 21,700/回収 16,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=26 hit%=34.6% ROI=1.06 (コスト 6,400/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-05T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=29 hit%=20.7% ROI=0.49 (コスト 8,200/回収 3,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.85MB / last modified 2026-07-05T18:30:04.511866+09:00

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
O] predictor: CALIBRATION_MODE=on
2026-07-05 18:27:57,613 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-05 18:27:57,621 [INFO] run_cycle: fetched 12/8 [scan]: 154 combos
2026-07-05 18:27:57,813 [INFO] race_id: notif: nid=2026070512081840 sid=S00 phase=scan rank=S
2026-07-05 18:27:58,497 [INFO] notifier: Discord notify OK (status=204)
2026-07-05 18:27:58,880 [INFO] notifier: Discord notify OK (status=204)
2026-07-05 18:27:58,921 [INFO] run_cycle: SCAN S00 住之江8R S
2026-07-05 18:27:59,034 [INFO] run_cycle: run_cycle done: 1 notifications
2026-07-05 18:28:06,045 [INFO] run_cycle: === run_cycle 18:28:06 ===
2026-07-05 18:28:06,045 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-05 18:28:06,045 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 18:28:06,103 [INFO] predictor: Models loaded OK
2026-07-05 18:28:18,548 [INFO] scraper: odds3t: 120/120 parsed
2026-07-05 18:28:19,633 [INFO] scraper: odds3f: 20/20 parsed
2026-07-05 18:28:20,737 [INFO] scraper: odds2t: 30/30 parsed
2026-07-05 18:28:20,738 [INFO] scraper: odds2f: 15/15 parsed
2026-07-05 18:28:21,812 [INFO] scraper: odds_win: 6/6 parsed
2026-07-05 18:28:21,812 [INFO] scraper: fetch_race 24/3: boats=6 odds=191/191
2026-07-05 18:28:21,823 [INFO] predictor: CALIBRATION_MODE=on
2026-07-05 18:28:21,823 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-05 18:28:21,831 [INFO] run_cycle: fetched 24/3 [scan]: 156 combos
2026-07-05 18:28:22,022 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-05 18:29:06,055 [INFO] run_cycle: === run_cycle 18:29:06 ===
2026-07-05 18:29:06,056 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-05 18:29:06,056 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-05 18:29:06,127 [INFO] predictor: Models loaded OK
2026-07-05 18:29:06,579 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 20, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 128
  FINAL_MISSING: 59
  ANOMALY_SCAN_FINAL_RATIO: 17
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 8
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 10 | 10,800 | 7,500 | -3,300 | 0.694 |
| S01_NAKAANA1 | 39 | 14 | 7,800 | 7,300 | -500 | 0.936 |
| S02_TETSUBAN | 25 | 12 | 5,000 | 4,340 | -660 | 0.868 |

## 直近アラート (24h・新しい順)
```
[18:29:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 817}
[18:28:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 827}
[18:27:59] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 820}
[18:11:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[18:08:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 886}
[18:07:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 905}
[18:06:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 919}
[18:05:42] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:05:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 901}
[18:01:42] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 7500, "roi_7d": 0.694, "sid": "S00"}
```

## 本日残レース: 25件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 143件 締切済
- 通知発射: scan=25 nid / final=29 nid / result=18 nid
- predictions: 20 / うち結果DB記録済: 20
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 015R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=- drift=- | 17:27:32 |
| S02_TETSUBAN | 1611R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=2.8 drift=-28.6% | 16:08:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.3599 | 3.3 | 1.19 | 200 | scan=4.7 drift=-29.8% | 15:22:22 |
| S02_TETSUBAN | 058R | win | 1 | 0.5367 | 2.3 | 1.23 | 200 | scan=- drift=- | 15:03:21 |
| S01_NAKAANA1 | 099R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 14:37:46 |
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 14:33:46 |
| S02_TETSUBAN | 098R | win | 1 | 0.5476 | 2.8 | 1.53 | 200 | scan=- drift=- | 14:07:28 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=- drift=- | 14:06:52 |
| S00 | 045R | win | 1 | 0.4989 | 4.2 | 2.10 | 300 | scan=- drift=- | 13:53:22 |
| S01_NAKAANA1 | 045R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=- drift=- | 13:52:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +8.4% | -68.9% | +584.6% | 20 | 5 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 422.2s |
| **Latency** (scan→final max) | 623.5s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 2,400円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 393 | 0.4791 | 0.3181 | +0.1610 | 🟡+34% | 0.2389 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4423 | 0.2892 | 0.2228 | 🔴-0.08 | 0.781 |
| S01_NAKAANA1 | win | 150 | 0.4886 | 0.3200 | 0.2437 | 🔴-0.12 | 0.871 |
| S02_TETSUBAN | win | 77 | 0.5399 | 0.3766 | 0.2644 | 🔴-0.13 | 0.643 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 139 | 0.4216 | 0.2878 | 🔴+0.1338 |
| 0.50+ | 230 | 0.5433 | 0.3522 | 🔴+0.1911 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 60 | 0.75 |
| win | <5.0 | ✅learned | 120 | 0.717 |
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
_auto-generated by claude_snapshot.py at 2026-07-05T18:30:02.045336+09:00_