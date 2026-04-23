# ClaudeDebug スナップショット

## 🟡 現状: YELLOW

**生成**: 2026-04-24T04:10:01.543118+09:00

### 次に取るべきアクション
> YELLOW監視: FINAL_MISSING×46 (24h)

### 検出された問題
- 🟡 FINAL_MISSING×46 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-04-23T17:31:29]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×12  [2026-04-23T17:21:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-04-23T11:00:49]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-04-23T06:00:07]
- key: `ORPHAN_SCAN|14 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-23T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=22 pred=0.4170 actual=0.2273 error=+0.1897 (+45%) brier=0.2060 [OVERCO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-23T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=22 pred=0.4170 hit=0.2273 cal_err=+0.1897 brier=0.2060 BSS=-0.17 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=8 pred=0.4391 actual=0.3750 gap=+0.0641`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=9 pred=0.5253 actual=0.2222 gap=+0.3030`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-23T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-23T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.09MB / last modified 2026-04-24T04:00:02.225421+09:00

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
81 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-23 23:55:05,381 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-23 23:55:05,425 [INFO] predictor: Models loaded OK
2026-04-23 23:55:05,429 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-23 23:56:05,926 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-04-23 23:56:05,926 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-23 23:56:05,926 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-23 23:56:05,970 [INFO] predictor: Models loaded OK
2026-04-23 23:56:05,975 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-23 23:57:06,076 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-04-23 23:57:06,076 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-23 23:57:06,076 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-23 23:57:06,125 [INFO] predictor: Models loaded OK
2026-04-23 23:57:06,128 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-23 23:58:05,423 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-04-23 23:58:05,423 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-23 23:58:05,423 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-23 23:58:05,479 [INFO] predictor: Models loaded OK
2026-04-23 23:58:05,481 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-23 23:59:05,110 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-04-23 23:59:05,110 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-23 23:59:05,110 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-23 23:59:05,162 [INFO] predictor: Models loaded OK
2026-04-23 23:59:05,172 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 20
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 20
  }
]
```

## Phase別通知記録 (24h)
{'final': 6, 'result': 3, 'scan': 11}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 203
  FINAL_MISSING: 46
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 25 | 5 | 7,500 | 6,120 | -1,380 | 0.816 |

## 直近アラート (24h・新しい順)
```
[23:58:05] FINAL_MISSING: {"deadline": "2026-04-23T16:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042312031624", "sid": "S00"}
[23:48:05] FINAL_MISSING: {"deadline": "2026-04-23T13:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042314101312", "sid": "S00"}
[23:38:05] FINAL_MISSING: {"deadline": "2026-04-23T14:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042305061401", "sid": "S00"}
[23:30:09] FINAL_MISSING: {"deadline": "2026-04-23T16:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042322101654", "sid": "S00"}
[23:05:06] FINAL_MISSING: {"deadline": "2026-04-23T13:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042322031329", "sid": "S00"}
[22:57:06] FINAL_MISSING: {"deadline": "2026-04-23T16:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042312031624", "sid": "S00"}
[22:47:05] FINAL_MISSING: {"deadline": "2026-04-23T13:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042314101312", "sid": "S00"}
[22:37:06] FINAL_MISSING: {"deadline": "2026-04-23T14:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042305061401", "sid": "S00"}
[22:29:05] FINAL_MISSING: {"deadline": "2026-04-23T16:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042322101654", "sid": "S00"}
[22:05:06] FINAL_MISSING: {"deadline": "2026-04-23T13:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026042322031329", "sid": "S00"}
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
| S00 | 206R | win | 1 | 0.5735 | 4.7 | 2.70 | 300 | scan=6.7 drift=-29.9% | 17:41:21 |
| S00 | 1611R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=8.7 drift=-54.0% | 16:07:32 |
| S00 | 226R | win | 1 | 0.4989 | 8.2 | 4.09 | 300 | scan=22.6 drift=-63.7% | 14:52:44 |
| S00 | 014R | win | 1 | 0.0156 | 45.3 | 0.71 | 300 | scan=- drift=- | 16:36:27 |
| S00 | 227R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=- drift=- | 15:19:20 |
| S00 | 118R | win | 1 | 0.3177 | 8.1 | 2.57 | 300 | scan=25.5 drift=-68.2% | 14:05:45 |
| S00 | 066R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=7.0 drift=+28.6% | 13:51:20 |
| S00 | 1810R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=- drift=- | 12:55:44 |
| S00 | 115R | win | 1 | 0.0838 | 5.2 | 0.44 | 300 | scan=- drift=- | 12:27:21 |
| S00 | 063R | win | 1 | 0.5151 | 5.2 | 2.68 | 300 | scan=4.2 drift=+23.8% | 12:20:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 12 | -7.8% | -68.2% | +33.3% | 5 | 3 | 11 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 571.1s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 20 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 25 | 0.4263 | 0.2000 | +0.2263 | 🔴+53% | 0.2112 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 25 | 0.4263 | 0.2000 | 0.2112 | 🔴-0.32 | 0.816 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 12 | 0.4247 | 0.2500 | 🔴+0.1747 |
| 0.50+ | 10 | 0.5301 | 0.2000 | 🔴+0.3301 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 1 | 0.35 |
| win | <10.0 | ⚠️fallback | 3 | 0.32 |
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
_auto-generated by claude_snapshot.py at 2026-04-24T04:10:01.543118+09:00_