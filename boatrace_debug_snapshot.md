# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-30T11:10:01.608508+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 CALIBRATION_DRIFT×10 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-04-30T11:04:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×8  [2026-04-30T11:02:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×8  [2026-04-30T11:02:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-04-30T11:00:49]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-04-30T10:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

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

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×55  [2026-04-29T19:35:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.47MB / last modified 2026-04-30T11:09:06.343086+09:00

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
]: 156 combos
2026-04-30 11:07:54,996 [INFO] run_cycle: run_cycle done: 1 notifications
2026-04-30 11:08:05,695 [INFO] run_cycle: === run_cycle 11:08:05 ===
2026-04-30 11:08:05,695 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 11:08:05,696 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 11:08:05,761 [INFO] predictor: Models loaded OK
2026-04-30 11:08:16,877 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=17&hd=20260430: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-04-30 11:08:27,933 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=17&hd=20260430: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-04-30 11:08:42,504 [INFO] scraper: odds3t: 120/120 parsed
2026-04-30 11:08:43,842 [INFO] scraper: odds3f: 20/20 parsed
2026-04-30 11:08:44,979 [INFO] scraper: odds2t: 30/30 parsed
2026-04-30 11:08:44,980 [INFO] scraper: odds2f: 14/15 parsed
2026-04-30 11:08:46,096 [INFO] scraper: odds_win: 6/6 parsed
2026-04-30 11:08:46,096 [INFO] scraper: fetch_race 17/2: boats=6 odds=190/191
2026-04-30 11:08:46,099 [INFO] predictor: CALIBRATION_MODE=on
2026-04-30 11:08:46,099 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-30 11:08:46,103 [INFO] run_cycle: fetched 17/2 [final]: 156 combos
2026-04-30 11:08:46,413 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 11:09:05,664 [INFO] run_cycle: === run_cycle 11:09:05 ===
2026-04-30 11:09:05,664 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 11:09:05,666 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 11:09:05,734 [INFO] predictor: Models loaded OK
2026-04-30 11:09:06,180 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 11, 'result': 4, 'scan': 14}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 306
  FINAL_MISSING: 54
  CIRCUIT_BREAKER_TRIP: 26
  CIRCUIT_BREAKER_NO_ACTION: 17
  CALIBRATION_DRIFT: 10
  ANOMALY_BET_VOLUME_DROP: 3
  ANOMALY_BET_VOLUME_SPIKE: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 11 | 15,000 | 10,200 | -4,800 | 0.68 |

## 直近アラート (24h・新しい順)
```
[11:07:55] CIRCUIT_BREAKER_TRIP: {"cost": 15000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 10200, "roi_7d": 0.68, "sid": "S00"}
[11:07:55] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.9, "baseline_n_days": 7, "baseline_stdev": 0.7, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 1, "z_score": -2.69}
[11:04:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.279, "baseline_mean": 0.612, "baseline_stdev": 0.132, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -2.11}
[11:02:06] CIRCUIT_BREAKER_TRIP: {"cost": 14700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 10200, "roi_7d": 0.694, "sid": "S00"}
[11:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:00:49] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.9, "baseline_n_days": 7, "baseline_stdev": 0.7, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -4.14}
[10:02:05] CIRCUIT_BREAKER_TRIP: {"cost": 14700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 10200, "roi_7d": 0.694, "sid": "S00"}
[10:02:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:00:09] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.6, "baseline_n_days": 5, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.92}
[09:01:41] CIRCUIT_BREAKER_TRIP: {"cost": 14700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 10200, "roi_7d": 0.694, "sid": "S00"}
```

## 本日残レース: 143件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 25件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 172R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=8.1 drift=-3.7% | 11:07:46 |
| S00 | 1810R | win | 1 | 0.4111 | 5.5 | 2.26 | 300 | scan=- drift=- | 12:55:21 |
| S00 | 033R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=4.3 drift=+55.8% | 12:05:21 |
| S00 | 032R | win | 1 | 0.3177 | 8.8 | 2.80 | 300 | scan=- drift=- | 11:38:19 |
| S00 | 187R | win | 1 | 0.3177 | 14.7 | 4.67 | 300 | scan=16.6 drift=-11.4% | 11:16:20 |
| S00 | 145R | win | 1 | 0.2173 | 10.1 | 2.19 | 300 | scan=13.0 drift=-22.3% | 10:29:20 |
| S00 | 185R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=5.2 drift=+36.5% | 10:14:32 |
| S00 | 152R | win | 1 | 0.4989 | 12.7 | 6.34 | 300 | scan=12.7 drift=+0.0% | 15:48:20 |
| S00 | 087R | win | 1 | 0.5891 | 5.9 | 3.48 | 300 | scan=9.0 drift=-34.4% | 13:08:32 |
| S00 | 162R | win | 1 | 0.3177 | 7.2 | 2.29 | 300 | scan=6.4 drift=+12.5% | 11:19:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 34 | +7.9% | -63.7% | +156.7% | 16 | 8 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 429.1s |
| **Latency** (scan→final max) | 599.8s |
| **Traffic** (notifications 24h) | 29 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 71 | 0.4368 | 0.2254 | +0.2114 | 🟡+48% | 0.2215 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 71 | 0.4368 | 0.2254 | 0.2215 | 🔴-0.27 | 0.766 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 35 | 0.4273 | 0.2000 | 🔴+0.2273 |
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
_auto-generated by claude_snapshot.py at 2026-04-30T11:10:01.608508+09:00_