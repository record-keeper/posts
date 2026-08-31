# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-31T11:30:01.464352+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×28  [2026-08-31T11:02:50]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×84  [2026-08-31T11:02:50]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-08-31T11:02:50]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-31T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-31T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-31T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-08-31T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-31T06:00:17]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1819 actual=0.1667 gap=+0.0152`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1221 actual=0.1000 gap=+0.0221`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-31T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-31T06:00:17]
- key: `ROI_STAT|S00: n=170 hit%=27.1% hit_CI[Bonf]=[18.5,37.8]% ROI=0.87 ROI_boot95=[0.63,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-31T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=183 hit%=24.6% hit_CI[Bonf]=[16.6,34.8]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-31T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-31T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=41.7% hit_CI[Bonf]=[27.6,57.2]% ROI=0.71 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-31T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=16.2% ROI=0.43 (コスト 10,700/回収 4,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-31T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=31.0% ROI=0.97 (コスト 9,700/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-31T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=29.0% ROI=0.94 (コスト 21,300/回収 20,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.9MB / last modified 2026-08-31T11:30:03.251058+09:00

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
IBRATION_MODE=on
2026-08-31 11:27:25,095 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-31 11:27:25,098 [INFO] run_cycle: fetched 18/7 [scan]: 156 combos
2026-08-31 11:27:25,200 [INFO] race_id: notif: nid=2026083118071137 sid=S01_NAKAANA1 phase=scan rank=B
2026-08-31 11:27:25,818 [INFO] notifier: Discord notify OK (status=204)
2026-08-31 11:27:26,388 [INFO] notifier: Discord notify OK (status=204)
2026-08-31 11:27:26,421 [INFO] run_cycle: SCAN S01_NAKAANA1 徳山7R B
2026-08-31 11:27:26,537 [INFO] run_cycle: run_cycle done: 1 notifications
2026-08-31 11:28:03,204 [INFO] run_cycle: === run_cycle 11:28:03 ===
2026-08-31 11:28:03,204 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-31 11:28:03,204 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-31 11:28:03,254 [INFO] predictor: Models loaded OK
2026-08-31 11:28:03,450 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-31 11:29:03,925 [INFO] run_cycle: === run_cycle 11:29:03 ===
2026-08-31 11:29:03,925 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-31 11:29:03,925 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-31 11:29:03,974 [INFO] predictor: Models loaded OK
2026-08-31 11:29:16,441 [INFO] scraper: odds3t: 120/120 parsed
2026-08-31 11:29:17,534 [INFO] scraper: odds3f: 20/20 parsed
2026-08-31 11:29:18,645 [INFO] scraper: odds2t: 28/30 parsed
2026-08-31 11:29:18,646 [INFO] scraper: odds2f: 15/15 parsed
2026-08-31 11:29:19,730 [INFO] scraper: odds_win: 4/6 parsed
2026-08-31 11:29:19,730 [INFO] scraper: fetch_race 11/3: boats=6 odds=187/191
2026-08-31 11:29:19,734 [INFO] predictor: CALIBRATION_MODE=on
2026-08-31 11:29:19,734 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-08-31 11:29:19,738 [INFO] run_cycle: fetched 11/3 [scan]: 152 combos
2026-08-31 11:29:19,863 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 44
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 44
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 10, 'scan': 17}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_NO_ACTION: 48
  FINAL_MISSING: 47
  ANOMALY_SCRAPER_FAILURE_BURST: 41
  CIRCUIT_BREAKER_TRIP: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  ANOMALY_BET_VOLUME_DROP: 6
  CALIBRATION_DRIFT: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 8 | 11,700 | 8,520 | -3,180 | 0.728 |
| S01_NAKAANA1 | 34 | 8 | 6,800 | 3,680 | -3,120 | 0.541 |
| S02_TETSUBAN | 21 | 8 | 4,200 | 3,420 | -780 | 0.814 |

## 直近アラート (24h・新しい順)
```
[11:02:49] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:49] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:02:49] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[11:02:49] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:33:29] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3680, "roi_7d": 0.541, "sid": "S01_NAKAANA1"}
[10:01:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:20] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 3680, "roi_7d": 0.558, "sid": "S01_NAKAANA1"}
[10:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[10:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 117件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 27件 締切済
- 通知発射: scan=2 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 185R | win | 1 | 0.5070 | 3.1 | 1.57 | 200 | scan=- drift=- | 10:33:19 |
| S02_TETSUBAN | 079R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=- drift=- | 19:00:21 |
| S00 | 196R | win | 1 | 0.5123 | 5.5 | 2.82 | 300 | scan=- drift=- | 17:40:19 |
| S00 | 048R | win | 1 | 0.4111 | 12.4 | 5.10 | 300 | scan=4.8 drift=+158.3% | 15:19:25 |
| S00 | 0810R | win | 1 | 0.5891 | 4.5 | 2.65 | 300 | scan=14.0 drift=-67.9% | 15:07:19 |
| S01_NAKAANA1 | 099R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=3.0 drift=+33.3% | 14:30:30 |
| S00 | 099R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=- drift=- | 14:30:28 |
| S00 | 166R | win | 1 | 0.3177 | 11.2 | 3.56 | 300 | scan=5.2 drift=+115.4% | 13:49:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5123 | 2.3 | 1.18 | 200 | scan=- drift=- | 13:41:30 |
| S01_NAKAANA1 | 164R | win | 1 | 0.5476 | 3.0 | 1.64 | 200 | scan=- drift=- | 12:47:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +5.1% | -73.3% | +158.3% | 18 | 8 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.4s |
| **Latency** (scan→final max) | 654.7s |
| **Traffic** (notifications 24h) | 44 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 434 | 0.4726 | 0.2880 | +0.1845 | 🟡+39% | 0.2395 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4146 | 0.2695 | 0.2160 | 🔴-0.10 | 0.877 |
| S01_NAKAANA1 | win | 184 | 0.4909 | 0.2446 | 0.2506 | 🔴-0.36 | 0.747 |
| S02_TETSUBAN | win | 83 | 0.5486 | 0.4217 | 0.2621 | 🔴-0.07 | 0.722 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1232 | 0.1111 | ✅+0.0120 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 145 | 0.4094 | 0.2414 | 🔴+0.1680 |
| 0.50+ | 257 | 0.5457 | 0.3307 | 🔴+0.2150 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 225 | 0.745 |
| win | <10.0 | ✅learned | 109 | 0.458 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-31T11:30:01.464352+09:00_