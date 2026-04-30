# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-01T02:30:02.381018+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 CALIBRATION_DRIFT×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-01T02:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×53  [2026-04-30T23:07:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×53  [2026-04-30T23:07:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×18  [2026-04-30T19:44:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×41  [2026-04-30T13:41:41]
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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.48MB / last modified 2026-05-01T02:30:03.315002+09:00

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
18 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 23:55:06,618 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 23:55:06,662 [INFO] predictor: Models loaded OK
2026-04-30 23:55:06,666 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 23:56:05,229 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-04-30 23:56:05,229 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 23:56:05,229 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 23:56:05,306 [INFO] predictor: Models loaded OK
2026-04-30 23:56:05,310 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 23:57:05,969 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-04-30 23:57:05,969 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 23:57:05,969 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 23:57:06,037 [INFO] predictor: Models loaded OK
2026-04-30 23:57:06,042 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 23:58:06,274 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-04-30 23:58:06,274 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 23:58:06,274 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 23:58:06,322 [INFO] predictor: Models loaded OK
2026-04-30 23:58:06,328 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-30 23:59:05,298 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-04-30 23:59:05,298 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-30 23:59:05,298 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-30 23:59:05,343 [INFO] predictor: Models loaded OK
2026-04-30 23:59:05,348 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 31
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 31
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 6, 'scan': 15}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 61
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  ANOMALY_SCRAPER_FAILURE_BURST: 16
  CALIBRATION_DRIFT: 5
  ANOMALY_BET_VOLUME_DROP: 3
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 12 | 15,600 | 10,710 | -4,890 | 0.687 |

## 直近アラート (24h・新しい順)
```
[23:45:06] CIRCUIT_BREAKER_TRIP: {"cost": 15600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 10710, "roi_7d": 0.687, "sid": "S00"}
[23:42:06] FINAL_MISSING: {"deadline": "2026-04-30T18:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043024021808", "sid": "S00"}
[23:42:06] FINAL_MISSING: {"deadline": "2026-04-30T13:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043005031304", "sid": "S00"}
[23:29:06] FINAL_MISSING: {"deadline": "2026-04-30T10:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043021061054", "sid": "S00"}
[23:27:06] FINAL_MISSING: {"deadline": "2026-04-30T16:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043022101653", "sid": "S00"}
[23:09:05] FINAL_MISSING: {"deadline": "2026-04-30T16:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043019041635", "sid": "S00"}
[23:07:06] FINAL_MISSING: {"deadline": "2026-04-30T12:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043022011233", "sid": "S00"}
[23:07:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:59:05] FINAL_MISSING: {"deadline": "2026-04-30T17:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026043022111725", "sid": "S00"}
[22:45:06] CIRCUIT_BREAKER_TRIP: {"cost": 15600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 10710, "roi_7d": 0.687, "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 056R | win | 1 | 0.5735 | 5.4 | 3.10 | 300 | scan=- drift=- | 14:33:20 |
| S00 | 098R | win | 1 | 0.4111 | 5.9 | 2.43 | 300 | scan=15.8 drift=-62.7% | 13:50:35 |
| S00 | 149R | win | 1 | 0.2173 | 8.1 | 1.76 | 300 | scan=7.3 drift=+11.0% | 12:35:22 |
| S00 | 174R | win | 1 | 0.4989 | 17.1 | 8.53 | 300 | scan=- drift=- | 12:13:46 |
| S00 | 093R | win | 1 | 0.4989 | 9.0 | 4.49 | 300 | scan=6.7 drift=+34.3% | 11:22:21 |
| S00 | 172R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=8.1 drift=-3.7% | 11:07:46 |
| S00 | 1810R | win | 1 | 0.4111 | 5.5 | 2.26 | 300 | scan=- drift=- | 12:55:21 |
| S00 | 033R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=4.3 drift=+55.8% | 12:05:21 |
| S00 | 032R | win | 1 | 0.3177 | 8.8 | 2.80 | 300 | scan=- drift=- | 11:38:19 |
| S00 | 187R | win | 1 | 0.3177 | 14.7 | 4.67 | 300 | scan=16.6 drift=-11.4% | 11:16:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 34 | +11.7% | -63.0% | +156.7% | 14 | 7 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.9s |
| **Latency** (scan→final max) | 610.7s |
| **Traffic** (notifications 24h) | 31 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 77 | 0.4366 | 0.2208 | +0.2158 | 🟡+49% | 0.2223 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 77 | 0.4366 | 0.2208 | 0.2223 | 🔴-0.29 | 0.729 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 39 | 0.4301 | 0.2051 | 🔴+0.2250 |
| 0.50+ | 29 | 0.5344 | 0.2759 | 🔴+0.2585 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 4 | 0.35 |
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
_auto-generated by claude_snapshot.py at 2026-05-01T02:30:02.381018+09:00_