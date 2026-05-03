# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-03T18:50:02.239712+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×24 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×90 (24h)
- 🔴 CALIBRATION_DRIFT×24 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 PSI_DRIFT_DETECTED×10 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-05-03T18:20:25]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CALIBRATION_DRIFT  ×43  [2026-05-03T18:07:21]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×43  [2026-05-03T18:07:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×43  [2026-05-03T18:07:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-03T18:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×54  [2026-05-03T17:20:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×18  [2026-05-03T15:56:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×53  [2026-05-03T10:00:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-05-03T06:00:09]
- key: `ROI_STAT|S00: n=95 hit%=22.1% hit_CI[Bonf]=[12.4,36.4]% ROI=0.83 ROI_boot95=[0.49,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=95<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-03T06:00:09]
- key: `ORPHAN_SCAN|80 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=95 pred=0.4279 actual=0.2211 error=+0.2068 (+48%) brier=0.2309 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=95 pred=0.4279 hit=0.2211 cal_err=+0.2068 brier=0.2309 BSS=-0.34 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.2857 gap=-0.0630`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=7 pred=0.3232 actual=0.0000 gap=+0.3232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=38 pred=0.4490 actual=0.2368 gap=+0.2122`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.50+: n=35 pred=0.5340 actual=0.2286 gap=+0.3054`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-03T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-03T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-03T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.7MB / last modified 2026-05-03T18:49:29.775781+09:00

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
== run_cycle 18:48:05 ===
2026-05-03 18:48:05,388 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-03 18:48:05,388 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-03 18:48:05,433 [INFO] predictor: Models loaded OK
2026-05-03 18:48:05,526 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-03 18:49:06,014 [INFO] run_cycle: === run_cycle 18:49:06 ===
2026-05-03 18:49:06,014 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-03 18:49:06,014 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-03 18:49:06,090 [INFO] predictor: Models loaded OK
2026-05-03 18:49:18,612 [INFO] scraper: odds3t: 120/120 parsed
2026-05-03 18:49:19,925 [INFO] scraper: odds3f: 20/20 parsed
2026-05-03 18:49:21,094 [INFO] scraper: odds2t: 30/30 parsed
2026-05-03 18:49:21,096 [INFO] scraper: odds2f: 15/15 parsed
2026-05-03 18:49:22,181 [INFO] scraper: odds_win: 6/6 parsed
2026-05-03 18:49:22,181 [INFO] scraper: fetch_race 01/9: boats=6 odds=191/191
2026-05-03 18:49:22,193 [INFO] predictor: CALIBRATION_MODE=on
2026-05-03 18:49:22,193 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-03 18:49:22,200 [INFO] run_cycle: fetched 01/9 [final]: 156 combos
2026-05-03 18:49:25,840 [INFO] scraper: odds3t: 120/120 parsed
2026-05-03 18:49:26,982 [INFO] scraper: odds3f: 20/20 parsed
2026-05-03 18:49:28,421 [INFO] scraper: odds2t: 30/30 parsed
2026-05-03 18:49:28,423 [INFO] scraper: odds2f: 15/15 parsed
2026-05-03 18:49:29,520 [INFO] scraper: odds_win: 4/6 parsed
2026-05-03 18:49:29,520 [INFO] scraper: fetch_race 19/9: boats=6 odds=189/191
2026-05-03 18:49:29,529 [INFO] predictor: CALIBRATION_MODE=on
2026-05-03 18:49:29,537 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-03 18:49:29,541 [INFO] run_cycle: fetched 19/9 [scan]: 154 combos
2026-05-03 18:49:29,690 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 33
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 33
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 6, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 122
  FINAL_MISSING: 90
  CALIBRATION_DRIFT: 24
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  PSI_DRIFT_DETECTED: 10
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 8 | 14,100 | 9,810 | -4,290 | 0.696 |

## 直近アラート (24h・新しい順)
```
[18:48:05] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 9810, "roi_7d": 0.696, "sid": "S00"}
[18:48:05] CALIBRATION_DRIFT: {"avg_actual": 0.1702, "avg_pred": 0.4196, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 47, "overconf_pct": 59.4}
[18:46:06] FINAL_MISSING: {"deadline": "2026-05-03T17:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050307051716", "sid": "S00"}
[18:38:19] FINAL_MISSING: {"deadline": "2026-05-03T14:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050317071405", "sid": "S00"}
[18:24:33] FINAL_MISSING: {"deadline": "2026-05-03T15:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050307021553", "sid": "S00"}
[18:20:25] FINAL_MISSING: {"deadline": "2026-05-03T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050302011047", "sid": "S00"}
[18:17:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 54, "n_recent": 47, "psi": 0.956}
[18:14:42] FINAL_MISSING: {"deadline": "2026-05-03T15:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050301021542", "sid": "S00"}
[18:13:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 920}
[18:12:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 927}
```

## 本日残レース: 20件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 204件 登録 / 184件 締切済
- 通知発射: scan=17 nid / final=10 nid / result=6 nid
- predictions: 6 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 193R | win | 1 | 0.5174 | 5.5 | 2.85 | 300 | scan=11.2 drift=-50.9% | 16:15:21 |
| S00 | 192R | win | 1 | 0.5476 | 13.5 | 7.39 | 300 | scan=- drift=- | 15:45:22 |
| S00 | 098R | win | 1 | 0.4111 | 38.2 | 15.70 | 300 | scan=- drift=- | 13:51:44 |
| S00 | 093R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=- drift=- | 11:23:22 |
| S00 | 106R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=10.2 drift=-48.0% | 10:53:20 |
| S00 | 161R | win | 1 | 0.5174 | 5.4 | 2.79 | 300 | scan=4.5 drift=+20.0% | 10:49:20 |
| S00 | 076R | win | 1 | 0.2290 | 6.0 | 1.37 | 300 | scan=4.0 drift=+50.0% | 17:48:32 |
| S00 | 072R | win | 1 | 0.1957 | 7.6 | 1.49 | 300 | scan=40.8 drift=-81.4% | 15:54:45 |
| S00 | 178R | win | 1 | 0.3177 | 45.7 | 14.52 | 300 | scan=- drift=- | 14:33:32 |
| S00 | 167R | win | 1 | 0.4989 | 4.9 | 2.44 | 300 | scan=4.7 drift=+4.3% | 14:06:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 33 | -3.8% | -81.4% | +117.3% | 14 | 10 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 490.7s |
| **Latency** (scan→final max) | 609.9s |
| **Traffic** (notifications 24h) | 33 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 101 | 0.4304 | 0.2178 | +0.2125 | 🟡+49% | 0.2301 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 101 | 0.4304 | 0.2178 | 0.2301 | 🔴-0.35 | 0.817 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.20-0.30 | 7 | 0.2227 | 0.2857 | 🔴-0.0630 |
| 0.30-0.50 | 48 | 0.4283 | 0.1875 | 🔴+0.2408 |
| 0.50+ | 38 | 0.5335 | 0.2368 | 🔴+0.2967 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 5 | 0.35 |
| win | <10.0 | ✅learned | 15 | 0.59 |
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
_auto-generated by claude_snapshot.py at 2026-05-03T18:50:02.239712+09:00_