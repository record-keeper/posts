# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-07T12:10:01.273748+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×85 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-09-07T12:03:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×7  [2026-09-07T12:03:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-09-07T12:03:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×8  [2026-09-07T11:53:38]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-09-07T11:43:04]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-07T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×32  [2026-09-07T10:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-07T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-07T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-07T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-07T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=42 pred=0.3214 actual=0.2619 gap=+0.0595`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-07T06:00:14]
- key: `ROI_STAT|S00: n=187 hit%=28.3% hit_CI[Bonf]=[19.9,38.6]% ROI=0.95 ROI_boot95=[0.68,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-07T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=22.8% hit_CI[Bonf]=[15.3,32.5]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-07T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=89 hit%=38.2% hit_CI[Bonf]=[25.0,53.5]% ROI=0.64 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-07T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=89<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-07T06:00:14]
- key: `ORPHAN_SCAN|207 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-07T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=16.2% ROI=0.42 (コスト 10,600/回収 4,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-07T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.90 (コスト 10,000/回収 9,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-07T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=104 hit%=27.9% ROI=0.97 (コスト 24,000/回収 23,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-07T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=52 hit%=21.2% ROI=0.44 (コスト 11,400/回収 4,960)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.58MB / last modified 2026-09-07T12:09:24.112067+09:00

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
=== run_cycle 12:08:04 ===
2026-09-07 12:08:04,964 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-07 12:08:04,964 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-07 12:08:04,997 [INFO] predictor: Models loaded OK
2026-09-07 12:08:17,887 [INFO] scraper: odds3t: 120/120 parsed
2026-09-07 12:08:19,075 [INFO] scraper: odds3f: 20/20 parsed
2026-09-07 12:08:20,200 [INFO] scraper: odds2t: 30/30 parsed
2026-09-07 12:08:20,201 [INFO] scraper: odds2f: 12/15 parsed
2026-09-07 12:08:21,311 [INFO] scraper: odds_win: 3/6 parsed
2026-09-07 12:08:21,311 [INFO] scraper: fetch_race 22/2: boats=6 odds=185/191
2026-09-07 12:08:21,316 [INFO] predictor: CALIBRATION_MODE=on
2026-09-07 12:08:21,316 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-07 12:08:21,321 [INFO] run_cycle: fetched 22/2 [scan]: 153 combos
2026-09-07 12:08:21,456 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-07 12:09:04,654 [INFO] run_cycle: === run_cycle 12:09:04 ===
2026-09-07 12:09:04,654 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-07 12:09:04,654 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-07 12:09:04,704 [INFO] predictor: Models loaded OK
2026-09-07 12:09:17,590 [INFO] scraper: odds3t: 120/120 parsed
2026-09-07 12:09:18,693 [INFO] scraper: odds3f: 20/20 parsed
2026-09-07 12:09:19,923 [INFO] scraper: odds2t: 30/30 parsed
2026-09-07 12:09:19,924 [INFO] scraper: odds2f: 15/15 parsed
2026-09-07 12:09:21,136 [INFO] scraper: odds_win: 3/6 parsed
2026-09-07 12:09:21,136 [INFO] scraper: fetch_race 04/4: boats=6 odds=188/191
2026-09-07 12:09:21,140 [INFO] predictor: CALIBRATION_MODE=on
2026-09-07 12:09:21,140 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-07 12:09:21,144 [INFO] run_cycle: fetched 04/4 [scan]: 153 combos
2026-09-07 12:09:21,285 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 70
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 70
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 13, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 136
  FINAL_MISSING: 85
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 12
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 15 | 15,000 | 15,780 | +780 | 1.052 |
| S01_NAKAANA1 | 46 | 6 | 9,200 | 2,780 | -6,420 | 0.302 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,440 | -1,360 | 0.514 |

## 直近アラート (24h・新しい順)
```
[12:07:04] FINAL_MISSING: {"deadline": "2026-09-07T11:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090711031137", "sid": "S00"}
[12:01:30] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:30] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:58:30] FINAL_MISSING: {"deadline": "2026-09-07T10:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090714051028", "sid": "S00"}
[11:53:37] CALIBRATION_DRIFT: {"avg_actual": 0.2407, "avg_pred": 0.4819, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 108, "overconf_pct": 50.0}
[11:38:29] CIRCUIT_BREAKER_TRIP: {"cost": 9200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 2780, "roi_7d": 0.302, "sid": "S01_NAKAANA1"}
[11:38:29] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -16.2, "final": 3.1, "kind": "LARGE_ODDS_DRIFT", "race": "032R", "scan": 3.7, "sid": "S01_NAKAANA1"}
[11:38:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.41, "baseline_mean": 0.81, "baseline_stdev": 0.119, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -3.46}
[11:31:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.61, "baseline_mean": 0.81, "baseline_stdev": 0.119, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.2, "today_scan_count": 5, "z_score": -5.14}
[11:27:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.56, "baseline_mean": 0.81, "baseline_stdev": 0.119, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 4, "z_score": -4.72}
```

## 本日残レース: 107件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 37件 締切済
- 通知発射: scan=5 nid / final=5 nid / result=2 nid
- predictions: 5 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 033R | win | 1 | 0.3177 | 5.4 | 1.72 | 300 | scan=- drift=- | 12:05:19 |
| S00 | 163R | win | 1 | 0.4111 | 10.5 | 4.32 | 300 | scan=- drift=- | 11:56:43 |
| S01_NAKAANA1 | 032R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=3.7 drift=-16.2% | 11:38:19 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=- drift=- | 11:21:30 |
| S00 | 111R | win | 1 | 0.4111 | 13.5 | 5.55 | 300 | scan=25.5 drift=-47.1% | 10:32:20 |
| S02_TETSUBAN | 079R | win | 1 | 0.5719 | 2.0 | 1.14 | 200 | scan=2.1 drift=-4.8% | 19:11:19 |
| S01_NAKAANA1 | 019R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=- drift=- | 18:51:18 |
| S01_NAKAANA1 | 078R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.0 drift=+0.0% | 18:40:20 |
| S02_TETSUBAN | 074R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=- drift=- | 16:49:30 |
| S00 | 014R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=6.0 drift=+86.7% | 16:30:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 65 | +5.7% | -75.5% | +137.8% | 17 | 10 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 463.9s |
| **Latency** (scan→final max) | 652.2s |
| **Traffic** (notifications 24h) | 70 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 468 | 0.4762 | 0.2799 | +0.1963 | 🟡+41% | 0.2412 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4297 | 0.2849 | 0.2231 | 🔴-0.09 | 0.958 |
| S01_NAKAANA1 | win | 194 | 0.4890 | 0.2268 | 0.2481 | 🔴-0.41 | 0.679 |
| S02_TETSUBAN | win | 88 | 0.5465 | 0.3864 | 0.2644 | 🔴-0.12 | 0.645 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1302 | 0.0000 | 🔴+0.1302 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2264 | 0.2222 | ✅+0.0042 |
| 0.30-0.50 | 159 | 0.4054 | 0.2327 | 🔴+0.1727 |
| 0.50+ | 282 | 0.5452 | 0.3156 | 🔴+0.2295 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 131 | 0.772 |
| win | <5.0 | ✅learned | 237 | 0.738 |
| win | <10.0 | ✅learned | 117 | 0.47 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-07T12:10:01.273748+09:00_