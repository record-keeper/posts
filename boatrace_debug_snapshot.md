# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-30T12:30:02.179003+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×24 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 CALIBRATION_DRIFT×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-04-30T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×28  [2026-04-30T12:02:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-04-30T12:02:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CALIBRATION_DRIFT  ×50  [2026-04-30T11:40:25]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-04-30T11:04:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×22  [2026-04-30T11:00:49]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-04-30T06:00:08]
- key: `ROI_STAT|S00: n=71 hit%=22.5% hit_CI[Bonf]=[11.6,39.3]% ROI=0.77 ROI_boot95=[0.41,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-30T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-30T06:00:08]
- key: `ORPHAN_SCAN|59 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-30T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=71 pred=0.4368 actual=0.2254 error=+0.2114 (+48%) brier=0.2215 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-30T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=71 pred=0.4368 hit=0.2254 cal_err=+0.2114 brier=0.2215 BSS=-0.27 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-30T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=6 pred=0.3241 actual=0.0000 gap=+0.3241`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-30T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=29 pred=0.4486 actual=0.2414 gap=+0.2073`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-30T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=28 pred=0.5330 actual=0.2857 gap=+0.2472`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-30T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=931 bet=300 odds=5.9 payout=450 ratio=0.25`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.48MB / last modified 2026-04-30T12:30:03.890414+09:00

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
odels loaded OK
2026-04-30 12:28:15,798 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=4
2026-04-30 12:28:15,799 [WARNING] run_cycle: fetch None: 03/4
2026-04-30 12:28:19,388 [INFO] scraper: odds3t: 120/120 parsed
2026-04-30 12:28:20,497 [INFO] scraper: odds3f: 20/20 parsed
2026-04-30 12:28:21,595 [INFO] scraper: odds2t: 30/30 parsed
2026-04-30 12:28:21,596 [INFO] scraper: odds2f: 15/15 parsed
2026-04-30 12:28:22,835 [INFO] scraper: odds_win: 5/6 parsed
2026-04-30 12:28:22,836 [INFO] scraper: fetch_race 14/9: boats=6 odds=190/191
2026-04-30 12:28:22,847 [INFO] predictor: CALIBRATION_MODE=on
2026-04-30 12:28:22,847 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-30 12:28:22,855 [INFO] run_cycle: fetched 14/9 [scan]: 155 combos
2026-04-30 12:28:22,998 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 12:29:05,608 [INFO] run_cycle: === run_cycle 12:29:05 ===
2026-04-30 12:29:05,609 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 12:29:05,609 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 12:29:05,691 [INFO] predictor: Models loaded OK
2026-04-30 12:29:16,208 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=4
2026-04-30 12:29:16,208 [WARNING] run_cycle: fetch None: 03/4
2026-04-30 12:29:19,780 [INFO] scraper: odds3t: 120/120 parsed
2026-04-30 12:29:20,947 [INFO] scraper: odds3f: 20/20 parsed
2026-04-30 12:29:22,092 [INFO] scraper: odds2t: 30/30 parsed
2026-04-30 12:29:22,093 [INFO] scraper: odds2f: 15/15 parsed
2026-04-30 12:29:23,188 [INFO] scraper: odds_win: 6/6 parsed
2026-04-30 12:29:23,189 [INFO] scraper: fetch_race 06/3: boats=6 odds=191/191
2026-04-30 12:29:23,201 [INFO] predictor: CALIBRATION_MODE=on
2026-04-30 12:29:23,201 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-30 12:29:23,208 [INFO] run_cycle: fetched 06/3 [scan]: 156 combos
2026-04-30 12:29:23,304 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 32
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 32
  }
]
```

## Phase別通知記録 (24h)
{'final': 11, 'result': 4, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 259
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  CALIBRATION_DRIFT: 8
  ANOMALY_BET_VOLUME_DROP: 3
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 11 | 15,600 | 10,200 | -5,400 | 0.654 |

## 直近アラート (24h・新しい順)
```
[12:24:30] FINAL_MISSING: {"deadline": "2026-04-30T10:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043021061054", "sid": "S00"}
[12:13:47] CIRCUIT_BREAKER_TRIP: {"cost": 15600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 10200, "roi_7d": 0.654, "sid": "S00"}
[12:02:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:55:24] CALIBRATION_DRIFT: {"avg_actual": 0.2157, "avg_pred": 0.446, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 51, "overconf_pct": 51.6}
[11:40:25] CALIBRATION_DRIFT: {"avg_actual": 0.22, "avg_pred": 0.4449, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 50, "overconf_pct": 50.6}
[11:24:05] FINAL_MISSING: {"deadline": "2026-04-30T10:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043021061054", "sid": "S00"}
[11:22:22] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 10200, "roi_7d": 0.667, "sid": "S00"}
[11:22:22] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 34.3, "final": 9.0, "kind": "LARGE_ODDS_DRIFT", "race": "093R", "scan": 6.7, "sid": "S00"}
[11:07:55] CIRCUIT_BREAKER_TRIP: {"cost": 15000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 10200, "roi_7d": 0.68, "sid": "S00"}
[11:07:55] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.9, "baseline_n_days": 7, "baseline_stdev": 0.7, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 1, "z_score": -2.69}
```

## 本日残レース: 118件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 50件 締切済
- 通知発射: scan=7 nid / final=5 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 174R | win | 1 | 0.4989 | 17.1 | 8.53 | 300 | scan=- drift=- | 12:13:46 |
| S00 | 093R | win | 1 | 0.4989 | 9.0 | 4.49 | 300 | scan=6.7 drift=+34.3% | 11:22:21 |
| S00 | 172R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=8.1 drift=-3.7% | 11:07:46 |
| S00 | 1810R | win | 1 | 0.4111 | 5.5 | 2.26 | 300 | scan=- drift=- | 12:55:21 |
| S00 | 033R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=4.3 drift=+55.8% | 12:05:21 |
| S00 | 032R | win | 1 | 0.3177 | 8.8 | 2.80 | 300 | scan=- drift=- | 11:38:19 |
| S00 | 187R | win | 1 | 0.3177 | 14.7 | 4.67 | 300 | scan=16.6 drift=-11.4% | 11:16:20 |
| S00 | 145R | win | 1 | 0.2173 | 10.1 | 2.19 | 300 | scan=13.0 drift=-22.3% | 10:29:20 |
| S00 | 185R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=5.2 drift=+36.5% | 10:14:32 |
| S00 | 152R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=12.7 drift=+0.0% | 15:48:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 35 | +8.6% | -63.7% | +156.7% | 16 | 8 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 407.5s |
| **Latency** (scan→final max) | 599.8s |
| **Traffic** (notifications 24h) | 32 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 73 | 0.4373 | 0.2192 | +0.2181 | 🟡+50% | 0.2211 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 73 | 0.4373 | 0.2192 | 0.2211 | 🔴-0.29 | 0.745 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 37 | 0.4288 | 0.1892 | 🔴+0.2396 |
| 0.50+ | 28 | 0.5330 | 0.2857 | 🔴+0.2472 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 4 | 0.35 |
| win | <10.0 | ✅learned | 10 | 0.546 |
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
_auto-generated by claude_snapshot.py at 2026-04-30T12:30:02.179003+09:00_