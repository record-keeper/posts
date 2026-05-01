# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-01T22:20:01.806473+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×19 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×19 (24h)
- 🔴 CALIBRATION_DRIFT×10 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×9  [2026-05-01T22:11:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×13  [2026-05-01T22:07:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-01T22:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×36  [2026-05-01T21:44:22]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-01T21:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-05-01T20:30:36]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-05-01T17:39:43]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×24  [2026-05-01T13:00:49]
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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.53MB / last modified 2026-05-01T22:19:03.638215+09:00

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
d
2026-05-01 22:17:21,069 [INFO] scraper: odds2t: 30/30 parsed
2026-05-01 22:17:21,071 [INFO] scraper: odds2f: 15/15 parsed
2026-05-01 22:17:22,216 [INFO] scraper: odds_win: 6/6 parsed
2026-05-01 22:17:22,217 [INFO] scraper: fetch_race 24/11: boats=6 odds=191/191
2026-05-01 22:17:22,229 [INFO] predictor: CALIBRATION_MODE=on
2026-05-01 22:17:22,229 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-01 22:17:22,236 [INFO] run_cycle: fetched 24/11 [final]: 156 combos
2026-05-01 22:17:22,349 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-01 22:18:05,939 [INFO] run_cycle: === run_cycle 22:18:05 ===
2026-05-01 22:18:05,939 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-01 22:18:05,939 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-01 22:18:06,017 [INFO] predictor: Models loaded OK
2026-05-01 22:18:17,690 [INFO] scraper: odds3t: 120/120 parsed
2026-05-01 22:18:18,998 [INFO] scraper: odds3f: 20/20 parsed
2026-05-01 22:18:20,291 [INFO] scraper: odds2t: 30/30 parsed
2026-05-01 22:18:20,292 [INFO] scraper: odds2f: 15/15 parsed
2026-05-01 22:18:21,374 [INFO] scraper: odds_win: 6/6 parsed
2026-05-01 22:18:21,374 [INFO] scraper: fetch_race 24/11: boats=6 odds=191/191
2026-05-01 22:18:21,385 [INFO] predictor: CALIBRATION_MODE=on
2026-05-01 22:18:21,385 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-01 22:18:21,393 [INFO] run_cycle: fetched 24/11 [final]: 156 combos
2026-05-01 22:18:21,504 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-01 22:19:03,552 [INFO] run_cycle: === run_cycle 22:19:03 ===
2026-05-01 22:19:03,552 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-01 22:19:03,553 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-01 22:19:03,599 [INFO] predictor: Models loaded OK
2026-05-01 22:19:03,603 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 26
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 26
  }
]
```

## Phase別通知記録 (24h)
{'final': 8, 'result': 7, 'scan': 11}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 186
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_TRIP: 19
  CIRCUIT_BREAKER_NO_ACTION: 17
  CALIBRATION_DRIFT: 10
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 10 | 14,400 | 9,420 | -4,980 | 0.654 |

## 直近アラート (24h・新しい順)
```
[22:07:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[21:50:09] FINAL_MISSING: {"deadline": "2026-05-01T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050102041214", "sid": "S00"}
[21:39:05] CIRCUIT_BREAKER_TRIP: {"cost": 14400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 9420, "roi_7d": 0.654, "sid": "S00"}
[21:39:05] CALIBRATION_DRIFT: {"avg_actual": 0.2083, "avg_pred": 0.4333, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 48, "overconf_pct": 51.9}
[21:34:05] FINAL_MISSING: {"deadline": "2026-05-01T19:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050124041903", "sid": "S00"}
[21:31:05] FINAL_MISSING: {"deadline": "2026-05-01T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050103071356", "sid": "S00"}
[21:30:09] FINAL_MISSING: {"deadline": "2026-05-01T15:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050107021556", "sid": "S00"}
[21:29:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 505}
[21:28:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 508}
[21:27:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 512}
```

## 本日残レース: 1件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 179件 締切済
- 通知発射: scan=11 nid / final=8 nid / result=7 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1911R | win | 1 | 0.2290 | 7.6 | 1.74 | 300 | scan=- drift=- | 20:05:22 |
| S00 | 014R | win | 1 | 0.5476 | 7.1 | 3.89 | 300 | scan=12.0 drift=-40.8% | 16:29:44 |
| S00 | 012R | win | 1 | 0.5174 | 22.5 | 11.64 | 300 | scan=19.5 drift=+15.4% | 15:39:20 |
| S00 | 179R | win | 1 | 0.4111 | 10.1 | 4.15 | 300 | scan=- drift=- | 15:07:22 |
| S00 | 176R | win | 1 | 0.4111 | 11.3 | 4.65 | 300 | scan=5.2 drift=+117.3% | 13:24:20 |
| S00 | 021R | win | 1 | 0.2082 | 4.1 | 0.85 | 300 | scan=- drift=- | 10:45:32 |
| S00 | 111R | win | 1 | 0.5123 | 5.3 | 2.72 | 300 | scan=18.7 drift=-71.7% | 10:37:21 |
| S00 | 056R | win | 1 | 0.5735 | 5.4 | 3.10 | 300 | scan=- drift=- | 14:33:20 |
| S00 | 098R | win | 1 | 0.4111 | 5.9 | 2.43 | 300 | scan=15.8 drift=-62.7% | 13:50:35 |
| S00 | 149R | win | 1 | 0.2173 | 8.1 | 1.76 | 300 | scan=7.3 drift=+11.0% | 12:35:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 31 | +2.2% | -71.7% | +156.7% | 14 | 8 | 25 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 430.7s |
| **Latency** (scan→final max) | 599.9s |
| **Traffic** (notifications 24h) | 26 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 84 | 0.4340 | 0.2262 | +0.2078 | 🟡+48% | 0.2322 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 84 | 0.4340 | 0.2262 | 0.2322 | 🔴-0.33 | 0.779 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 5 | 0.2201 | 0.4000 | 🔴-0.1799 |
| 0.30-0.50 | 41 | 0.4292 | 0.1951 | 🔴+0.2341 |
| 0.50+ | 32 | 0.5335 | 0.2500 | 🔴+0.2835 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 12 | 0.496 |
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
_auto-generated by claude_snapshot.py at 2026-05-01T22:20:01.806473+09:00_