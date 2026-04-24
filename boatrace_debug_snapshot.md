# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-24T23:20:01.917841+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×2 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×89 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-04-24T18:39:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-04-24T15:59:05]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CALIBRATION_DRIFT  ×33  [2026-04-24T13:57:29]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×6  [2026-04-24T13:52:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-04-24T11:00:36]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-04-24T06:00:06]
- key: `ORPHAN_SCAN|19 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|bt=win: n=25 pred=0.4263 actual=0.2000 error=+0.2263 (+53%) brier=0.2112 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|S00(win): n=25 pred=0.4263 hit=0.2000 cal_err=+0.2263 brier=0.2112 BSS=-0.32 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=10 pred=0.4423 actual=0.3000 gap=+0.1423`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-24T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.50+: n=10 pred=0.5301 actual=0.2000 gap=+0.3301`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-24T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-24T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.12MB / last modified 2026-04-24T23:19:05.778537+09:00

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
32 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-24 23:15:06,532 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-24 23:15:06,588 [INFO] predictor: Models loaded OK
2026-04-24 23:15:06,594 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-24 23:16:05,538 [INFO] run_cycle: === run_cycle 23:16:05 ===
2026-04-24 23:16:05,539 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-24 23:16:05,539 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-24 23:16:05,612 [INFO] predictor: Models loaded OK
2026-04-24 23:16:05,616 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-24 23:17:05,559 [INFO] run_cycle: === run_cycle 23:17:05 ===
2026-04-24 23:17:05,559 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-24 23:17:05,559 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-24 23:17:05,621 [INFO] predictor: Models loaded OK
2026-04-24 23:17:05,627 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-24 23:18:06,075 [INFO] run_cycle: === run_cycle 23:18:06 ===
2026-04-24 23:18:06,075 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-24 23:18:06,075 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-24 23:18:06,147 [INFO] predictor: Models loaded OK
2026-04-24 23:18:06,153 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-24 23:19:05,673 [INFO] run_cycle: === run_cycle 23:19:05 ===
2026-04-24 23:19:05,673 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-24 23:19:05,673 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-24 23:19:05,725 [INFO] predictor: Models loaded OK
2026-04-24 23:19:05,731 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 14, 'result': 11, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 160
  FINAL_MISSING: 89
  ANOMALY_BET_VOLUME_SPIKE: 3
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  CALIBRATION_DRIFT: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 9 | 10,500 | 10,200 | -300 | 0.971 |

## 直近アラート (24h・新しい順)
```
[23:05:07] FINAL_MISSING: {"deadline": "2026-04-24T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042409031127", "sid": "S00"}
[23:02:06] FINAL_MISSING: {"deadline": "2026-04-24T13:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042416061327", "sid": "S00"}
[23:02:06] FINAL_MISSING: {"deadline": "2026-04-24T20:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042401122030", "sid": "S00"}
[22:59:05] FINAL_MISSING: {"deadline": "2026-04-24T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042404061322", "sid": "S00"}
[22:59:05] FINAL_MISSING: {"deadline": "2026-04-24T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042404041222", "sid": "S00"}
[22:50:08] FINAL_MISSING: {"deadline": "2026-04-24T15:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042408111514", "sid": "S00"}
[22:40:09] FINAL_MISSING: {"deadline": "2026-04-24T14:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042416071405", "sid": "S00"}
[22:38:05] FINAL_MISSING: {"deadline": "2026-04-24T11:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042414061102", "sid": "S00"}
[22:27:06] FINAL_MISSING: {"deadline": "2026-04-24T12:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042416051250", "sid": "S00"}
[22:04:06] FINAL_MISSING: {"deadline": "2026-04-24T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042409031127", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 156件 締切済
- 通知発射: scan=19 nid / final=14 nid / result=11 nid
- predictions: 11 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 078R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=17.8 drift=-60.1% | 18:36:21 |
| S00 | 1610R | win | 1 | 0.5123 | 5.1 | 2.61 | 300 | scan=- drift=- | 15:34:32 |
| S00 | 168R | win | 1 | 0.5016 | 5.6 | 2.81 | 300 | scan=4.7 drift=+19.1% | 14:38:31 |
| S00 | 098R | win | 1 | 0.5113 | 5.4 | 2.76 | 300 | scan=5.2 drift=+3.8% | 13:57:22 |
| S00 | 047R | win | 1 | 0.4111 | 33.7 | 13.85 | 300 | scan=- drift=- | 13:50:23 |
| S00 | 097R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=- drift=- | 13:26:21 |
| S00 | 087R | win | 1 | 0.5476 | 9.7 | 5.31 | 300 | scan=4.5 drift=+115.6% | 13:07:32 |
| S00 | 164R | win | 1 | 0.4111 | 10.8 | 4.44 | 300 | scan=4.5 drift=+140.0% | 12:16:19 |
| S00 | 043R | win | 1 | 0.5476 | 28.5 | 15.61 | 300 | scan=- drift=- | 11:50:34 |
| S00 | 163R | win | 1 | 0.1371 | 5.1 | 0.70 | 300 | scan=6.7 drift=-23.9% | 11:47:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 19 | +13.6% | -68.2% | +156.7% | 7 | 4 | 17 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 534.7s |
| **Latency** (scan→final max) | 609.1s |
| **Traffic** (notifications 24h) | 44 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 36 | 0.4350 | 0.2500 | +0.1850 | 🟡+42% | 0.2324 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 36 | 0.4350 | 0.2500 | 0.2324 | 🔴-0.24 | 0.944 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 16 | 0.4268 | 0.1875 | 🔴+0.2393 |
| 0.50+ | 16 | 0.5271 | 0.3125 | 🔴+0.2146 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 1 | 0.35 |
| win | <10.0 | ⚠️fallback | 7 | 0.32 |
| win | <20.0 | ⚠️fallback | 1 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-04-24T23:20:01.917841+09:00_