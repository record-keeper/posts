# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-01T11:50:01.920861+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×62 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 CALIBRATION_DRIFT×4 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-05-01T11:43:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-01T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-05-01T11:02:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×47  [2026-05-01T11:02:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×37  [2026-05-01T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-01T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=6 pred=0.3241 actual=0.0000 gap=+0.3241`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-01T06:00:09]
- key: `ROI_STAT|S00: n=77 hit%=22.1% hit_CI[Bonf]=[11.6,38.1]% ROI=0.73 ROI_boot95=[0.38,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-01T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-01T06:00:09]
- key: `ORPHAN_SCAN|66 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-01T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=77 pred=0.4366 actual=0.2208 error=+0.2158 (+49%) brier=0.2223 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-01T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=77 pred=0.4366 hit=0.2208 cal_err=+0.2158 brier=0.2223 BSS=-0.29 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-01T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=33 pred=0.4494 actual=0.2424 gap=+0.2070`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-01T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.50+: n=29 pred=0.5344 actual=0.2759 gap=+0.2585`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=931 bet=300 odds=5.9 payout=450 ratio=0.25`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-01T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=943 bet=300 odds=5.9 payout=510 ratio=0.29`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.51MB / last modified 2026-05-01T11:49:29.711681+09:00

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
rsed
2026-05-01 11:48:53,349 [INFO] scraper: fetch_race 18/8: boats=6 odds=181/191
2026-05-01 11:48:53,357 [INFO] predictor: CALIBRATION_MODE=on
2026-05-01 11:48:53,357 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-05-01 11:48:53,365 [INFO] run_cycle: fetched 18/8 [scan]: 149 combos
2026-05-01 11:48:53,482 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-01 11:49:05,633 [INFO] run_cycle: === run_cycle 11:49:05 ===
2026-05-01 11:49:05,633 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-01 11:49:05,633 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-01 11:49:05,679 [INFO] predictor: Models loaded OK
2026-05-01 11:49:18,532 [INFO] scraper: odds3t: 120/120 parsed
2026-05-01 11:49:19,633 [INFO] scraper: odds3f: 20/20 parsed
2026-05-01 11:49:20,709 [INFO] scraper: odds2t: 30/30 parsed
2026-05-01 11:49:20,710 [INFO] scraper: odds2f: 13/15 parsed
2026-05-01 11:49:21,843 [INFO] scraper: odds_win: 6/6 parsed
2026-05-01 11:49:21,843 [INFO] scraper: fetch_race 23/8: boats=6 odds=189/191
2026-05-01 11:49:21,854 [INFO] predictor: CALIBRATION_MODE=on
2026-05-01 11:49:21,855 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-01 11:49:21,862 [INFO] run_cycle: fetched 23/8 [final]: 156 combos
2026-05-01 11:49:25,779 [INFO] scraper: odds3t: 120/120 parsed
2026-05-01 11:49:26,932 [INFO] scraper: odds3f: 20/20 parsed
2026-05-01 11:49:28,231 [INFO] scraper: odds2t: 30/30 parsed
2026-05-01 11:49:28,233 [INFO] scraper: odds2f: 15/15 parsed
2026-05-01 11:49:29,429 [INFO] scraper: odds_win: 4/6 parsed
2026-05-01 11:49:29,429 [INFO] scraper: fetch_race 05/1: boats=6 odds=189/191
2026-05-01 11:49:29,439 [INFO] predictor: CALIBRATION_MODE=on
2026-05-01 11:49:29,439 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-01 11:49:29,447 [INFO] run_cycle: fetched 05/1 [scan]: 154 combos
2026-05-01 11:49:29,561 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 29
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 29
  }
]
```

## Phase別通知記録 (24h)
{'final': 9, 'result': 7, 'scan': 13}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 62
  ANOMALY_SCRAPER_FAILURE_BURST: 23
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  CALIBRATION_DRIFT: 4
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 12 | 15,600 | 12,150 | -3,450 | 0.779 |

## 直近アラート (24h・新しい順)
```
[11:49:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1031}
[11:48:53] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1015}
[11:47:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1039}
[11:46:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1033}
[11:45:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1038}
[11:44:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[11:43:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1047}
[11:20:25] FINAL_MISSING: {"deadline": "2026-05-01T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050123040950", "sid": "S00"}
[11:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:45:41] CIRCUIT_BREAKER_TRIP: {"cost": 16200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 54, "payout": 10710, "roi_7d": 0.661, "sid": "S00"}
```

## 本日残レース: 145件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 35件 締切済
- 通知発射: scan=2 nid / final=2 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 021R | win | 1 | 0.2082 | 4.1 | 0.85 | 300 | scan=- drift=- | 10:45:32 |
| S00 | 111R | win | 1 | 0.5123 | 5.3 | 2.72 | 300 | scan=18.7 drift=-71.7% | 10:37:21 |
| S00 | 056R | win | 1 | 0.5735 | 5.4 | 3.10 | 300 | scan=- drift=- | 14:33:20 |
| S00 | 098R | win | 1 | 0.4111 | 5.9 | 2.43 | 300 | scan=15.8 drift=-62.7% | 13:50:35 |
| S00 | 149R | win | 1 | 0.2173 | 8.1 | 1.76 | 300 | scan=7.3 drift=+11.0% | 12:35:22 |
| S00 | 174R | win | 1 | 0.4989 | 17.1 | 8.53 | 300 | scan=- drift=- | 12:13:46 |
| S00 | 093R | win | 1 | 0.4989 | 9.0 | 4.49 | 300 | scan=6.7 drift=+34.3% | 11:22:21 |
| S00 | 172R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=8.1 drift=-3.7% | 11:07:46 |
| S00 | 1810R | win | 1 | 0.4111 | 5.5 | 2.26 | 300 | scan=- drift=- | 12:55:21 |
| S00 | 033R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=4.3 drift=+55.8% | 12:05:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 33 | +5.9% | -71.7% | +156.7% | 14 | 8 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 533.1s |
| **Latency** (scan→final max) | 610.7s |
| **Traffic** (notifications 24h) | 29 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 79 | 0.4347 | 0.2278 | +0.2068 | 🟡+48% | 0.2279 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 79 | 0.4347 | 0.2278 | 0.2279 | 🔴-0.30 | 0.809 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 39 | 0.4301 | 0.2051 | 🔴+0.2250 |
| 0.50+ | 30 | 0.5336 | 0.2667 | 🔴+0.2670 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 11 | 0.523 |
| win | <20.0 | ⚠️fallback | 2 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-01T11:50:01.920861+09:00_