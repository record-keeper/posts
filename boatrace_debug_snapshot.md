# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-07T11:10:01.952987+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×71 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×71 (24h)
- 🔴 CALIBRATION_DRIFT×29 (24h)
- 🟡 FINAL_MISSING×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×9  [2026-06-07T11:01:45]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×27  [2026-06-07T11:01:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×27  [2026-06-07T11:01:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×9  [2026-06-07T11:01:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×44  [2026-06-07T10:13:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-06-07T09:21:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2201 actual=0.4000 gap=-0.1799`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=25.0% ROI=0.96 (コスト 8,200/回収 7,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 8,400/回収 4,750)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S00: n=156 hit%=26.3% hit_CI[Bonf]=[17.5,37.5]% ROI=0.78 ROI_boot95=[0.54,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=133 hit%=28.6% hit_CI[Bonf]=[18.8,40.9]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=133<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=40.3% hit_CI[Bonf]=[25.9,56.6]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.54MB / last modified 2026-06-07T11:09:06.147565+09:00

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
== run_cycle 11:08:05 ===
2026-06-07 11:08:05,265 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-07 11:08:05,265 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-07 11:08:05,309 [INFO] predictor: Models loaded OK
2026-06-07 11:08:17,780 [INFO] scraper: odds3t: 120/120 parsed
2026-06-07 11:08:18,880 [INFO] scraper: odds3f: 20/20 parsed
2026-06-07 11:08:20,048 [INFO] scraper: odds2t: 30/30 parsed
2026-06-07 11:08:20,049 [INFO] scraper: odds2f: 15/15 parsed
2026-06-07 11:08:21,170 [INFO] scraper: odds_win: 6/6 parsed
2026-06-07 11:08:21,170 [INFO] scraper: fetch_race 17/2: boats=6 odds=191/191
2026-06-07 11:08:21,182 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 11:08:21,182 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-07 11:08:21,194 [INFO] run_cycle: fetched 17/2 [final]: 156 combos
2026-06-07 11:08:24,887 [INFO] scraper: odds3t: 120/120 parsed
2026-06-07 11:08:25,986 [INFO] scraper: odds3f: 20/20 parsed
2026-06-07 11:08:27,063 [INFO] scraper: odds2t: 29/30 parsed
2026-06-07 11:08:27,064 [INFO] scraper: odds2f: 13/15 parsed
2026-06-07 11:08:28,186 [INFO] scraper: odds_win: 6/6 parsed
2026-06-07 11:08:28,187 [INFO] scraper: fetch_race 03/1: boats=6 odds=188/191
2026-06-07 11:08:28,196 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 11:08:28,198 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-06-07 11:08:28,204 [INFO] run_cycle: fetched 03/1 [scan]: 155 combos
2026-06-07 11:08:28,475 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-07 11:09:05,598 [INFO] run_cycle: === run_cycle 11:09:05 ===
2026-06-07 11:09:05,598 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-07 11:09:05,598 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-07 11:09:05,647 [INFO] predictor: Models loaded OK
2026-06-07 11:09:05,915 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  CIRCUIT_BREAKER_TRIP: 71
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 29
  FINAL_MISSING: 24
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 4 | 8,700 | 2,220 | -6,480 | 0.255 |
| S01_NAKAANA1 | 23 | 2 | 4,600 | 580 | -4,020 | 0.126 |
| S02_TETSUBAN | 25 | 7 | 5,000 | 1,880 | -3,120 | 0.376 |

## 直近アラート (24h・新しい順)
```
[11:07:37] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 2220, "roi_7d": 0.255, "sid": "S00"}
[11:07:37] CALIBRATION_DRIFT: {"avg_actual": 0.1733, "avg_pred": 0.4857, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 75, "overconf_pct": 64.3}
[11:01:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:45] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 580, "roi_7d": 0.126, "sid": "S01_NAKAANA1"}
[11:01:45] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 2940, "roi_7d": 0.327, "sid": "S00"}
[11:01:45] CALIBRATION_DRIFT: {"avg_actual": 0.1842, "avg_pred": 0.4835, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 76, "overconf_pct": 61.9}
[11:01:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[11:01:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:01:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:57:29] CIRCUIT_BREAKER_TRIP: {"cost": 4800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 24, "payout": 1500, "roi_7d": 0.312, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 132件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 24件 締切済
- 通知発射: scan=5 nid / final=5 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 186R | win | 1 | 0.5174 | 4.7 | 2.43 | 200 | scan=4.7 drift=+0.0% | 10:57:20 |
| S00 | 082R | win | 1 | 0.5891 | 25.1 | 14.79 | 300 | scan=6.7 drift=+274.6% | 10:55:22 |
| S02_TETSUBAN | 213R | win | 1 | 0.5476 | 2.1 | 1.15 | 200 | scan=- drift=- | 09:22:21 |
| S02_TETSUBAN | 0712R | win | 1 | 0.5735 | 2.6 | 1.49 | 200 | scan=- drift=- | 20:43:45 |
| S01_NAKAANA1 | 0710R | win | 1 | 0.4989 | 4.0 | 2.00 | 200 | scan=- drift=- | 19:48:20 |
| S00 | 0710R | win | 1 | 0.4989 | 14.1 | 7.03 | 300 | scan=23.8 drift=-40.8% | 19:47:21 |
| S02_TETSUBAN | 079R | win | 1 | 0.5476 | 2.1 | 1.15 | 200 | scan=- drift=- | 19:20:35 |
| S00 | 078R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=8.2 drift=-31.7% | 18:51:21 |
| S00 | 243R | win | 1 | 0.5123 | 4.4 | 2.25 | 300 | scan=4.4 drift=+0.0% | 18:31:21 |
| S00 | 1811R | win | 1 | 0.4111 | 7.9 | 3.25 | 300 | scan=- drift=- | 13:36:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 41 | +14.4% | -62.9% | +432.7% | 16 | 8 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 462.6s |
| **Latency** (scan→final max) | 617.2s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 366 | 0.4658 | 0.3005 | +0.1653 | 🟡+36% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 155 | 0.4217 | 0.2581 | 0.2206 | 🔴-0.15 | 0.775 |
| S01_NAKAANA1 | win | 133 | 0.4835 | 0.2857 | 0.2424 | 🔴-0.19 | 0.714 |
| S02_TETSUBAN | win | 78 | 0.5233 | 0.4103 | 0.2612 | 🔴-0.08 | 0.731 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 5 | 0.2201 | 0.4000 | 🔴-0.1799 |
| 0.30-0.50 | 151 | 0.4191 | 0.2450 | 🔴+0.1740 |
| 0.50+ | 192 | 0.5417 | 0.3594 | 🔴+0.1823 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 32 | 0.741 |
| win | <5.0 | ✅learned | 59 | 0.732 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 12 | 0.197 |
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
_auto-generated by claude_snapshot.py at 2026-06-07T11:10:01.952987+09:00_