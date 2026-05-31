# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-31T11:20:01.786792+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-05-31T11:01:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×36  [2026-05-31T11:01:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-05-31T11:01:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-31T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-31T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-05-31T09:00:14]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-31T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-31T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-31T06:00:15]
- key: `ORPHAN_SCAN|231 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.05 (コスト 8,400/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S00: n=181 hit%=28.2% hit_CI[Bonf]=[19.7,38.6]% ROI=0.94 ROI_boot95=[0.68,1.23]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=110 hit%=31.8% hit_CI[Bonf]=[20.7,45.5]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=110<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-31T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=53 hit%=47.2% hit_CI[Bonf]=[29.1,66.0]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-31T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=53<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=30.0% ROI=0.85 (コスト 14,700/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=32.4% ROI=0.88 (コスト 16,200/回収 14,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=32 hit%=28.1% ROI=1.04 (コスト 7,600/回収 7,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-31T06:00:15]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.45 (コスト 9,200/回収 4,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.93MB / last modified 2026-05-31T11:19:28.560213+09:00

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
arsed
2026-05-31 11:18:20,467 [INFO] scraper: fetch_race 18/7: boats=6 odds=185/191
2026-05-31 11:18:20,478 [INFO] predictor: CALIBRATION_MODE=on
2026-05-31 11:18:20,479 [INFO] predictor: combos: {'win': 6, '2t': 27, '3t': 120}
2026-05-31 11:18:20,486 [INFO] run_cycle: fetched 18/7 [scan]: 153 combos
2026-05-31 11:18:20,757 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-31 11:19:05,756 [INFO] run_cycle: === run_cycle 11:19:05 ===
2026-05-31 11:19:05,757 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-31 11:19:05,757 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-31 11:19:05,802 [INFO] predictor: Models loaded OK
2026-05-31 11:19:18,348 [INFO] scraper: odds3t: 120/120 parsed
2026-05-31 11:19:19,415 [INFO] scraper: odds3f: 20/20 parsed
2026-05-31 11:19:20,500 [INFO] scraper: odds2t: 30/30 parsed
2026-05-31 11:19:20,501 [INFO] scraper: odds2f: 15/15 parsed
2026-05-31 11:19:21,594 [INFO] scraper: odds_win: 3/6 parsed
2026-05-31 11:19:21,596 [INFO] scraper: fetch_race 09/3: boats=6 odds=188/191
2026-05-31 11:19:21,615 [INFO] predictor: CALIBRATION_MODE=on
2026-05-31 11:19:21,615 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-31 11:19:21,627 [INFO] run_cycle: fetched 09/3 [scan]: 153 combos
2026-05-31 11:19:25,034 [INFO] scraper: odds3t: 120/120 parsed
2026-05-31 11:19:26,149 [INFO] scraper: odds3f: 19/20 parsed
2026-05-31 11:19:27,232 [INFO] scraper: odds2t: 30/30 parsed
2026-05-31 11:19:27,235 [INFO] scraper: odds2f: 14/15 parsed
2026-05-31 11:19:28,309 [INFO] scraper: odds_win: 4/6 parsed
2026-05-31 11:19:28,309 [INFO] scraper: fetch_race 14/7: boats=6 odds=187/191
2026-05-31 11:19:28,317 [INFO] predictor: CALIBRATION_MODE=on
2026-05-31 11:19:28,319 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-31 11:19:28,325 [INFO] run_cycle: fetched 14/7 [scan]: 154 combos
2026-05-31 11:19:28,470 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 19, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 72
  FINAL_MISSING: 51
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 26
  ANOMALY_BET_VOLUME_SPIKE: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 6 | 11,700 | 4,050 | -7,650 | 0.346 |
| S01_NAKAANA1 | 38 | 13 | 7,600 | 5,980 | -1,620 | 0.787 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 2,240 | +440 | 1.244 |

## 直近アラート (24h・新しい順)
```
[11:06:37] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 4050, "roi_7d": 0.338, "sid": "S00"}
[11:01:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:01:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:46:29] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 4050, "roi_7d": 0.346, "sid": "S00"}
[10:01:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:21] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 4050, "roi_7d": 0.355, "sid": "S00"}
[10:01:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:01:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[09:01:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 160件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 32件 締切済
- 通知発射: scan=1 nid / final=3 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 132R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=- drift=- | 11:06:20 |
| S01_NAKAANA1 | 146R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 11:00:27 |
| S00 | 236R | win | 1 | 0.3177 | 11.6 | 3.69 | 300 | scan=8.2 drift=+41.5% | 10:46:21 |
| S00 | 156R | win | 1 | 0.1485 | 5.6 | 0.83 | 300 | scan=5.2 drift=+7.7% | 17:46:21 |
| S01_NAKAANA1 | 122R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.7 drift=+5.4% | 16:12:20 |
| S01_NAKAANA1 | 0811R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=4.7 drift=-2.1% | 15:38:20 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.3 drift=+12.1% | 15:21:21 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 15:05:22 |
| S01_NAKAANA1 | 039R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 14:49:20 |
| S01_NAKAANA1 | 118R | win | 1 | 0.3599 | 3.0 | 1.08 | 200 | scan=- drift=- | 14:05:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 43 | +11.4% | -81.4% | +229.3% | 12 | 8 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 437.6s |
| **Latency** (scan→final max) | 599.8s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 343 | 0.4564 | 0.3207 | +0.1357 | 🟡+30% | 0.2348 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4222 | 0.2778 | 0.2219 | 🔴-0.11 | 0.898 |
| S01_NAKAANA1 | win | 110 | 0.4851 | 0.3182 | 0.2449 | 🔴-0.13 | 0.795 |
| S02_TETSUBAN | win | 53 | 0.5129 | 0.4717 | 0.2578 | 🔴-0.03 | 0.898 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 10 | 0.2246 | 0.4000 | 🔴-0.1754 |
| 0.30-0.50 | 145 | 0.4142 | 0.2690 | 🔴+0.1453 |
| 0.50+ | 171 | 0.5394 | 0.3801 | 🔴+0.1592 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 53 | 0.746 |
| win | <10.0 | ✅learned | 38 | 0.529 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-31T11:20:01.786792+09:00_