# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-11T10:00:01.809209+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×64 (24h)
- 🔴 CALIBRATION_DRIFT×30 (24h)
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-06-11T09:47:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×59  [2026-06-11T09:01:08]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×177  [2026-06-11T09:01:08]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×177  [2026-06-11T09:01:08]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×59  [2026-06-11T09:01:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-11T06:00:11]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S00: n=149 hit%=25.5% hit_CI[Bonf]=[16.7,36.9]% ROI=0.76 ROI_boot95=[0.50,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=28.3% hit_CI[Bonf]=[18.7,40.3]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=36.2% hit_CI[Bonf]=[22.7,52.4]% ROI=0.61 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-11T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=32.4% ROI=0.89 (コスト 10,000/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-11T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=20.0% ROI=0.42 (コスト 7,700/回収 3,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.8MB / last modified 2026-06-11T10:00:05.887746+09:00

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
[INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 09:57:06,503 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 09:57:06,553 [INFO] predictor: Models loaded OK
2026-06-11 09:57:17,588 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=14&hd=20260611: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-11 09:57:30,182 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 09:57:31,304 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 09:57:32,447 [INFO] scraper: odds2t: 30/30 parsed
2026-06-11 09:57:32,448 [INFO] scraper: odds2f: 15/15 parsed
2026-06-11 09:57:33,542 [INFO] scraper: odds_win: 5/6 parsed
2026-06-11 09:57:33,543 [INFO] scraper: fetch_race 14/4: boats=6 odds=190/191
2026-06-11 09:57:33,555 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 09:57:33,555 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-11 09:57:33,563 [INFO] run_cycle: fetched 14/4 [scan]: 155 combos
2026-06-11 09:57:33,690 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 09:58:06,354 [INFO] run_cycle: === run_cycle 09:58:06 ===
2026-06-11 09:58:06,355 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 09:58:06,355 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 09:58:06,399 [INFO] predictor: Models loaded OK
2026-06-11 09:58:06,495 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 09:59:05,338 [INFO] run_cycle: === run_cycle 09:59:05 ===
2026-06-11 09:59:05,338 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 09:59:05,338 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 09:59:05,381 [INFO] predictor: Models loaded OK
2026-06-11 09:59:05,582 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 9, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 86
  CIRCUIT_BREAKER_TRIP: 64
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 30
  FINAL_MISSING: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 8 | 11,400 | 6,090 | -5,310 | 0.534 |
| S01_NAKAANA1 | 29 | 7 | 5,800 | 3,040 | -2,760 | 0.524 |
| S02_TETSUBAN | 26 | 5 | 5,200 | 1,560 | -3,640 | 0.3 |

## 直近アラート (24h・新しい順)
```
[09:54:31] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 6090, "roi_7d": 0.534, "sid": "S00"}
[09:54:31] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.143, "baseline_mean": 0.857, "baseline_stdev": 0.062, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.3}
[09:53:06] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 6090, "roi_7d": 0.549, "sid": "S00"}
[09:53:06] CALIBRATION_DRIFT: {"avg_actual": 0.2174, "avg_pred": 0.4888, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 55.5}
[09:47:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.19, "baseline_mean": 0.857, "baseline_stdev": 0.062, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -3.07}
[09:21:43] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 5370, "roi_7d": 0.484, "sid": "S00"}
[09:01:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:06] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1560, "roi_7d": 0.3, "sid": "S02_TETSUBAN"}
[09:01:06] CIRCUIT_BREAKER_TRIP: {"cost": 5800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 3040, "roi_7d": 0.524, "sid": "S01_NAKAANA1"}
[09:01:06] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 5370, "roi_7d": 0.497, "sid": "S00"}
```

## 本日残レース: 133件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 11件 締切済
- 通知発射: scan=3 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 234R | win | 1 | 0.4111 | 7.9 | 3.25 | 300 | scan=5.9 drift=+33.9% | 09:54:22 |
| S00 | 103R | win | 1 | 0.5891 | 12.7 | 7.48 | 300 | scan=12.7 drift=+0.0% | 09:21:33 |
| S02_TETSUBAN | 0710R | win | 1 | 0.5509 | 2.5 | 1.38 | 200 | scan=2.8 drift=-10.7% | 19:47:21 |
| S01_NAKAANA1 | 0610R | win | 1 | 0.5719 | 3.4 | 1.94 | 200 | scan=- drift=- | 16:04:21 |
| S00 | 055R | win | 1 | 0.5334 | 10.1 | 5.39 | 300 | scan=16.5 drift=-38.8% | 13:28:21 |
| S00 | 117R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=7.5 drift=+0.0% | 13:24:23 |
| S02_TETSUBAN | 136R | win | 1 | 0.4111 | 2.6 | 1.07 | 200 | scan=2.1 drift=+23.8% | 13:02:23 |
| S02_TETSUBAN | 053R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=- drift=- | 12:29:20 |
| S01_NAKAANA1 | 239R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=4.6 drift=-17.4% | 12:15:22 |
| S02_TETSUBAN | 132R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.8 drift=-10.7% | 10:59:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +9.2% | -62.9% | +274.6% | 17 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 487.8s |
| **Latency** (scan→final max) | 606.3s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 367 | 0.4694 | 0.2916 | +0.1778 | 🟡+38% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 149 | 0.4205 | 0.2617 | 0.2190 | 🔴-0.13 | 0.776 |
| S01_NAKAANA1 | win | 138 | 0.4877 | 0.2826 | 0.2427 | 🔴-0.20 | 0.707 |
| S02_TETSUBAN | win | 80 | 0.5288 | 0.3625 | 0.2613 | 🔴-0.13 | 0.61 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1918 | 0.2000 | ✅-0.0082 |
| 0.20-0.30 | 5 | 0.2225 | 0.4000 | 🔴-0.1775 |
| 0.30-0.50 | 138 | 0.4203 | 0.2246 | 🔴+0.1957 |
| 0.50+ | 205 | 0.5413 | 0.3512 | 🔴+0.1901 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 35 | 0.736 |
| win | <5.0 | ✅learned | 66 | 0.72 |
| win | <10.0 | ✅learned | 42 | 0.51 |
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
_auto-generated by claude_snapshot.py at 2026-06-11T10:00:01.809209+09:00_